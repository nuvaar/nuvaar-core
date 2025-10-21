# NUVAAR Omega Full Launch
# Part 07 - Atlas Cultural Programs

Language is English only. ASCII only. No special dashes or spaces. This chapter defines Atlas as a cultural engine that treats memory as public infrastructure. It includes editorial policy, submission guidelines, translation and accessibility, archiving methods, legal and licensing, partnerships, operations, metrics, and risk controls. The goal is to publish works that uplift dignity and keep them accessible for the long term.

## 1. Mission And Scope

Atlas preserves and circulates cultural works that help people make sense of their lives with care and clarity. It focuses on creators who face structural barriers and on works that are useful for learning and solidarity.

In scope
- Essays, guides, interviews, manifestos, documentary media, community toolkits, open educational resources, and project case studies from the NUVAAR ecosystem.
- Translations and adaptations for wider reach when creators consent.
- Archival records that document governance decisions and public outcomes.

Out of scope
- Content that exploits people or communities.
- Hateful propaganda or harassment.
- Hidden advertising or coercive political messaging.

## 2. Editorial Policy

Principles
- Publish works that add clarity, not noise.
- Explain risk, context, and constraints.
- Credit collaborators and sources.
- Avoid sensational and extractive narratives.

Roles
- Editor in Chief. Sets editorial calendar and standards.
- Section Editors. Oversee themes such as care, craft, and civic practice.
- Copy Editors. Maintain style and clarity.
- Fact Checkers. Verify claims and references.
- Rights And Permissions. Manage licenses and releases.
- Accessibility Lead. Ensures alternate formats and inclusive language.

Conflicts
- Disclose any conflict that may bias selection. A conflicted editor steps back from decisions about a work.

## 3. Submission Guidelines

Eligible submissions
- Original works by NUVAAR members or partners.
- Documentation of NUVAAR projects with creator consent.
- Translations and adaptations with permission from rights holders.

Requirements
- Plain language summary of 120 to 200 words.
- Statement of purpose and audience.
- Sources and references in a simple list.
- License choice that fits NUVAAR policy.
- Accessibility notes: alt text for images, captions for video.

File formats
- Text: Markdown or plain text.
- Images: PNG or JPEG with alt text.
- Audio: WAV or MP3 with transcript.
- Video: MP4 with captions file in VTT.

Quality bar
- Substance: the work teaches or reveals something real.
- Care: no doxxing or humiliation.
- Clarity: explain context and limits.

## 4. Review And Publication Flow

1. Intake. Submission is logged with metadata and a work id.
2. Screening. Quick check for scope and safety.
3. Editorial review. Section editor gives notes within 7 days.
4. Fact check. Claims and stats are verified or marked as opinion.
5. Rights check. Licenses and releases confirmed.
6. Accessibility pass. Alt text, captions, and contrast confirmed.
7. Publication. Work appears with a stable URL and a citation block.
8. Archive. Files and metadata are packaged for preservation and replicated.

Turnaround targets
- Routine works: 14 days from intake to publication.
- Complex works: 30 days with status notes to the author.

## 5. Translation And Adaptation

Goals
- Reach readers who do not share the original language.
- Preserve meaning over literal word choices.

Process
- Translator claim check. Identify domain terms and author intent.
- Parallel draft with notes for ambiguous phrases.
- Review by a second translator or editor for sense and tone.
- Author sign off when possible.
- Credits show translator names and roles.

Rights
- Ensure the original license allows derivative works. If not, obtain permission.
- Mark the translation as an adaptation and link to the source.

## 6. Accessibility

Minimums
- Alt text for all non decorative images.
- Captions for videos and accurate transcripts for audio.
- Clear type, sufficient contrast, and logical heading order.
- Keyboard navigation and focus states on the site.

Preferred
- Easy read versions for key works.
- Audio narration for selected essays.
- Multiple language support where capacity allows.

## 7. Metadata And Citation

Atlas uses a simple but rich metadata set for search and citation.

Core fields
- work_id, title, author_names, summary, keywords[], language, original_language, license, publication_date, version, url, doi_or_handle optional.
- for translations: translator_names, source_work_id.

Context fields
- program_cell_id if related to a NUVAAR cell.
- funding_reference if supported by a grant.
- related_proposals[] for governance traceability.

JSON schema sketch
```json
{
  "work_id": "atlas-2025-0001",
  "title": "Care And Craft In Small Groups",
  "authors": ["A. Author", "B. Collaborator"],
  "summary": "A field guide to running humane small group cycles with real constraints.",
  "keywords": ["care", "craft", "cell", "facilitation"],
  "language": "en",
  "original_language": "en",
  "license": "CC BY NC SA 4.0",
  "publication_date": "2025-10-21",
  "version": "1.0.0",
  "program_cell_id": "cell-123",
  "funding_reference": "proposal-456",
  "related_proposals": ["prop-789"],
  "url": "https://nuvaar.xyz/atlas/care-and-craft",
  "translator_names": []
}
```

## 8. Licensing Policy

Default
- Creative Commons BY NC SA for text and still images unless a different choice better fits author intent.

Options
- CC BY for maximum reuse.
- CC BY SA for copyleft share alike.
- CC0 for public domain where authors want full release.

Rules
- Honor author chosen license if it meets dignity constraints.
- Respect third party content and quotes. Keep quotes short and cite.

## 9. Archiving And Preservation

Strategy
- Keep at least two independent copies in different regions.
- Package each work with metadata, checksums, and a manifest.
- Prefer open formats. Document any proprietary dependencies.

