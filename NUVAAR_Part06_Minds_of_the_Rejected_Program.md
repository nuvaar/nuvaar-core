# NUVAAR Omega Full Launch
# Part 06 - Minds Of The Rejected Program

Language is English only. ASCII only. No special dashes or special spaces. This chapter is the operational handbook for Minds Of The Rejected. It covers goals, scope, roles, eligibility, onboarding, matching, funding, delivery, safety, privacy, conflict resolution, metrics, and graduation. It is designed so that a motivated team can run a pilot in a new city with minimal extra guidance.

## 1. Program Charter

Purpose
- Enable excluded or sidelined creators to produce public work and durable income with dignity.
- Provide small group structure, clear milestones, and transparent micro funding.
- Build confidence and networks through practice, not speeches.

Scope
- Cells of 3 to 12 members who commit to a 6 to 12 week cycle.
- Public outcomes that respect privacy and consent.
- Micro grants tied to real deliverables and learning.

Non goals
- Not therapy or clinical services. We provide care in the sense of respect and structure, not medical support.
- Not a speculative token scheme.
- Not a gig market with race to the bottom prices.

## 2. Roles And Responsibilities

Core roles
- Maker. Produces work, documents progress, and participates in reviews.
- Facilitator. Guides process, protects psychological safety, and runs rituals.
- Observer. Supports research and documentation. May become a maker in next cycles.
- Mentor. Provides feedback and targeted knowledge. Time bound engagement.
- Treasurer. Executes approved disbursements from Safe and keeps reports current.
- Data Steward. Guards privacy in forms, dashboards, and archives.

Role cards
- Each role has a one page card that lists mandate, must do items, must not do items, common risks, and handover steps.

Separation of duties
- No person should both request funds and be the sole reviewer of that request.
- Facilitators cannot unilaterally deny a payout that passes a published quality gate.

## 3. Eligibility And Inclusion

Eligibility
- Individuals 16 years or older who accept the Code of Conduct, Data Policy, and Dignity Protocol.
- Priority for people who face structural barriers: neurodivergent creators, women, migrants, disabled creators, and independent artists without access to fair funding.

Access supports
- Asynchronous friendly communications.
- Written briefs with reading time.
- Flexible hours and low noise check ins.
- Clear opt outs without penalty beyond loss of specific funding.

Exclusions
- Hate speech, harassment, fraud, or clear bad faith.
- Conflicts of interest not disclosed after request.
- Repeated non delivery without communication.

## 4. Onboarding Flow

Steps
1. Join form is submitted. Fields are minimal: email, path, bio, time constraints, and needs.
2. Screening call or chat. Confirm goals and constraints. Provide a simple explainer of the program.
3. Consent and data brief. Right to exit and export is stated clearly.
4. Matching. Candidate is placed in a Cell based on goals, skills, and time zone.
5. Kickoff. Facilitator runs the initial ritual and defines the first milestone.

Artifacts
- Join intake notes with explicit consent flags.
- Role cards.
- Cell charter and conflict norms.
- Safety contacts and escalation matrix.

## 5. Matching Algorithm

Goals
- Keep noise low and fit high. Maximize working overlap in time and intent.

Inputs
- Skills and interests.
- Time zone and availability.
- Desired outcomes and constraints.
- Access needs.

Heuristic pseudocode
```
score = 0
if timezone_overlap >= 2 hours: score += 3
if complementary_skills: score += 3
if shared_outcome_theme: score += 2
if access_needs_met_by_cell: score += 2
if language_compatibility: score += 1
```

Thresholds
- Cells form when total score across pairs passes a target value.
- Facilitator can override with a reason. Overrides are logged for learning.

## 6. Cell Lifecycle

Cadence
- Weekly check in 45 minutes.
- Midweek async update thread.
- End of cycle demo for public outcomes.

Rituals
- Kickoff. Why me, why now, what is the smallest outcome that matters.
- Midpoint reset. What is blocked, what can be cut, what stays.
- Demo. Show work, discuss lessons, publish links.

Exit
- A member may leave with no stigma. If funds were disbursed, deliverables due to date must be posted or a refund plan is negotiated.

## 7. Funding And Payouts

Grant envelopes
- Seed. 100 to 1000 USD equivalent per member for first cycle.
- Scale. 1000 to 3000 USD per Cell for group needs.
- Support. Micro budget for accessibility or equipment needs when justified.

Stage gates
- Gate 1 plan. Proposal and scope with risks. 20 percent.
- Gate 2 first milestone. Visible progress with partial outcome. 30 percent.
- Gate 3 final outcome. Public deliverable plus documentation. 50 percent.

Rules
- Payments reference proposal id and milestone id.
- Disputes use the quality rubric and facilitator notes.
- Emergency advances are possible for access or safety, with receipts.

Receipts
- Accept screenshots of digital costs and simple photos for physical items.
- No demand for private information beyond what the payment processor needs.

## 8. Deliverables And Quality Rubric

Definition of done
- The work exists, is accessible to the audience, and has a short written context.
- Assets are licensed in a way that respects creators and community.

Rubric categories
- Clarity. Goal and audience are clear.
- Value. Outcome is useful or moving for its intended audience.
- Craft. The work is coherent and avoids avoidable defects.
- Learning. The team documents what changed and why.
- Care. The process respected consent, safety, and inclusion.

Scoring
- 1 weak, 2 partial, 3 meets, 4 strong.
- A payout passes when average is at least 2.5 and Care is at least 3.

