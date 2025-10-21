# NUVAAR Omega Full Launch
# Part 13 - Deployment and Monorepo Scaffold

Language is English only. ASCII only. No special dashes or special spaces. This chapter gives you a production ready monorepo scaffold for NUVAAR with deployment recipes for Vercel and Netlify. It includes a tree layout, package manifests, configs, example routes, Supabase schema and RLS, seed scripts, CI workflows, Docker files, and a step by step runbook.

## 1. Repository Layout

Root is a Turborepo style monorepo with two Next apps and shared packages.

```
nuvaar/
  apps/
    site/               # public website
    admin/              # admin panel
  packages/
    ui/                 # shared UI components
    config/             # shared linting and TypeScript config
    lib/                # shared utilities and API client
  infra/
    supabase/           # schema.sql, policies.sql, seed scripts
    deploy/             # vercel.json, netlify.toml, nginx.conf optional
    ci/                 # GitHub Actions workflows
    docker/             # Dockerfiles and compose
  scripts/              # project scripts and generators
  .github/
    workflows/          # CI workflows mirror of infra/ci
  .vscode/              # tasks and recommended extensions
  package.json
  turbo.json
  tsconfig.json
  .npmrc
  .editorconfig
  .gitignore
  README.md
  LICENSE
```

## 2. Root package.json

```json
{
  "name": "nuvaar",
  "private": true,
  "workspaces": [
    "apps/*",
    "packages/*"
  ],
  "scripts": {
    "dev": "turbo run dev --parallel",
    "build": "turbo run build",
    "lint": "turbo run lint",
    "typecheck": "turbo run typecheck",
    "format": "prettier -w .",
    "prepare": "husky install",
    "seed": "node scripts/seed.cjs",
    "migrate": "node scripts/migrate.cjs"
  },
  "devDependencies": {
    "turbo": "latest",
    "typescript": "5.6.3",
    "prettier": "3.3.3",
    "eslint": "8.57.0",
    "eslint-config-next": "14.2.5",
    "husky": "9.1.6",
    "lint-staged": "15.2.2"
  },
  "lint-staged": {
    "*.{ts,tsx,js,jsx,css,md,json}": "prettier -w"
  },
  "packageManager": "npm@10.9.0"
}
```

## 3. Turbo and TS configs

### 3.1 turbo.json

```json
{
  "pipeline": {
    "dev": {
      "cache": false
    },
    "build": {
      "dependsOn": ["^build"],
      "outputs": ["dist/**", ".next/**"]
    },
    "lint": {},
    "typecheck": {}
  }
}
```

### 3.2 tsconfig.json

```json
{
  "compilerOptions": {
    "target": "ES2022",
    "module": "ESNext",
    "moduleResolution": "Bundler",
    "lib": ["ES2022", "DOM", "DOM.Iterable"],
    "jsx": "react-jsx",
    "strict": true,
    "noEmit": true,
    "baseUrl": ".",
    "paths": {
      "@ui/*": ["packages/ui/src/*"],
      "@config/*": ["packages/config/*"],
      "@lib/*": ["packages/lib/src/*"]
    }
  }
}
```

## 4. Shared packages

### 4.1 packages/ui

```
packages/ui/
  package.json
  src/
    index.ts
    components/
      Button.tsx
      Card.tsx
      KpiTile.tsx
    styles/
      globals.css
```

Example component exports

```ts
export { Button } from "./components/Button";
export { Card } from "./components/Card";
export { KpiTile } from "./components/KpiTile";
```

### 4.2 packages/config

```
packages/config/
  package.json
  eslint/
    index.js
  tsconfig/
    base.json
```

Example eslint config

```js
module.exports = {
  root: false,
  extends: ["next/core-web-vitals"],
  rules: {
    "@next/next/no-img-element": "off"
  }
};
```

### 4.3 packages/lib

```
packages/lib/
  package.json
  src/
    env.ts
    api.ts
    i18n.ts
    auth.ts
```

env loader

```ts
export const env = {
  NEXT_PUBLIC_SITE_URL: process.env.NEXT_PUBLIC_SITE_URL || "",
  SUPABASE_URL: process.env.SUPABASE_URL || "",
  SUPABASE_ANON_KEY: process.env.SUPABASE_ANON_KEY || ""
};
```

## 5. Next apps

### 5.1 apps/site

```
apps/site/
  package.json
  next.config.mjs
  postcss.config.mjs
  tailwind.config.ts
  app/
    layout.tsx
    page.tsx
    vision/page.tsx
    minds/page.tsx
    fluxskin/page.tsx
    atlas/page.tsx
    join/page.tsx
    dao/page.tsx
    docs/page.tsx
    contact/page.tsx
    api/health/route.ts
  public/
    favicon.ico
    og.png
  styles/
    globals.css
```

