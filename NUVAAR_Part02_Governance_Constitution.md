# NUVAAR Omega Full Launch
# Part 02 - Governance Constitution

Language is English only. ASCII only. No special dashes or spaces. This constitution defines how NUVAAR makes decisions, moves funds, resolves disputes, and remains accountable in practice. It is designed for small groups that need clear, humane rules that scale without bureaucracy.

## 1. Purpose And Scope

NUVAAR governance turns administration into care. The purpose is to create predictable, fair, and auditable decision making while preserving dignity and agency for all members. This document applies to all Cells, programs, committees, and shared infrastructure owned or operated by NUVAAR.

Scope includes roles, elections, proposals, voting, treasury, transparency, conflict resolution, data handling in governance contexts, risk controls, and amendment procedures.

## 2. Core Principles

1. Dignity before efficiency. No outcome is worth degrading people.
2. One clear source of truth. Decisions, votes, and treasury actions are recorded and linkable.
3. Least power needed. Grant the minimum authority required to act, and audit it.
4. Separation of duties. Proposal, review, and execution are distinct responsibilities.
5. Open records by default. Sensitive data is minimized and protected, but reasoning and results are public.
6. Human veto on irreversible outcomes. The Ethics Council can pause or revert actions that would cause harm.

## 3. Roles And Responsibilities

Every role has a clear mandate, minimum competencies, and a handover path.

- Founder. Direction, partner relations, constitutional stewardship. Duties include maintaining alignment with mission and approving the governance calendar. May not unilaterally spend treasury funds.
- Member. Participates in Cells and governance. Rights include proposing items, voting, and requesting records. Duties include following the Code of Conduct and Data Policy.
- Facilitator. Ensures inclusive process and psychological safety. Runs retrospectives and conflict de escalation steps. Cannot approve payments alone.
- Treasurer. Operates the Safe multisig. Prepares transaction bundles, maintains spend categories, and publishes monthly reports. Must pass background checks appropriate to jurisdiction.
- Ethics Council. Independent review and veto for dignity violations or material risk. Can pause execution for up to 7 days while the DAO votes.
- Data Steward. Oversees privacy, data access, and incident response for governance data. Maintains redaction guidelines.
- Security Officer. Coordinates incident response for systems, including keys and supply chain risks. Works with Data Steward for coordinated disclosures.
- Election Officer. Runs member and council elections, verifies eligibility, and publishes results.

Role overlap is allowed in small pilots but must maintain separation of duties in each decision flow. Example: a Treasurer cannot serve as the sole reviewer of a payment that they initiated.

## 4. Membership

- Eligibility. Any person who accepts the Code of Conduct, the Data Policy, and the Dignity Protocol can apply.
- Admission. Join requests are reviewed for basic fit and safety. Rejections include a reason and a path to reapply.
- Status. Members are active if they have participated in a vote or a Cell activity in the last 60 days.
- Removal. Pattern of harmful behavior, fraud, or repeated policy violations may result in removal after due process.
- Appeals. Members may appeal removal 30 days after decision with new facts.

## 5. Conflict Of Interest Policy

- Members must disclose material conflicts before proposing or voting.
- A conflicted member should abstain in treasury matters. The abstention is recorded.
- Gifts or compensation above a set limit must be reported in the monthly transparency report.
- Violations of disclosure obligations are subject to sanctions.

## 6. Proposal Lifecycle

All governance items follow a common flow. The steps are designed for asynchronous collaboration.

1. Draft. A member posts a proposal that includes problem, options considered, preferred option, budget, risks, KPIs, and timeline.
2. Review. The Ethics Council and Data Steward review for dignity and privacy. Comments are public and time boxed.
3. Signaling Vote. Snapshot vote records support, quorum, and any reputation signals used for guidance.
4. Execution Plan. The Treasurer prepares a Safe transaction bundle if funds move. The plan includes controls and milestones.
5. Execution. Signers meet threshold and execute. If non financial, the responsible role documents the action taken.
6. Report. A public report is posted with outcomes, links to deliverables, funds used, lessons, and next steps.
7. Archive. Materials are versioned and stored in the Atlas archive for long term accountability.

## 7. Decision Classes And Thresholds

Decisions are grouped by risk level. Quorums and thresholds are tuned to minimize both capture and deadlock.

- Class A Routine. Text updates, page copies, and small ops not touching funds. Quorum 30 percent of active members. Simple majority.
- Class B Program. Program rules, Cell formation, partner MoUs, minor grants. Quorum 50 percent. Simple majority or ranked choice if more than two options.
- Class C Treasury. Grants, payments, or contracts above the minor threshold. Quorum 60 percent. Quadratic voting for signal. Final execution by Safe threshold.
- Class D Emergency. Security or safety incidents requiring fast action. Ethics Council can pause for up to 7 days. A special vote decides continuation.

Thresholds are reviewed quarterly. Safe thresholds start at 2 of 3 in pilot and grow to 3 of 5 or 4 of 7 with scale.

## 8. Voting Methods

- One person one vote. Default for routine items.
- Ranked choice. Used when more than two options exist and a clear majority is needed.
- Quadratic voting. Used for treasury signals to reduce dominance by large holders or social clusters. Reputation signals are advisory and must be published with criteria.
- Abstain and no confidence. Always allowed and recorded.
- Delegation. Members may delegate their vote to a trusted proxy for a term not longer than 90 days. Delegations are public and revocable.

## 9. Elections

- Terms. 6 months for council roles, renewable once before a cooling period of 6 months.
- Eligibility. Active members with clean conduct record in the last 90 days.
- Process. Nomination, Q and A, Snapshot vote with ranked choice, and public results.
- Removal. A recall vote may remove a role holder with a two thirds vote if clear misconduct or incapacity is shown.

