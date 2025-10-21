# NUVAAR Omega Full Launch
# Part 03 - Data, Privacy, and Security

Language is English only. ASCII only. No special dashes or spaces. This chapter makes privacy and safety operational. It describes what we collect, why we collect it, how we protect it, who can access it, and how we respond when something goes wrong. The goal is clear practice, not slogans.

## 1. Policy Summary

- Users own their data.
- Consent is explicit, purpose bound, and revocable.
- Collection is minimal and tied to a clear need.
- Access follows least privilege with auditable paths.
- Sensitive data is encrypted in transit and at rest.
- Public outputs are aggregated and non identifying.
- Incident response is measured in hours, not weeks.
- People can export or delete their personal data unless law requires retention.

## 2. Legal And Ethical Basis

- Consent: opt in for accounts and communications.
- Contract: performing membership and program obligations.
- Legitimate interest: basic analytics and fraud prevention with privacy safeguards.
- Compliance: financial records retention and safety reporting when required.
- Ethics baseline: dignity before efficiency, right to exit, no dark patterns.

This document is not legal advice. We align to common privacy frameworks and safety standards while keeping the design usable.

## 3. Data Taxonomy

### 3.1 Personal Data
- Identification: name, email, country, optional display name.
- Participation: membership status, cell membership, vote signals.
- Communications: messages related to proposals and support.

### 3.2 Sensitive Data
- Health or biometrics: not collected by default. If a program requires it for care or safety, use explicit opt in, narrow scope, retention limits, and encryption.

### 3.3 Operational Data
- Projects: titles, outcomes, milestone records.
- Treasury: amounts, categories, public proofs.
- Incidents: severity, timestamps, anonymized notes.

### 3.4 Derived Or Aggregate Data
- KPI metrics aggregated over windows.
- Pseudonymous activity counts for product decisions.

## 4. Data Map

- Source: join form, account creation, proposal comments, project records, payments.
- Store: Supabase Postgres with RLS. Media in object storage where needed.
- Process: Edge Functions and controlled admin actions.
- Share: public pages with aggregated data and cultural works with creator consent.
- Transfer: only to listed processors with signed agreements.

## 5. Collection By Feature

- Account: email and optional display name. Required for auth.
- Join form: email, path, and bio text to match a Cell. Optional phone only if needed for payment routing in a region.
- Project management: outcomes, milestones, public links. No unnecessary personal fields in tasks.
- Payments: beneficiary data required by processor and law. We do not store full card details.
- Analytics: page views and conversions with privacy first tools and no third party ads cookies.

## 6. Consent Management

- Clear language at join and at any new data use.
- Separate toggles for newsletters and product updates.
- Single click opt out that works.
- Audit trail records what was consented to and when.

## 7. User Rights

- Access: get a copy of personal data.
- Correction: fix mistakes in profiles.
- Portability: export in a common format.
- Deletion: remove personal data unless legal retention rules apply.
- Objection: opt out of specific processing where available.

Requests are acknowledged within 7 days. Fulfillment target is 30 days. Complex requests may take longer with a reasoned note.

## 8. Data Retention Schedule

Keep it short and specific. Numbers are defaults and can be tightened per program.

- Accounts and profiles: active lifetime plus 12 months.
- Join requests: 12 months or on request deletion after matching.
- Projects metadata: 24 months for audit. Public works are archived by consent.
- Treasury records: per jurisdiction requirements. Reference links remain public.
- Incident records: 24 months with anonymization.
- Logs: 30 days for operational use unless a security event requires longer retention.

## 9. Access Control And RLS

Principle is least privilege. Most reads are public or scoped to a Cell. Writes require roles.

### 9.1 Example RLS Policy Fragments

```sql
-- profiles: self read and write
create policy profiles_sel_self on profiles
for select using (user_id = auth.uid());

create policy profiles_upd_self on profiles
for update using (user_id = auth.uid())
with check (user_id = auth.uid());

-- cells: public read, facilitator writes
create policy cells_sel_public on cells
for select using (true);

create policy cells_upd_facilitator on cells
for update using (facilitator_id = auth.uid());
```

### 9.2 Secrets And Roles
- Service role is used only in secure functions and CI, not in client code.
- Anon key is read only and scoped to public operations.
- Admin actions require multi factor auth.

## 10. Encryption

