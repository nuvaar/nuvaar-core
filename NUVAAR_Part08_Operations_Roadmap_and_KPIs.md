# NUVAAR Omega Full Launch
# Part 08 - Operations, Roadmap, and KPIs

Language is English only. ASCII only. No special dashes or spaces. This chapter makes NUVAAR operational. It defines how we run cycles, measure health, publish reports, handle incidents, and improve week by week without losing sight of dignity.

## 1. Operating Model

### 1.1 Cadence
- Weekly: cell check in, ops triage, transparency draft updates.
- Biweekly: governance review window and backlog grooming.
- Monthly: treasury report, KPI review, budget reforecast, partner sync.
- Quarterly: strategy review, risk audit, and OKR reset.

### 1.2 Pods
- Cells Pod: facilitators, mentors, and a data steward for RLS checks.
- Product Pod: site, admin, integrations, and accessibility.
- Atlas Pod: editorial, translation, preservation.
- Treasury Pod: treasurer, reviewer pair, and reporting.
- Safety Pod: security officer, incident lead, comms liaison.

### 1.3 RACI Pattern
- Responsible: executes the task.
- Accountable: owns the outcome and signs off.
- Consulted: provides input.
- Informed: receives updates.

## 2. Core Playbooks

### 2.1 Onboarding
- Intake: email, path, bio, availability, access needs.
- Screen: 20 minute call or async chat. Confirm goals and constraints.
- Consent: plain language summary, privacy and exit rights.
- Match: assign to a cell or waiting list with a date.
- Kickoff: run role cards and set first milestone.

### 2.2 Cell Lifecycle
- Kickoff ritual with smallest outcome that matters.
- Weekly check in 45 minutes. Board columns: now, next, blocked.
- Midpoint reset: cut scope if needed to protect dignity and delivery.
- Demo day: public link and case note.
- Retro: one page lessons and process tweaks.

### 2.3 Grant And Payment
- Proposal: problem, outcome, budget, risks, KPIs, timeline.
- Review: ethics and privacy notes, data steward sign off.
- Vote: Snapshot signal.
- Execute: Safe transaction bundle, milestone gates.
- Report: deliverables, receipts, lessons, next steps.

### 2.4 Content Publishing
- Intake form with metadata and license.
- Editorial review within 7 days.
- Accessibility pass: alt text, captions, contrast.
- Publish with stable URL and archive package.
- Update broken links within 72 hours.

### 2.5 Security Incident
- Detect and confirm.
- Contain. Isolate affected components.
- Notify within 24 hours with what we know.
- Eradicate root cause and verify.
- Recover and monitor.
- Publish an anonymized report and action items.

### 2.6 Data Subject Requests
- Acknowledge within 7 days.
- Verify identity and scope.
- Fulfill within 30 days or explain delay.
- Log request and close with confirmation.

### 2.7 Moderation
- Enforce Code of Conduct.
- Ladder: warn, time out, ban by vote if needed.
- Appeals to an uninvolved editor or facilitator.

### 2.8 Vendor Onboarding And Offboarding
- Due diligence checklist.
- DPA signed. Data map updated.
- Access keys scoped and rotated on exit.
- Confirm deletion where possible.

### 2.9 Accessibility QA
- Use a checklist for pages and assets.
- Fix blockers before publish.
- Track pass rate and defects by category.

### 2.10 Localization
- Identify priority languages.
- Prepare terminology list.
- Translate with review and author sign off.
- Publish and track feedback.

### 2.11 Ambassador Program
- Recruit 3 pilot regions.
- KPI: events held, members joined, works published.
- Provide a starter kit and monthly check ins.

## 3. Roadmap

### 3.1 0 to 30 Days
- Domain and deployment live.
- Home, Vision, Join pages published.
- Snapshot space and Safe created and documented.
- Two pilot cells formed and matched.
- Data policy and ethics pages live.
- Exit rules: if 2 cells cannot form, expand partner outreach and slip by 2 weeks maximum.