Storage
- Primary: object storage with versioning and lifecycle rules.
- Secondary: IPFS pinning for public access to non sensitive works.
- Offline: periodic snapshots to cold storage for long term safety.

Fixity
- Generate checksums on ingest and verify on schedule.
- Log changes and keep a version history visible to readers.

Example manifest
```json
{
  "work_id": "atlas-2025-0001",
  "files": [
    {"path": "text.md", "sha256": "..." },
    {"path": "poster.jpg", "sha256": "..." },
    {"path": "captions.vtt", "sha256": "..." }
  ],
  "meta": "meta.json",
  "created_at": "2025-10-21T00:00:00Z"
}
```

## 10. Public Access And Search

- Simple search by title, author, keyword, and language.
- Filters for program, license, and format.
- Stable URLs and predictable slugs.
- Sitemap and robots files for discoverability.
- Feeds for new works and for specific tags.

## 11. Community Standards And Moderation

- Code of Conduct applies to comments and discussions.
- Moderation focuses on safety and clarity. No harassment or spam.
- Escalation path: warning, time out, and ban as last resort.
- Appeals are reviewed by an editor not involved in the original action.

## 12. Partnerships

Types
- Universities and libraries for preservation and workshops.
- Cultural centers for exhibitions and talks.
- Media partners for syndication under compatible licenses.

Memorandum of understanding content
- Scope, credit, licensing, data handling, costs, and exit clauses.
- Public summary of the collaboration for transparency.

## 13. Operations And Roles

Daily
- Triage submissions, update status, and answer author questions.
- Publish minor updates and fix broken links.

Weekly
- Editorial meeting to review pipeline and risks.
- Accessibility checks on selected works.
- Outreach to translators and mentors.

Monthly
- Transparency report with counts, timelines, and selected highlights.
- Archive integrity checks and a random quality test.

## 14. Metrics And KPIs

- Submissions received and accepted.
- Median time from intake to publication.
- Number of translations and languages supported.
- Accessibility pass rate.
- Works cited by other media or institutions.
- Uptime and broken link rate.
- Reader signals: time on page, scroll depth, and completion without tracking individuals.

Each KPI lists an owner, a source, a target, and a review cadence.

## 15. Budget And Cost Model

Expected costs per month for an active program
- Editorial staff: 1 to 2 part time editors.
- Accessibility: captioning and transcription services.
- Storage and bandwidth for media.
- Small grants to translators and contributors.
- Events and workshops for outreach.

Funding sources
- Grants and donations with clear terms.
- Revenue from events and publications when aligned with mission.
- Sponsorships that do not force content or compromise dignity.

## 16. Risk Register

- Burnout in editorial team. Mitigation: rotate duties and keep a small steady pace.
- Copyright conflict. Mitigation: clear intake forms, license checks, and takedown process.
- Privacy leak. Mitigation: redact sensitive fields and follow Data Policy.
- Censorship pressure. Mitigation: legal review, multi region hosting, and public statements when safe.
- Link rot. Mitigation: archive primary sources and use checksums.

## 17. Takedown And Corrections

Takedown
- Accept requests with a simple form. Review within 7 days.
- Remove or redact when legitimate rights or safety concerns exist.
- Publish a brief note so readers understand why a link now points to a notice.

Corrections
- Corrections are versioned with a visible note and date.
- Fact changes include a reason and source.
- Style and copy edits do not require a public note unless meaning changed.

## 18. Templates

### 18.1 Submission Front Matter

```md
Title: Care And Craft In Small Groups
Authors: A. Author; B. Collaborator
Summary: A field guide to running humane small group cycles with real constraints.
Keywords: care, craft, cell, facilitation
License: CC BY NC SA 4.0
Language: en
OriginalLanguage: en
ProgramCellID: cell-123
FundingReference: proposal-456
```

### 18.2 Fact Check Log

```txt
Claim: 70 percent retention in 90 days.
Source: program KPI export for period 2025 Q3.
Status: verified on 2025-10-21 by E. Checker.
```

### 18.3 Accessibility Checklist

- Alt text present and descriptive.
- Captions accurate with speakers identified.
- Contrast meets WCAG AA.
- Link text is meaningful out of context.
- Reading level appropriate for audience.

## 19. API Notes

Public JSON endpoints may be provided for simple listings and metadata.
- GET /atlas/api/works
- GET /atlas/api/works/{id}
- GET /atlas/api/tags
- GET /atlas/api/translations?source_id=

Responses include no personal data. Rate limits apply. CORS is restricted to nuvaar domains for admin calls.

## 20. Preservation Plan

Time horizons
- 1 year. Active mirror, monthly fixity checks.
- 3 years. Storage lifecycle review, format migration review.
- 10 years. Re package archives if formats change. Maintain a public roadmap of preservation assumptions and gaps.

Staff duties
- Preservation lead runs quarterly reviews and publishes notes.
- Editor in Chief approves any destructive change to archives.

## 21. Launch Plan

Phase 1
- Publish 10 seed works from NUVAAR programs with full metadata.
- Open submissions to members and partners.
- Run a public reading or online session around the first theme.

Phase 2
- Add translation pipeline for at least 2 languages.
- Partner with one library for a joint exhibit or workshop.
- Publish a first year anthology as a PDF and print on demand.

Phase 3
- Expand to additional regions.
- Launch a fellowship for community editors.
- Build public tools for educators to assemble teaching packs from Atlas works.

## 22. Closing Note

Atlas is a promise to remember well. It makes culture a daily practice by publishing careful works, preserving them with respect, and inviting people to learn, adapt, and build on them without fear.