- Transport: TLS for all network traffic.
- Storage: encrypted disks and encrypted columns for any sensitive field.
- Keys: rotated on schedule and on role change. No keys in source control.

## 11. Logging And Monitoring

- Logs avoid personal payloads. Use request IDs and coarse metadata.
- Access logs are retained for 30 days unless an incident is open.
- Security events trigger alerts to the on call rotation.
- Use structured logs for reliable parsing and search.

## 12. Backups And Recovery

- Daily logical and weekly physical backups with integrity checks.
- Restore drills run quarterly.
- Disaster recovery objective: RPO 24 hours, RTO 24 hours for pilot, reduce over time.

## 13. Vendor And Processor Management

- Maintain a public list of subprocessors with purpose and region.
- Due diligence checklist before onboarding a vendor.
- Data processing addendum signed with equivalent safeguards.
- Offboarding includes data export and confirmed deletion when possible.

### 13.1 Due Diligence Checklist Keywords
- Security certifications and posture.
- Data location and transfer safeguards.
- Incident history and response promise.
- Contract terms on deletion and audit.

## 14. International Transfers

- Prefer regional hosting aligned with member base.
- Use standard contractual protections when transfers are required.
- Inform users in the privacy notice and allow opt out when possible.

## 15. Privacy By Design

- Feature intake includes a privacy checklist.
- Data fields require justification and retention plan.
- UI never nudges people into sharing more than needed.
- Public dashboards are aggregated by design.

### 15.1 DPIA Steps
- Describe processing and purpose.
- Assess necessity and proportionality.
- Identify risks to rights and freedoms.
- Define mitigations and residual risk.
- Record sign off by Data Steward and Ethics Council.

## 16. Special Cases

- Children data: we do not knowingly collect data from minors without verified guardian consent where required.
- Health data: only by explicit opt in for a clear safety purpose with strict limits.
- Research: if data is used for research, use anonymization and ethics review.

## 17. Cookies And Analytics

- Essential cookies: auth and session.
- Optional analytics: privacy focused, no cross site tracking, no ads cookies.
- Cookie banner is simple and honest.
- Opt out link is visible and works without tricks.

## 18. Incident Response

We treat incidents as learning events. Speed and clarity matter.

### 18.1 Severity Levels
- Sev 1: active breach or ongoing harm.
- Sev 2: suspected breach with limited scope.
- Sev 3: minor privacy issue without exposure.

### 18.2 Response Steps
- Detect and confirm.
- Contain the issue and isolate systems if needed.
- Notify stakeholders within 24 hours with what we know.
- Eradicate root cause and verify.
- Recover services and monitor.
- Publish an anonymized root cause report and action plan.

### 18.3 Roles
- Incident Lead: coordinates the response.
- Security Officer: technical triage and remediation.
- Data Steward: privacy risk and notification.
- Communications: public notes and user updates.
- Legal liaison: regulator communication where required.

## 19. Governance Interfaces

- Ethics Council can pause risky processing.
- Treasurer ensures that incident costs are recorded and reported.
- Data Steward publishes quarterly privacy reports with metrics and lessons.

## 20. Templates

### 20.1 Privacy Notice Skeleton

```md
We collect the minimum data needed for coordination and safety.
You can export or delete your personal data on request.
We do not sell personal data.
Contact privacy@nuvaar.org for questions or requests.
```

### 20.2 Data Subject Request Acknowledgment

```txt
Subject: We received your request

Hello,
We received your request regarding your personal data. We will respond within 30 days. If we need more time, we will explain why. You can reach us at privacy@nuvaar.org.
Thank you.
```

### 20.3 Incident Public Note

```md
Summary: what happened in one paragraph.
Impact: who was affected and how.
Action: what we did to contain and fix.
Next: what will change to prevent recurrence.
Contact: privacy@nuvaar.org
```

## 21. Metrics

- Time to acknowledge a request.
- Time to fulfill a request.
- Number of incidents per quarter.
- Mean time to detect and to resolve.
- Percentage of features that pass privacy checklist on first review.

## 22. Roadmap

- Automate data export and deletion flows.
- Add per field retention metadata.
- Expand encryption to selected columns with key wrapping.
- Run a third party security review before major releases.

## 23. Versioning

This policy is versioned and archived. Changes include a reason and an effective date.

## 24. Closing Note

Privacy is not a fixed state. It is a daily practice. The easiest way to protect people is to collect less, explain clearly, and keep promises when stress is high.
