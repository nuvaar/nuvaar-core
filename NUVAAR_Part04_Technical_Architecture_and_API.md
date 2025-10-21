# NUVAAR Omega Full Launch
# Part 04 - Technical Architecture And API

Language is English only. ASCII only. No special dashes or spaces. This chapter defines the full stack architecture, data model, security posture, API surface, CI and SRE practices needed to run NUVAAR in production. It is written to be practical for engineers and auditable by stakeholders.

## 1. Architecture Overview

NUVAAR uses a modern web stack with clear boundaries and minimum moving parts. The goal is reliability, safety, and a humane developer experience.

- Frontend: Next.js App Router, React 18, Tailwind CSS, shared UI package.
- Backend: Supabase Postgres with Row Level Security and Edge Functions.
- Auth: Supabase Auth with magic link for admin and session tokens for site.
- Governance Integrations: Snapshot for voting, Gnosis Safe for treasury.
- Storage: object storage for media, IPFS for cultural archive when needed.
- Observability: Sentry plus OpenTelemetry for traces and metrics.
- Delivery: Vercel or Netlify for site, GitHub Actions for CI.
- Secrets: platform secret managers and local .env files.

### 1.1 ASCII Diagram

```
[ Client Browser ]
    |
    v
[ Next.js App Router ] -- fetch --> [ API Routes ] -- supabase-js --> [ Supabase Postgres ]
    |                                     |                                   |
    |                                     v                                   v
    |                              [ Edge Functions ]                 [ RLS Policies ]
    |
    v
[ Public Pages ] <-> [ Auth Flows ] <-> [ Join Form ] <-> [ Cells, Projects, KPIs ]

Governance:
[ Snapshot Space ] <-> off chain votes
[ Gnosis Safe ]   <-> on chain multisig execution

Observability:
[ Sentry ] + [ OTel ] -> alerts, logs, traces
```

## 2. Monorepo Structure

- apps/site: public site, API routes for join and simple health checks.
- apps/admin: admin panel for sign in, dashboards, cells, projects, incidents.
- packages/ui: shared UI components.
- packages/config: shared tsconfig and lint configs.
- infra/supabase: schema.sql, policies.sql, seed scripts.

Code owners are assigned per package. Changes to infra require a reviewer from security or data stewardship.

## 3. Environments

- Local: developer machine with .env and Supabase project.
- Staging: same settings as prod with fake data and disabled emails to real users.
- Production: locked migrations, audited secrets, on call rotation enabled.

Promote only through CI. Do not push from laptops to production services.

## 4. Dependencies And Versions

- Node 20, pnpm 9, Next 14, React 18.
- supabase-js 2.x, lucide-react for icons.
- tailwindcss 3.x, postcss, autoprefixer.
- vitest for unit tests, Playwright for e2e.

Pin versions in package.json. Run dependency audit weekly.

## 5. Frontend Architecture

### 5.1 Routing And Data Fetching
- App Router with server components for static and dynamic pages.
- API routes under app/api for small public writes like join.
- Data fetching with supabase-js on the server for public reads with anon key.

### 5.2 State And Forms
- React state is local for forms and UI only.
- Form validation is server side plus client hints.
- The join form posts to an API route which inserts into join_requests.

### 5.3 Accessibility
- WCAG AA contrast and keyboard navigation.
- Use semantic HTML. Every interactive element has a visible focus state.
- Do not rely on color alone to convey meaning.

### 5.4 Performance
- Static generation for mostly static pages.
- Dynamic rendering for lists that change often.
- Image optimization through Next built in pipeline.
- Targets: LCP under 2.5s, CLS near 0.01, TBT under 200ms on mid range devices.

### 5.5 SEO And Analytics
- Metadata and OG tags in layout.
- robots.txt and sitemap.xml provided.
- Plausible analytics with domain env. No ads cookies.

## 6. Backend And Data

### 6.1 Schema

The following tables are required. Column types shown as hints.

- users: id uuid pk, email text unique, role text, created_at timestamptz.
- profiles: user_id uuid pk fk users, display_name text, bio text, skills text[], country text, lang text, privacy_opt boolean, kyc_flag boolean.
- cells: id uuid pk, name text, facilitator_id uuid, status text, created_at timestamptz.
- cell_members: cell_id uuid, user_id uuid, role text, joined_at timestamptz, pk(cell_id, user_id).
- projects: id uuid pk, cell_id uuid, title text, outcome text, milestone_json jsonb, status text, public_url text.
- transactions: id uuid pk, project_id uuid, amount_usd numeric, type text, tx_hash text, created_at timestamptz.
- incidents: id uuid pk, cell_id uuid, severity text, note text, created_at timestamptz, resolved_at timestamptz.
- kpis: id uuid pk, metric text, value numeric, window text, note text, created_at timestamptz.
- join_requests: id uuid pk, email text, path text, bio text, created_at timestamptz, user_id uuid.

