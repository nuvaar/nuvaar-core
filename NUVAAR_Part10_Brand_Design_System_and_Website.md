
# NUVAAR Omega Full Launch
# Part 10 - Brand, Design System, and Website Implementation

Language is English only. ASCII only. No special dashes or special spaces. This chapter defines how NUVAAR looks, sounds, and behaves across surfaces, and how the website is implemented to production standards. It covers brand, design tokens, UI components, accessibility, content style, site architecture, page specs, SEO, performance, security, theming, and launch operations.

## 1. Brand Platform

### 1.1 Name And Promise
- Name: NUVAAR.
- Promise: dignity, clarity, and visible care.
- Tagline candidates: Care at the center. Small groups. Real outcomes.

### 1.2 Voice And Tone
- Voice: confident, humane, and specific. Explain trade offs. Avoid hype.
- Tone slider: calm for policy, warm for community, direct for safety notices.
- Microcopy rules: use verbs, avoid jargon, prefer short sentences, show examples.

### 1.3 Values In Practice
- Dignity is a design constraint.
- Data minimalism is a default, not an afterthought.
- Transparency means the public can follow decisions to actions.

## 2. Accessibility Foundations

- WCAG 2.2 AA as a minimum.
- Keyboard navigation for all interactive elements.
- Focus is always visible. Avoid outlines set to none.
- Do not rely on color alone. Use icons, labels, or patterns.
- All images have alt text or empty alt when purely decorative.
- Video uses captions and audio uses transcripts.
- Motion is subtle and respectful. Reduce motion setting is honored.

## 3. Design Tokens

Define one source of truth for design. Names are readable and stable.

### 3.1 Color Tokens
- background.default: near black for calm depth.
- surface.default: dark gray for cards.
- text.primary: high contrast light.
- text.muted: medium light for secondary text.
- accent.primary: teal for actions.
- accent.warning: amber for warnings.
- accent.success: green for positive states.
- border.default: subtle gray for lines and dividers.

### 3.2 Typography Tokens
- font.family.base: Inter, system fallbacks.
- font.size.xs: 12
- font.size.sm: 14
- font.size.md: 16
- font.size.lg: 18
- font.size.xl: 20
- font.size.display: 36
- line.height.tight: 1.2
- line.height.base: 1.5
- line.height.loose: 1.7

### 3.3 Spacing And Radius
- space.1: 4
- space.2: 8
- space.3: 12
- space.4: 16
- space.6: 24
- space.8: 32
- radius.sm: 8
- radius.md: 12
- radius.lg: 16
- radius.xl: 24

### 3.4 Elevation
- shadow.sm: soft spread for small cards.
- shadow.md: medium for dialogs.
- shadow.lg: stronger for overlays.

### 3.5 Motion
- ease.standard: cubic with soft start and end.
- duration.fast: 120ms
- duration.base: 200ms
- duration.slow: 300ms

## 4. UI Kit

### 4.1 Core Components
- Button: sizes sm, md, lg. Variants primary, secondary, ghost, destructive.
- Input: text, email, textarea, password with show toggle.
- Select: searchable for long lists.
- Checkbox and Radio: large hit areas and clear focus.
- Toggle: for binary settings with labels on both sides.
- Badge: status and category labels.
- Card: section grouping with title and actions.
- Dialog: modal with focus trap and escape to close.
- Toast: non blocking alerts with timeouts and manual close.
- Table: responsive with row actions and empty state.
- Tabs: keyboard friendly. Active tab is clear.
- Timeline: milestones and gates with dates.
- KPI Tile: number, trend, and caption.
- Markdown Renderer: safe list of tags and anchors.

### 4.2 Patterns
- Forms: top aligned labels, helpful hints, and error messages tied to fields.
- Empty States: explain purpose, show a sample, and provide a primary action.
- Loading States: skeletons for cards and tables.
- Error States: apology, guidance, and a support link with a correlation id.
- Confirmation: clear action and cancel path. Never hide destructive actions.

### 4.3 Icons And Illustration
- Icon set: lucide or equivalent. Use consistent stroke.
- Illustration: abstract geometric shapes that suggest care and craft. No stock photos that stereotype people.

## 5. Content Style Guide

- Keep paragraphs short and concrete.
- Prefer active voice and present tense.
- Do not manufacture certainty. Name constraints and risks.
- Credits are explicit. Link to sources.
- Use content warnings when needed.
- Avoid sensational headlines. Express value, not shock.

## 6. Website Architecture

### 6.1 Information Architecture
- Home
- Vision
- Minds
- FluxSkin
- Atlas
- Join
- DAO
- Docs
- Contact

### 6.2 URL Pattern
- nuvaar.xyz/
- nuvaar.xyz/vision
- nuvaar.xyz/minds
- nuvaar.xyz/fluxskin
- nuvaar.xyz/atlas
- nuvaar.xyz/join
- nuvaar.xyz/dao
- nuvaar.xyz/docs
- nuvaar.xyz/contact