Example layout

```tsx
export default function RootLayout({ children }: { children: React.ReactNode }) {
  return (
    <html lang="en">
      <head>
        <meta name="title" content="NUVAAR - Dignity. Small groups. Real outcomes." />
        <meta name="description" content="NUVAAR helps people build creative livelihood with dignity." />
      </head>
      <body className="bg-[color:var(--bg)] text-[color:var(--text)]">
        <header className="max-w-5xl mx-auto p-4 flex items-center justify-between">
          <a href="/" className="font-semibold">NUVAAR</a>
          <nav className="space-x-4">
            <a href="/vision">Vision</a>
            <a href="/minds">Minds</a>
            <a href="/fluxskin">FluxSkin</a>
            <a href="/atlas">Atlas</a>
            <a href="/join" className="px-3 py-1 rounded-md bg-[color:var(--accent)] text-black">Join</a>
          </nav>
        </header>
        <main className="max-w-5xl mx-auto p-4">{children}</main>
        <footer className="max-w-5xl mx-auto p-4 border-t border-[color:var(--muted)] mt-16 text-sm">
          <div className="flex flex-wrap items-center gap-4">
            <a href="/docs/terms">Terms</a>
            <a href="/docs/privacy">Privacy</a>
            <a href="/docs/cookies">Cookies</a>
            <span>legal@nuvaar.xyz</span>
          </div>
        </footer>
      </body>
    </html>
  );
}
```

Example home

```tsx
export default function Page() {
  return (
    <section className="space-y-8">
      <h1 className="text-3xl font-semibold">Dignity. Small groups. Real outcomes.</h1>
      <p>NUVAAR helps people turn creativity into livelihood with care. Cells, ethical design, and a cultural archive.</p>
      <div className="grid grid-cols-1 md:grid-cols-3 gap-4">
        <div className="rounded-md p-4 border border-[color:var(--muted)]">
          <div className="text-sm text-[color:var(--muted)]">Active Cells</div>
          <div className="text-2xl font-semibold">5</div>
        </div>
        <div className="rounded-md p-4 border border-[color:var(--muted)]">
          <div className="text-sm text-[color:var(--muted)]">Completed Projects</div>
          <div className="text-2xl font-semibold">20</div>
        </div>
        <div className="rounded-md p-4 border border-[color:var(--muted)]">
          <div className="text-sm text-[color:var(--muted)]">Atlas Works</div>
          <div className="text-2xl font-semibold">10</div>
        </div>
      </div>
    </section>
  );
}
```

Tailwind config

```ts
import type { Config } from "tailwindcss";
const config: Config = {
  content: ["./app/**/*.{ts,tsx}", "../../packages/ui/src/**/*.{ts,tsx}"],
  theme: {
    extend: {}
  },
  plugins: []
};
export default config;
```

globals.css

```css
:root {
  --bg: #0b0d0f;
  --surface: #14171a;
  --text: #e7e9ea;
  --muted: #9aa0a6;
  --accent: #0fe1c7;
}
html, body { height: 100%; }
body { background: var(--bg); color: var(--text); }
a { color: var(--accent); }
```

package.json

```json
{
  "name": "@nuvaar/site",
  "private": true,
  "scripts": {
    "dev": "next dev",
    "build": "next build",
    "start": "next start",
    "lint": "next lint",
    "typecheck": "tsc -p tsconfig.json --noEmit"
  },
  "dependencies": {
    "next": "14.2.5",
    "react": "18.3.1",
    "react-dom": "18.3.1",
    "tailwindcss": "3.4.13",
    "autoprefixer": "10.4.20",
    "postcss": "8.4.47"
  }
}
```

### 5.2 apps/admin

```
apps/admin/
  package.json
  next.config.mjs
  tailwind.config.ts
  app/
    layout.tsx
    page.tsx
    cells/page.tsx
    projects/page.tsx
    incidents/page.tsx
    kpis/page.tsx
    api/health/route.ts
  styles/globals.css
```

Admin home

```tsx
export default function Page() {
  return (
    <section className="space-y-4">
      <h1 className="text-2xl font-semibold">Admin</h1>
      <ul className="list-disc pl-6">
        <li><a href="/cells">Cells</a></li>
        <li><a href="/projects">Projects</a></li>
        <li><a href="/incidents">Incidents</a></li>
        <li><a href="/kpis">KPIs</a></li>
      </ul>
    </section>
  );
}
```

## 6. Supabase Schema And RLS

### 6.1 schema.sql