## 9. Facilitation Manual

Weekly check in outline
- Open with one sentence wins.
- Review board columns: now, next, blocked.
- Ask for the smallest next step that creates real momentum.
- Name risks and request help early.
- End with a round of thanks and a time box for async follow ups.

Common anti patterns
- Silence that hides confusion. Use prompts and examples.
- Overscoped plans. Cut scope to preserve dignity and completion.
- Hidden conflicts. Name the tension kindly and focus on constraints.

Tools
- Low noise kanban board.
- Shared notes document.
- Timer in calls to keep turns fair.
- Optional voice to text summaries with consent.

## 10. Safety, Safeguarding, And Boundaries

- This program is not therapy. If someone needs clinical help we provide a resource list and pause involvement if safety is at risk.
- No doxxing or public shaming. Disagreements are handled in process.
- Physical events require a basic safety check: accessible venue, clear exits, and a way to contact organizers.
- Report channels are visible in every Cell charter.

Incident severity
- Sev 1 active harm. Pause work and contact local help where lawful.
- Sev 2 serious conflict. Move to mediation and pause payouts.
- Sev 3 policy breach without harm. Log, coach, and monitor.

## 11. Privacy And Data Minimization

- Collect only what is needed to match, pay, and publish deliverables.
- Use RLS to scope views to the member and their Cell.
- Aggregated dashboards for public transparency.
- Private notes are redacted before archiving or sharing.

## 12. Documentation And Templates

Templates
- Proposal. problem, outcome, budget, risks, kpis, timeline.
- Milestone report. what changed, links, blockers, next steps.
- Demo day sheet. title, 3 line context, link, license.
- Incident form. event, severity, action, next step.
- Accessibility checklist. font size, contrast, alt text, captions.

JSON skeletons
```json
{
  "proposal": {"id": "", "cell_id": "", "title": "", "outcome": "", "budget_usd": 0, "milestones": [], "risks": [], "kpis": []},
  "milestone": {"proposal_id": "", "n": 1, "summary": "", "links": [], "evidence": [], "score": 0},
  "incident": {"cell_id": "", "severity": "sev2", "note": "", "created_at": ""}
}
```

## 13. Communication Guidelines

- Write in plain language.
- Prefer short paragraphs and bullet points.
- Avoid sarcasm and in jokes that exclude newcomers.
- Use content warnings when needed for art that could disturb.
- Credit collaborators clearly.

## 14. Program KPIs

- Active cells.
- Completed projects per cycle.
- Payout speed from gate approval.
- Retention across cycles.
- Quality rubric averages over time.
- Number of public works published in the Atlas.

Data hygiene
- Each KPI has an owner, a source, and a review cadence.
- Dashboards show trends and confidence, not only point values.

## 15. Conflict Resolution

Ladder
1. Self check. Name the need and constraint.
2. Peer dialogue. 2 person chat with notes.
3. Facilitated session. Neutral guide writes a plan.
4. Council review. Recommendation is posted.
5. Vote. DAO chooses if needed.

Sanctions
- Warning with a concrete behavior change request.
- Time boxed suspension with a re entry plan.
- Removal by vote in serious or repeated cases.

## 16. Alumni And Marketplace

- Graduates join an alumni directory with skill tags and contact preferences.
- Alumni can mentor new Cells for a stipend.
- A simple marketplace lists services and public works by members who opt in.

## 17. Budgeting And Costs

Typical monthly ranges for a pilot with 2 Cells
- Micro grants 1500 to 2500 USD.
- Facilitation 800 to 1500 USD.
- Infra and tools 300 to 500 USD.
- Training and accessibility 200 to 400 USD.

Publish a transparency report each month with spend by category and links to proposals.

## 18. Risk Register

Examples
- Funding volatility. Mitigation: keep a 3 month reserve when possible.
- Facilitator burnout. Mitigation: rotate and cap session loads.
- Privacy leak. Mitigation: minimal logs and E2EE for sensitive notes.
- Partner capture. Mitigation: publish conflicts and diversify partners.

## 19. Launch Playbook For A New City

Week 1
- Recruit a facilitator and a treasurer. Run safety orientation.
- Open join form. Promote through community partners.
- Shortlist 12 to 24 candidates.

Week 2
- Screening and matching. Form 2 Cells.
- Kickoff rituals and set Gate 1 deliverables.
- Create a public page that explains scope and safety.

Weeks 3 to 5
- Weekly check ins and midweek async prompts.
- Gate 2 reviews and partial disbursements.

Week 6
- Demo day. Publish outcomes. Pay final disbursements.
- Retrospective. Update playbook and share public notes.

## 20. Quality Assurance Checks

Before Gate 1 payout
- Proposal exists and links resolve.
- Risks are named with at least one mitigation.
- Budget lines add up and are realistic.

Before Gate 2 payout
- Evidence of real progress.
- Scope cut decisions are explicit and documented.
- No open safety concerns.

Before final payout
- Public links and licenses present.
- Learning section updated.
- Facilitator confirms dignity protocol held during the cycle.

## 21. Graduation Paths

- Continue in a new Cell with a new role.
- Join the mentor pool.
- Apply for a larger grant with a partner org.
- Publish a case study in the Atlas.

## 22. Endnotes

This program assumes that people do their best when given respect, clarity, and a small budget with honest constraints. The point is not to win a game. The point is to build a life where work and dignity reinforce each other.