### 6.3 Navigation
- Global header with brand, primary links, and a prominent Join button.
- Footer with secondary links, contact, social, and legal.

## 7. Page Specifications

### 7.1 Home
- Headline that states value.
- Short copy that explains why NUVAAR exists.
- Primary call to action Join.
- Secondary call to action Learn.
- Section with KPI tiles pulled from public metrics.
- Featured projects and works.

### 7.2 Vision
- Principles, dignity protocol summary, roadmap highlights.
- Link to governance constitution and data policy.

### 7.3 Minds
- Program explanation, role cards, funding gates, and quality rubric.
- Form link to Join.
- Stories from cells with public links and licenses.

### 7.4 FluxSkin
- Product overview, safety notes, repair and care guides.
- Right to repair statement and parts catalog link.

### 7.5 Atlas
- Latest works, filters by format and language.
- Submission guidelines and editorial policy link.

### 7.6 Join
- Form with minimal fields: email, path, bio.
- Consent text and privacy summary.
- Confirmation page with next steps and timeline.

### 7.7 DAO
- Snapshot space link, Safe address, and monthly treasury report highlights.
- How to propose and vote guide.

### 7.8 Docs
- Governance, data, legal, and style guides.
- API notes and schema overview.

### 7.9 Contact
- Email, social links, and a basic contact form.
- Response time expectation and safety notes.

## 8. SEO And Metadata

- Titles under 60 characters where possible.
- Descriptions between 120 and 160 characters.
- Open Graph tags for title, description, and image.
- alt text on images and structured headings.
- Sitemap and robots files.
- Canonical links to avoid duplicate confusion.

## 9. Performance Budgets

- HTML under 50 KB per document where possible.
- CSS under 100 KB total.
- JS under 200 KB for landing pages and 300 KB for app pages at first paint.
- LCP under 2.5s on mid range devices.
- CLS under 0.1 and TBT under 200ms where practical.
- Lazy load images and non critical scripts.

## 10. Security Headers And CSP

- Strict Transport Security with long max age and include subdomains.
- X Content Type Options set to nosniff.
- X Frame Options set to SAMEORIGIN.
- Referrer Policy to strict origin when cross origin.
- Content Security Policy that allows self and required analytics only.

Example CSP
```
default-src 'self';
img-src 'self' data:;
script-src 'self' plausible.io;
style-src 'self' 'unsafe-inline';
font-src 'self' data:;
connect-src 'self' plausible.io;
```

## 11. Theming And Dark Mode

- Default theme is dark for calm reading and low glare.
- Light theme exists for preference toggles.
- Token based theming switches color variables only.
- Respect prefers color scheme setting.

## 12. Tailwind Tokens Sketch

Add tokens via CSS variables in globals and read them in the Tailwind config using plugin or extended theme values. Example snippets follow.

Example CSS variables
```css
:root {
  --bg: #0b0d0f;
  --surface: #14171a;
  --text: #e7e9ea;
  --muted: #9aa0a6;
  --accent: #0fe1c7;
  --warn: #cbb26a;
  --success: #45b36b;

  --radius-sm: 8px;
  --radius-md: 12px;
  --radius-lg: 16px;

  --shadow-sm: 0 1px 2px rgba(0,0,0,0.25);
  --shadow-md: 0 8px 24px rgba(0,0,0,0.35);
}
```

Example Tailwind config extension pseudo
```js
theme: {
  extend: {
    colors: {
      bg: "var(--bg)",
      surface: "var(--surface)",
      text: "var(--text)",
      muted: "var(--muted)",
      accent: "var(--accent)",
      warn: "var(--warn)",
      success: "var(--success)"
    },
    borderRadius: {
      sm: "var(--radius-sm)",
      md: "var(--radius-md)",
      lg: "var(--radius-lg)"
    },
    boxShadow: {
      sm: "var(--shadow-sm)",
      md: "var(--shadow-md)"
    }
  }
}
```

## 13. Example Components

### 13.1 Button Sketch

```tsx
type ButtonProps = {
  variant?: "primary" | "secondary" | "ghost" | "destructive";
  size?: "sm" | "md" | "lg";
  children: React.ReactNode;
} & React.ButtonHTMLAttributes<HTMLButtonElement>;

export function Button({ variant = "primary", size = "md", ...props }: ButtonProps) {
  const base = "inline-flex items-center justify-center rounded-md focus:outline-none focus-visible:ring transition";
  const sizes = {
    sm: "h-8 px-3 text-sm",
    md: "h-10 px-4 text-sm",
    lg: "h-12 px-6 text-base"
  }[size];
  const variants = {
    primary: "bg-[color:var(--accent)] text-black hover:opacity-90",
    secondary: "bg-[color:var(--surface)] text-[color:var(--text)] border border-[color:var(--muted)] hover:border-[color:var(--text)]",
    ghost: "bg-transparent text-[color:var(--text)] hover:bg-[color:var(--surface)]",
    destructive: "bg-red-600 text-white hover:bg-red-700"
  }[variant];
  return <button className={`${base} ${sizes} ${variants}`} {...props} />;
}
```