Indexes should cover foreign keys and frequent queries. Example: idx_projects_cell_id, idx_cell_members_user_id, idx_kpis_metric_window.

### 6.2 RLS Policies

Enable RLS on all tables. Examples below are minimal and must be reviewed per region.

```sql
alter table profiles enable row level security;
alter table cells enable row level security;
alter table cell_members enable row level security;
alter table projects enable row level security;
alter table transactions enable row level security;
alter table incidents enable row level security;
alter table kpis enable row level security;
alter table join_requests enable row level security;

-- profiles: self
create policy profiles_sel_self on profiles for select using (user_id = auth.uid());
create policy profiles_upd_self on profiles for update using (user_id = auth.uid()) with check (user_id = auth.uid());

-- cells: public read, facilitator writes
create policy cells_sel_public on cells for select using (true);
create policy cells_upd_facilitator on cells for update using (facilitator_id = auth.uid());

-- cell_members: members read their cell
create policy cell_members_sel_cell on cell_members for select using (
  exists(select 1 from cell_members cm where cm.cell_id = cell_members.cell_id and cm.user_id = auth.uid())
);

-- projects: public read summary, members write
create policy projects_sel_public on projects for select using (true);
create policy projects_ins_member on projects for insert with check (
  exists(select 1 from cell_members cm where cm.user_id = auth.uid() and cm.cell_id = projects.cell_id)
);
create policy projects_upd_member on projects for update using (
  exists(select 1 from cell_members cm where cm.user_id = auth.uid() and cm.cell_id = projects.cell_id)
);

-- transactions: read by project members, insert by service role
create policy tx_sel_member on transactions for select using (
  exists(select 1 from projects p join cell_members cm on cm.cell_id = p.cell_id
         where p.id = transactions.project_id and cm.user_id = auth.uid())
);

-- incidents: read and write by members of the cell
create policy inc_sel_member on incidents for select using (
  exists(select 1 from cell_members cm where cm.cell_id = incidents.cell_id and cm.user_id = auth.uid())
);
create policy inc_ins_member on incidents for insert with check (
  exists(select 1 from cell_members cm where cm.cell_id = incidents.cell_id and cm.user_id = auth.uid())
);

-- kpis: public read, service role writes
create policy kpi_sel_public on kpis for select using (true);

-- join requests: anyone can insert, owner can read
create policy jr_ins_any on join_requests for insert with check (true);
create policy jr_sel_self on join_requests for select using (user_id = auth.uid() or email = auth.email());
```

### 6.3 Migrations

- Keep schema.sql as the canonical definition.
- Use a migrations folder with timestamped SQL files for changes.
- Every migration contains up and down statements where possible.
- Run migrations in CI for testing before deploy.

### 6.4 Sample Seeds

- Two pilot cells with facilitators.
- Three projects per cell with milestones.
- A handful of KPI records per day for a week.

Seeds should never include real emails or secrets.

## 7. API Surface

NUVAAR uses Next API routes for light writes and server components for reads. For heavy workloads, use Edge Functions.

### 7.1 Public API Routes

- POST /api/join
  - Body: email, path, bio.
  - Action: insert into join_requests.
  - Response: ok and request id.
  - Rate limit: 10 per hour per IP.
  - Notes: validate email format and path set.

- GET /api/health
  - Action: returns service status and build identifiers.
  - Use: uptime checks and troubleshooting.

- GET /api/kpi
  - Query: window or metric filter.
  - Action: read aggregated KPIs from public view.
  - Cache: 60 seconds on CDN.

### 7.2 Admin Endpoints

Admin pages call Edge Functions or server actions with service role where needed. Examples:

- POST admin/projects/create
  - Validates membership and budget limit.
  - Inserts project with initial status.

- POST admin/transactions/record
  - Service role insert after Safe execution reference is included.

### 7.3 Error Model

- Use HTTP status codes. 2xx success, 4xx client errors, 5xx server errors.
- JSON body contains code, message, and optional detail fields.
- Do not leak stack traces in production responses.
- Include a correlation id header for support.

### 7.4 Pagination And Filtering

- Use cursor based pagination for large lists.
- Query params use simple ASCII keys.
- Enforce caps on page size.

### 7.5 Idempotency

- For payment related writes, require an Idempotency-Key header.
- Store keys with a short TTL to prevent duplicate processing.

## 8. Security Controls

### 8.1 Authentication And Sessions
- Supabase Auth for user accounts with email based login.
- Magic link for admin sign in.
- Session cookies use httpOnly, secure, and sameSite strict where possible.

### 8.2 Authorization
- RBAC: member, facilitator, treasurer, data_steward, council.
- Enforce in two places: RLS and application checks.
- Do not trust client side claims without server verification.

### 8.3 CSRF And CORS
- CSRF: same site cookies and anti CSRF tokens for form posts.
- CORS: restrict origins to known domains for admin APIs.