```sql
create table public.users (
  id uuid primary key default gen_random_uuid(),
  email text unique not null,
  role text not null check (role in ('member','facilitator','mentor','treasurer','council')),
  created_at timestamptz default now()
);

create table public.profiles (
  user_id uuid primary key references public.users(id) on delete cascade,
  display_name text,
  bio text,
  skills text[],
  country text,
  lang text,
  privacy_opt boolean default true
);

create table public.cells (
  id uuid primary key default gen_random_uuid(),
  name text not null,
  facilitator_id uuid references public.users(id),
  status text not null default 'active',
  created_at timestamptz default now()
);

create table public.cell_members (
  cell_id uuid references public.cells(id) on delete cascade,
  user_id uuid references public.users(id) on delete cascade,
  role text not null default 'member',
  joined_at timestamptz default now(),
  primary key (cell_id, user_id)
);

create table public.projects (
  id uuid primary key default gen_random_uuid(),
  cell_id uuid references public.cells(id) on delete cascade,
  title text not null,
  outcome text,
  milestone_json jsonb default '[]'::jsonb,
  status text not null default 'in_progress',
  public_url text,
  created_at timestamptz default now()
);

create table public.transactions (
  id uuid primary key default gen_random_uuid(),
  project_id uuid references public.projects(id) on delete cascade,
  amount_usd numeric(12,2) not null,
  kind text not null check (kind in ('grant','fee','expense','donation','payout')),
  tx_ref text,
  created_at timestamptz default now()
);

create table public.incidents (
  id uuid primary key default gen_random_uuid(),
  cell_id uuid references public.cells(id) on delete set null,
  severity text not null check (severity in ('sev1','sev2','sev3')),
  note text,
  created_at timestamptz default now(),
  resolved_at timestamptz
);

create table public.kpis (
  id uuid primary key default gen_random_uuid(),
  metric text not null,
  value numeric not null,
  window text not null,
  note text,
  created_at timestamptz default now()
);
```

### 6.2 policies.sql

```sql
alter table public.users enable row level security;
alter table public.profiles enable row level security;
alter table public.cells enable row level security;
alter table public.cell_members enable row level security;
alter table public.projects enable row level security;
alter table public.transactions enable row level security;
alter table public.incidents enable row level security;
alter table public.kpis enable row level security;

create policy profiles_self on public.profiles
  for select using (auth.uid() = user_id)
  with check (auth.uid() = user_id);

create policy cells_public on public.cells
  for select using (true);

create policy cell_members_by_user on public.cell_members
  for select using (auth.uid() = user_id);

create policy projects_by_cell on public.projects
  for select using (
    exists (
      select 1 from public.cell_members m
      where m.cell_id = projects.cell_id and m.user_id = auth.uid()
    )
  );

create policy kpis_public on public.kpis
  for select using (true);
```

### 6.3 seed.sql

```sql
insert into public.users (email, role) values
  ('founder@nuvaar.xyz', 'council'),
  ('facilitator@nuvaar.xyz', 'facilitator'),
  ('member1@nuvaar.xyz', 'member');

insert into public.cells (name, facilitator_id)
select 'Cell Alpha', id from public.users where email='facilitator@nuvaar.xyz';

insert into public.cell_members (cell_id, user_id, role)
select c.id, u.id, 'facilitator'
from public.cells c
join public.users u on u.email='facilitator@nuvaar.xyz';

insert into public.cell_members (cell_id, user_id, role)
select c.id, u.id, 'member'
from public.cells c
join public.users u on u.email='member1@nuvaar.xyz';

insert into public.projects (cell_id, title, status)
select c.id, 'First Outcome', 'in_progress' from public.cells c limit 1;

insert into public.kpis (metric, value, window, note)
values ('active_users_7d', 5, '7d', 'seed value');
```

## 7. Scripts

### 7.1 scripts/migrate.cjs

```js
import { execSync } from "node:child_process";
const env = process.env;
const supa = env.SUPABASE_DB_URL || "";
if (!supa) { console.error("Missing SUPABASE_DB_URL"); process.exit(1); }
execSync(`psql ${supa} -f infra/supabase/schema.sql`, { stdio: "inherit" });
execSync(`psql ${supa} -f infra/supabase/policies.sql`, { stdio: "inherit" });
console.log("Migration complete");
```

### 7.2 scripts/seed.cjs

```js
import { execSync } from "node:child_process";
const env = process.env;
const supa = env.SUPABASE_DB_URL || "";
if (!supa) { console.error("Missing SUPABASE_DB_URL"); process.exit(1); }
execSync(`psql ${supa} -f infra/supabase/seed.sql`, { stdio: "inherit" });
console.log("Seed complete");
```

## 8. CI Workflows

### 8.1 .github/workflows/ci.yml