### 13.2 Card Sketch

```tsx
export function Card({ title, children, action }) {
  return (
    <section className="rounded-lg bg-[color:var(--surface)] shadow-md p-6">
      <header className="flex items-center justify-between">
        <h2 className="text-lg text-[color:var(--text)]">{title}</h2>
        {action}
      </header>
      <div className="mt-4 text-[color:var(--text)]">{children}</div>
    </section>
  );
}
```

### 13.3 KPI Tile Sketch

```tsx
export function KpiTile({ label, value, trend }) {
  return (
    <div className="rounded-md p-4 border border-[color:var(--muted)]">
      <div className="text-sm text-[color:var(--muted)]">{label}</div>
      <div className="text-2xl font-semibold text-[color:var(--text)] mt-1">{value}</div>
      {trend && <div className="text-xs mt-1">{trend}</div>}
    </div>
  );
}
```

## 14. Admin Panel UX

- Sign in with magic link or passkey where supported.
- Dashboard tiles for cells, projects, incidents, and KPIs.
- Filters and saved views for facilitators.
- Inline edit for statuses with undo.
- Audit trail on sensitive actions.
- Role based views: member, facilitator, treasurer, council.

Shortcuts
- G to go to a page. Slash to search.
- Shift K opens command menu.

## 15. Content Governance

- Content owners per page. Owner names are visible in the CMS.
- Draft and review states. No surprise publishes.
- Version history with change notes.
- Broken link checks nightly and on publish.
- Style lint for headings, links, and alt text presence.

## 16. CMS Structure

- Collections for pages, posts, works, and docs.
- Fields with clear help text and limits.
- Media library with alt text required.
- Preview mode for drafts.

## 17. Routing And Errors

- 404 page explains where to go and links to search.
- 500 page apologizes and provides a correlation id with a link to status.
- Status page shows current incidents and maintenance windows.

## 18. Analytics

- Plausible or similar privacy first tool.
- Events: join started, join submitted, doc viewed, work viewed.
- No cross site tracking, no fingerprinting, no ad cookies.

## 19. Localization Plan

- English first. Additional languages in a dictionary layer per route.
- Translation keys use clear names with comments.
- Date and number formats localize automatically.

## 20. Quality Assurance

### 20.1 Pre Publish Checks
- Links resolve. No 404s.
- Alt text and captions present.
- Contrast meets AA.
- Forms submit with both mouse and keyboard.
- PWA install works where configured.

### 20.2 Performance Checks
- Lighthouse scores tracked for key pages.
- Largest images compressed and lazy loaded.
- Unused CSS trimmed.

### 20.3 Security Checks
- Headers present and correct.
- Secrets absent from repo.
- Forms protected against CSRF and bots.

## 21. Launch Checklist

- Domain DNS to hosting provider.
- Env secrets set and tested.
- Supabase schema and RLS applied.
- Snapshot and Safe links live.
- Content reviewed by accessibility and legal.
- Monitoring and on call rotation ready.
- Public announcement post drafted and scheduled.

## 22. Asset Management

- Store brand assets in a public repo folder and a CDN bucket.
- Provide SVG for logos and PNG fallbacks.
- Include a do not list for logo misuse and background clashes.

## 23. Maintenance And Review

- Monthly content and design review.
- Quarterly accessibility and security review.
- Yearly brand alignment workshop with community input.

## 24. Appendix

### 24.1 Example Meta Block

```html
<meta name="title" content="NUVAAR - Dignity. Small groups. Real outcomes.">
<meta name="description" content="NUVAAR helps people build creative livelihood with dignity through Cells, ethical design, and a cultural archive.">
<meta property="og:type" content="website">
<meta property="og:title" content="NUVAAR">
<meta property="og:description" content="Dignity, small groups, real outcomes.">
<meta property="og:image" content="/og.png">
```

### 24.2 Example robots.txt

```txt
User-agent: *
Allow: /
Sitemap: https://nuvaar.xyz/sitemap.xml
```

### 24.3 Example netlify.toml

```toml
[build]
  command = "npm run build"
  publish = "apps/site/out"

[[headers]]
  for = "/*"
  [headers.values]
  X-Frame-Options = "SAMEORIGIN"
  X-Content-Type-Options = "nosniff"
  Referrer-Policy = "strict-origin-when-cross-origin"
```

### 24.4 Example vercel.json

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

## 25. Closing Note

Brand is a promise, not a paint layer. The design system and website express the promise with clarity, access, and care. When constraints tighten, we keep the rules that protect dignity and remove extras that do not.