### 3.2 30 to 90 Days
- Five active cells.
- Twenty completed projects.
- Public KPI dashboard with daily refresh.
- First grants booked and reported.
- Atlas publishes 10 works.
- Exit rules: if deliveries lag, reduce scope and add mentoring hours rather than cutting quality controls.

### 3.3 90 to 180 Days
- FluxSkin v0.2 pilot.
- Atlas archive v1.0 with preservation plan online.
- Ambassadors active in three regions.
- Recurring income equals 1000 to 2000 USD per month.
- Exit rules: if income target misses, analyze price, channels, and offer. Publish adjustments.

### 3.4 Release Rhythm
- Weekly minor releases on site and admin.
- Monthly playbook updates with change notes.
- Quarterly program review and reset.

## 4. KPIs With Definitions And Formulas

Each KPI lists name, definition, formula, target, owner, source, privacy tier, and review cadence.

### 4.1 Activity
- Active users: number of unique accounts that performed an action in the last 7 days.
  - Formula: count(distinct user_id) where action_date >= today - 7.
  - Target: 50 by day 90.
  - Owner: product lead.
  - Source: event table with non identifying keys.
  - Privacy: aggregated.
  - Review: weekly.

- Active cells: cells with a check in or deliverable in the last 14 days.
  - Target: 5 by day 90.

- Retention 30 day: percent of users active in the current 7 day window who were also active 23 to 30 days earlier.
  - Target: 70 percent by day 90.

### 4.2 Production
- Completed projects: status equals done within period.
  - Target: 20 by day 90.
- Lead time: median days from Gate 1 to final deliverable.
  - Target: under 60 days.
- Quality rating: average rubric score across dimensions.
  - Target: 3.0 or higher.

### 4.3 Livelihood
- Ecosystem income: total USD equivalent where funds entered the treasury or creators.
  - Target: 500 USD by day 90.
- Payout speed: median days from approval to payment.
  - Target: under 7 days.
- Income diversity index: 1 minus sum of squared share by source category.
  - Target: trending upward quarterly.

### 4.4 Safety
- Incident count: number of logged incidents by severity.
  - Target: low and disclosed.
- Mean time to resolve: average hours from open to close for Sev2 and Sev3.
  - Target: under 72 hours for Sev2.
- Burnout signals: anonymized survey and opt in check ins.
  - Target: publish trends and actions, not raw scores.

### 4.5 Culture
- Public works: count of Atlas publications in period.
  - Target: 10 by day 90.
- Translations: unique languages added.
  - Target: 2 by day 180.
- Events: number of community sessions or workshops.
  - Target: monthly cadence.

## 5. Dashboard Specifications

### 5.1 Data Model
- Table kpi_daily(metric text, value numeric, window text, collected_at date, note text).
- Views for activity, production, livelihood, safety, and culture.
- No personal data in dashboards.

### 5.2 Refresh
- Daily at 02:00 UTC for aggregates.
- Real time for simple counts on landing pages where safe.
- SLA: dashboard ready by 08:00 local time for core regions.

### 5.3 Visuals
- Activity: 7 day rolling line.
- Production: bar by status.
- Livelihood: stacked area by source.
- Safety: table by severity with sparkline.
- Culture: list of latest works with tags.

## 6. SLOs And Error Budgets

- Site availability SLO: 99.90 percent monthly.
  - Error budget: 43 minutes per month.
  - Policy: pause feature rollouts if budget spent.

- Join form success SLO: 99.50 percent successful submissions.
  - Budget: 0.50 percent failures before rollback.

- Admin latency SLO: 95th percentile under 500 ms for key pages.
  - Budget: if exceeded for 3 days, prioritize performance fixes.

- Payout cycle SLO: median under 7 days from approval.
  - Budget: if missed in a month, a retro assigns owners and improvements.

## 7. Budget And Procurement

### 7.1 Cost Centers
- Micro grants.
- Facilitation and moderation.
- Infrastructure and security.
- Accessibility and translation.
- Atlas editorial and preservation.
- Experiments and research.

### 7.2 Approval Matrix
- Under 200 USD: treasurer and one reviewer.
- 200 to 1000 USD: treasurer plus program owner and one reviewer.
- Above 1000 USD: DAO vote and Safe threshold.