## 10. Treasury Governance

NUVAAR uses a Gnosis Safe multisig backed by on chain policies and off chain controls.

- Categories. Micro grants, facilitation, infrastructure, compliance, reserve, and experiments.
- Limits. Per payment limit, daily limit, and category monthly cap.
- Reviewers. Any payment above the minor threshold requires two reviewers plus Treasurer signature.
- Documentation. Each payment links to the proposal ID, milestone, and deliverable.
- Reports. Monthly reports include starting balance, income, expenses by category, outstanding commitments, and runway.
- Reserves. Maintain a minimum reserve equal to 3 months of operating costs whenever possible.

Safe configuration is published, including owner addresses, threshold, and policies. Keys are rotated on role changes.

## 11. Transparency And Records

- All proposals, votes, and reports are public links with stable IDs.
- Meeting notes and rationales are published within 7 days.
- Redactions are limited to sensitive personal data or security details.
- A public changelog records policy changes with effective dates.

## 12. Data Handling In Governance

- Governance data includes proposals, votes, comments, and contact information for notifications.
- Default is open records with privacy by design. Minimize personal fields. Use aliases where lawful.
- RLS controls access in the database. Only the Data Steward and service roles can access raw email fields when necessary for eligibility checks.
- Data retention for governance records is at least 24 months. Personal contact fields may be deleted on request after legal checks.

## 13. Conflict Resolution

NUVAAR prefers restorative methods that address harm without humiliation.

1. Facilitation. Clarify goals, constraints, and misunderstandings. Document the narrative and options.
2. Mediation. Neutral facilitator proposes a compromise plan with time boxed trial.
3. Council Review. Ethics Council issues a reasoned finding and recommendations.
4. Vote. The DAO chooses an action if the parties do not agree.
5. Sanctions. Warning, temporary suspension, removal from roles, or membership removal by vote.

Right of reply and appeal windows are respected at each step.

## 14. Code Of Conduct Enforcement

- Prohibited behavior includes harassment, hate speech, stalking, discrimination, and persistent disruption.
- Reports can be filed confidentially. Anonymous reporting is allowed where safe.
- The Enforcement Team investigates promptly and recommends actions. Transparency reports summarize cases in aggregate without naming victims.

## 15. Emergency Procedures

- Break glass. Ethics Council can pause execution for up to 7 days in case of credible harm or security risk.
- Special vote. A special vote is called to extend a pause or approve an emergency action.
- Communication. A public note states the reason for pause and the next steps without exposing sensitive details.

## 16. Risk Management

- Risk register. Each program maintains a list of risks with likelihood, impact, owner, and mitigation.
- Controls. Separation of duties, spend limits, and audits.
- Testing. Run tabletop exercises for incident response and treasury key loss.
- Dependencies. Track third party services and licenses. Define fallback plans.

## 17. Audits And Reviews

- Internal review. Quarterly governance and treasury reviews with action items.
- External audit. Annual financial or process audit by an independent party when budget allows.
- Public feedback. Open comment windows on major policy changes.

## 18. Metrics For Governance Health

- Participation rate in votes and proposals.
- Time to decision and time to payout.
- Incident count and time to resolution.
- Number of conflicts resolved without sanctions.
- Budget variance from plan.

Targets are published each quarter and reviewed in retrospectives.

## 19. Legal And Compliance Notes

- NUVAAR is not a security, investment fund, or financial advisor. It is a civic and cultural coordination project.
- Treasury operations comply with relevant laws in operating jurisdictions. KYC or vendor checks are performed where required by regulation or payment processor policies.
- Nothing in this document is legal advice. Members should consult counsel for personal risks or obligations.

## 20. Amendments

- Amendments require a two thirds quorum and a simple majority in favor after a public discussion of at least 10 days.
- Emergency amendments may be adopted with a special vote when a credible harm exists, but they must be re approved in the next cycle or they expire.
- All amendments are versioned with reason and effective date.

## 21. Implementation Guidance

- Snapshot. Create space, set voting strategies, quorum rules, and delegation settings. Publish a how to vote guide.
- Safe. Create the multisig, set owners, threshold, and spending policies. Publish addresses. Test small transactions before large ones.
- Records. Use stable IDs across proposals, votes, and payments. Link everything in reports.
- Training. Provide role cards for Treasurer, Facilitator, Data Steward, and Council members. Include ethics and privacy refreshers.

## 22. Templates

- Proposal Template. Problem, options, preferred option, budget, risks, KPIs, timeline, and success criteria.
- Payment Request Template. Proposal ID, milestone, amount, beneficiary, reviewer names, and links to deliverables.
- Conflict Report Template. Event summary, harm statement, desired outcome, and suggested steps.
- Transparency Report Template. Period covered, treasury summary, decisions, incidents, and pending items.

## 23. Exit And Handover

- Members may leave at any time with access to their data export.
- Roles must hand over credentials and documents within 7 days.
- Treasurers must transfer Safe keys on role change and publish a handover checklist.

## 24. Effective Date And Review

This constitution is effective at launch. It will be reviewed 60 days after launch and then quarterly. Revisions are archived with change notes.

## 25. Glossary

- Snapshot. Off chain voting platform with cryptographic signatures.
- Safe. Gnosis Safe multisig for treasury operations.
- Quadratic voting. A method that reduces influence concentration by increasing cost of additional votes.
- Reputation signals. Non transferable, documented criteria that provide advisory weight but not direct control.
- Restorative process. A process that aims to repair harm and restore trust without humiliation.
- Separation of duties. No single person controls draft, review, and execution for the same decision.

## 26. Closing Note

Good governance is patient, clear, and brave. It chooses care over theater and accountability over shortcuts. With this constitution, NUVAAR commits to building systems that people can trust when it matters most.