### 8.4 Headers And CSP
- X Content Type Options nosniff.
- X Frame Options SAMEORIGIN.
- Content Security Policy that allows self and required domains only.

### 8.5 Rate Limiting
- CDN layer throttling for public routes.
- App layer counters for sensitive endpoints.

### 8.6 Secrets And Keys
- Store in platform secret store.
- Rotate on schedule and on role changes.
- Never log secrets or tokens.

## 9. Observability

### 9.1 Logging
- Structured JSON logs. Fields include level, timestamp, service, route, and correlation id.
- No personal payloads in logs.

### 9.2 Tracing And Metrics
- OpenTelemetry instrumentation for server routes and Edge Functions.
- Key metrics: request rate, error rate, latency, database query duration.

### 9.3 Alerts
- Uptime checks on health endpoint.
- Error rate thresholds with paging to on call.
- Budget alerts for spend anomalies if cloud cost APIs are available.

## 10. CI And CD

### 10.1 CI
- Lint, type check, unit tests, build both apps.
- Database migrations dry run.
- Artifacts: build stats and coverage report.

### 10.2 CD
- Deploy to staging on main merge.
- Manual promotion to production after smoke tests.
- Git tags for releases with change notes.

### 10.3 Quality Gates
- Build must pass. No critical lint errors.
- Tests must pass. Minimum coverage targets set per package.
- Lighthouse budget checks for key pages in CI where practical.

## 11. Testing Strategy

- Unit tests with Vitest for utilities and UI components.
- Component tests for critical UI states.
- Integration tests for API routes.
- End to end tests with Playwright for join and admin flows.
- Accessibility checks with axe tooling during e2e where stable.

## 12. Release And Change Management

- Semantic versioning for packages.
- Conventional commits for useful changelogs.
- Weekly release cadence for minor changes, on demand for critical fixes.

## 13. SRE And Operations

### 13.1 Health Checks
- GET /api/health returns ok, version, build time, and environment.
- Database liveness check in a separate path with caution to avoid heavy queries.

### 13.2 Backups
- Daily logical backups and weekly physical snapshots.
- Retention for 30 days by default.
- Test restores quarterly.

### 13.3 Disaster Recovery
- RPO 24 hours and RTO 24 hours for pilot. Improve as scale grows.
- Document failover steps and contact lists in the runbook.

### 13.4 On Call
- Primary and secondary rotation.
- Escalation policy with clear timelines.
- Postmortems published internally, summaries public when appropriate.

## 14. Cost And Scale

- Base monthly costs include hosting, database, storage, and observability.
- Avoid premature microservices. Optimize SQL and caching first.
- Scale read heavy pages with CDN and incremental static regeneration.

## 15. Governance Integrations

### 15.1 Snapshot
- Create a space, set voting strategies, and publish a how to vote page.
- Use signed messages to prove identity when posting votes or proposals via API clients.

### 15.2 Gnosis Safe
- Document owners, threshold, and spend policies.
- Payment requests must reference a proposal id and milestone id.
- Publish monthly treasury reports with links to transactions and receipts where safe.

## 16. Security Reviews

- Threat modeling for new features before build.
- Checklists for privacy, injection risks, auth and session issues, and supply chain.
- External security review before major program launches when budget allows.

## 17. Developer Onboarding

- Install Node and pnpm. Enable corepack.
- Copy env example to .env and fill values.
- Start dev with pnpm dev. Site on 3000, admin on 4000.
- Run tests with pnpm test. Lint with pnpm lint.
- Read Code of Conduct and Data Policy before making changes.

## 18. Appendices

### 18.1 Example Health Endpoint

```ts
export async function GET() {
  const body = {
    ok: true,
    service: "nuvaar-site",
    version: process.env.VERCEL_GIT_COMMIT_SHA || "dev",
    time: new Date().toISOString()
  };
  return Response.json(body);
}
```

### 18.2 Example CSP Header
Add to platform config.

```
Content-Security-Policy: default-src 'self'; img-src 'self' data:; script-src 'self' plausible.io; style-src 'self' 'unsafe-inline';
```

### 18.3 Idempotency Pattern

```ts
const key = req.headers.get("Idempotency-Key");
if (!key) return NextResponse.json({ error: "missing idempotency key" }, { status: 400 });
const existing = await kv.get(key);
if (existing) return NextResponse.json(existing);
const result = await doWork();
await kv.set(key, result, { ex: 3600 });
return NextResponse.json(result);
```

### 18.4 Playwright Smoke Test Sketch

```ts
import { test, expect } from "@playwright/test";
test("home loads and shows headline", async ({ page }) => {
  await page.goto("http://localhost:3000");
  await expect(page.getByText("NUVAAR")).toBeVisible();
});
```

## 19. Closing Note

This architecture favors clarity over complexity. Start small, measure in the open, and let safety and dignity guide technical choices. When scale arrives, the fundamentals will still hold.