### 7.3 Forecasting
- Rolling 3 month forecast updated monthly.
- Burn rate target: 3000 to 5000 USD per month in pilot.
- Reserve target: 3 months of operating costs.

## 8. OKR Framework

### 8.1 Structure
- Set 3 to 4 Objectives per quarter.
- 3 to 5 Key Results per Objective.
- Each KR has a clear measure, owner, and due date.

### 8.2 Example Q1
Objective: make NUVAAR credible and useful for early members.
- KR1: reach 50 weekly active users by day 90.
- KR2: complete 20 projects with public outcomes.
- KR3: publish 10 works in Atlas.
- KR4: reduce payout median to under 7 days.

Review cadence: weekly check, monthly score, and quarter retro.

## 9. Meeting Cadences And Rituals

- Weekly ops standup: 25 minutes. Agenda sent the day before.
- Governance window: comments close every other Friday.
- Treasury review: first Monday monthly.
- Editorial meeting: weekly for Atlas.
- Postmortem review: within 7 days of Sev2 or higher incident.

Rules
- Start and end on time.
- Notes posted within 24 hours.
- Parking lot for off topic items.

## 10. On Call And Escalation

- Primary and secondary rotation covering business hours in core regions.
- Escalation ladder: on call, product lead, security officer, founder.
- Runbook links are visible in the on call calendar entry.
- Handover note at shift change with open issues and risks.

## 11. Change And Release Management

- Use feature flags for risky changes.
- Stage releases. Deploy to staging, run smoke tests, then promote.
- Maintain a public changelog for user visible changes.
- Rollback plan documented for each release.

## 12. Compliance Tasks Calendar

- Monthly: treasury report, KPI dashboard audit, access review for admin roles.
- Quarterly: privacy report, backup restore drill, key rotation check, governance metrics.
- Annual: external review where budget allows, policy refresh, license scans.

## 13. Risk Management

### 13.1 Register Template
- Risk, owner, likelihood 1 to 5, impact 1 to 5, score, mitigation, residual, review date.

### 13.2 Heat Policy
- Score 15 to 25: immediate action and weekly review.
- Score 8 to 14: plan within 30 days and monthly review.
- Score 1 to 7: monitor and assign a check in date.

## 14. Reporting Templates

### 14.1 Monthly Transparency Report

```md
Period: 2025-10
Treasury
- Start balance: 0000 USD
- Income: 0000 USD
- Expenses: 0000 USD
- End balance: 0000 USD
Program
- Active cells: 0
- Completed projects: 0
- Payout median: 0 days
Culture
- Atlas publications: 0
Notes: highlights, risks, and next steps.
```

### 14.2 Quarterly Impact Statement

```md
Outcomes: what changed for people and communities.
Evidence: links to works, public feedback, and KPIs.
Equity: inclusion metrics and access notes.
Dignity: privacy and safety measures taken.
Next: priorities for the next quarter.
```

### 14.3 Postmortem Template

```md
Title: concise summary
Impact: who felt it and how
Timeline: key events
Root causes: facts, not blame
Fixes: immediate, short term, long term
Follow up tasks: owners and due dates
```

## 15. Data Exports And Views

- KPI export: CSV with date, metric, value, window.
- Treasury export: CSV with date, category, amount, reference id.
- Atlas index: JSON with work ids, titles, authors, licenses, and URLs.
- Cell directory: CSV with cell id, facilitator, status, region.

## 16. Tooling And Automation

- GitHub Actions for CI with lint, type, test, and build.
- Scheduled jobs for KPI aggregation and backup verification.
- Bots for stale issue reminders and meeting note templates.
- Plausible analytics for public pages with privacy first settings.

## 17. People Practices

- Written briefs for work requests.
- No after hours paging unless Sev2+.
- Time off is documented and respected.
- Recognition is public and concrete.
- Feedback is kind, specific, and actionable.

## 18. Closing Note

Operations are about making care repeatable. When dignity is a constraint, quality improves and trust compounds. Keep the cycles short, the data honest, and the promises visible.