```yaml
name: ci
on:
  push:
    branches: [ "main" ]
  pull_request:
    branches: [ "main" ]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: 20
          cache: npm
      - run: npm ci
      - run: npm run lint
      - run: npm run typecheck
      - run: npm run build
```

### 8.2 .github/workflows/deploy-vercel.yml

```yaml
name: deploy-vercel
on:
  push:
    branches: [ "main" ]
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: amondnet/vercel-action@v25
        with:
          vercel-token: ${{ secrets.VERCEL_TOKEN }}
          github-token: ${{ secrets.GITHUB_TOKEN }}
          vercel-args: "--prod"
          working-directory: ./apps/site
```

## 9. Hosting Configs

### 9.1 Vercel vercel.json

```json
{
  "cleanUrls": true,
  "headers": [
    {
      "source": "/(.*)",
      "headers": [
        {"key": "X-Frame-Options", "value": "SAMEORIGIN"},
        {"key": "X-Content-Type-Options", "value": "nosniff"},
        {"key": "Referrer-Policy", "value": "strict-origin-when-cross-origin"}
      ]
    }
  ]
}
```

### 9.2 Netlify netlify.toml

```toml
[build]
  command = "npm run build"
  publish = "apps/site/.next"
  ignore = "git diff --quiet HEAD^ HEAD apps/site"

[[headers]]
  for = "/*"
  [headers.values]
  X-Frame-Options = "SAMEORIGIN"
  X-Content-Type-Options = "nosniff"
  Referrer-Policy = "strict-origin-when-cross-origin"
```

## 10. Docker

### 10.1 docker/Dockerfile.site

```Dockerfile
FROM node:20-alpine AS builder
WORKDIR /app
COPY . .
RUN npm ci
RUN npm run build --workspaces --if-present && npm --workspace=apps/site run build

FROM node:20-alpine AS runner
WORKDIR /app
ENV NODE_ENV=production
COPY --from=builder /app/apps/site/.next ./.next
COPY --from=builder /app/apps/site/package.json ./package.json
RUN npm i --omit=dev
EXPOSE 3000
CMD ["npx", "next", "start", "-p", "3000"]
```

### 10.2 docker-compose.yaml

```yaml
services:
  site:
    build:
      context: .
      dockerfile: docker/Dockerfile.site
    environment:
      - NEXT_PUBLIC_SITE_URL=http://localhost:3000
    ports:
      - "3000:3000"
```

## 11. Makefile

```make
.PHONY: dev build lint typecheck seed migrate

dev:
	npm run dev

build:
	npm run build

lint:
	npm run lint

typecheck:
	npm run typecheck

migrate:
	npm run migrate

seed:
	npm run seed
```

## 12. .env.example

```
NEXT_PUBLIC_SITE_URL=http://localhost:3000
SUPABASE_URL=
SUPABASE_ANON_KEY=
SUPABASE_SERVICE_ROLE=
SUPABASE_DB_URL=postgres://user:pass@host:5432/db
SNAPSHOT_SPACE_ID=
SAFE_TREASURY_ADDRESS=
PLAUSIBLE_DOMAIN=nuvaar.xyz
PLAUSIBLE_API=
```

## 13. VS Code Hints

```
.vscode/
  extensions.json
  settings.json
  tasks.json
```

Example extensions

```json
{
  "recommendations": [
    "dbaeumer.vscode-eslint",
    "esbenp.prettier-vscode",
    "bradlc.vscode-tailwindcss"
  ]
}
```

## 14. Deployment Runbook

1. Create GitHub repo nuvaar.
2. Push the monorepo skeleton or import from a template.
3. Create Supabase project. Get URL, anon key, and DB URL.
4. Set SUPABASE_DB_URL locally and run:
   - npm run migrate
   - npm run seed
5. In Vercel create a new project from apps/site directory. Set env vars:
   - NEXT_PUBLIC_SITE_URL
   - SUPABASE_URL
   - SUPABASE_ANON_KEY
6. Deploy. Confirm health at /api/health.
7. Add custom domain nuvaar.xyz and set DNS.
8. Repeat for apps/admin if deployed separately.
9. Enable GitHub Action deploy workflow with VERCEL_TOKEN secret.
10. Create Snapshot space and a Safe. Link them on the DAO page.
11. Publish Terms, Privacy, and Cookies pages under /docs.

## 15. Admin Auth Note

For pilot use magic link providers or Supabase Auth with email link. Keep roles in users.role and protect admin routes with middleware that checks role and session.

## 16. Status And Observability

- Add a simple status page under /status with build time and health checks.
- Use Logflare or Sentry for error tracking.
- Expose a public version file at /version.json with a build id and date.

## 17. Closing Note

This scaffold is designed to be copied into a repo and used as a base for NUVAAR. It is minimal where it should be and strict where it matters: access, data, and deploy discipline.
