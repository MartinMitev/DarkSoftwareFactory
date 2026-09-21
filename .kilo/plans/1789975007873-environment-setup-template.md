# Plan: Code Review Template

## Goal

Create a new document template `templates/development/code-review.md` (Markdown) that defines the structure and expected content of a Code Review document for a software project.

## Target File

- `templates/development/code-review.md` (the directory already exists from the Environment Setup template)

## Key Design Decision

The document is designed as a **per-change review record** (one document per PR/change under review), not a generic review policy:

- Matches the `skills/development/code-review-and-quality/SKILL.md` checklist format ("Review: [PR/Change title]").
- Makes findings traceable to a specific change, which is the natural reading of "Code Review document".
- Section 4 and the Appendix double as the reusable five-axis checklist.

## Context and Conventions

Repo template format (from `templates/testing/test-concept.md`, `templates/testing/project-risk-profile.md`, `templates/development/environment-setup.md`):

1. `# Title` + blockquote header: **Template Version / Last Updated / Document Status**
2. `## Metadata` table (project name, roles, classification, related documents)
3. `## Table of Contents` with anchor links
4. Numbered `## N. Section` headings; each section opens with an HTML comment block with `Expected content:` bullets
5. Placeholder tables with `<!-- comment -->` cells and inventory IDs (e.g., FIND-XXX, CR-XXX)
6. `## Document History` at the end

Terminology alignment with `skills/development/code-review-and-quality/SKILL.md`:

- Five review axes: **Correctness, Readability & Simplicity, Architecture, Security, Performance**
- Finding severity prefixes: *(no prefix)* required, **Critical:** blocks merge, **Nit:** optional, **Optional:/Consider:**, **FYI**
- Approval standard: approve when the change definitely improves overall code health
- Change sizing: ~100 / ~300 / ~1000 lines guidance; splitting strategies
- Verification story: tests run, build, manual verification, UI evidence
- Disagreement resolution hierarchy: technical facts > style guides > design principles > codebase consistency
- No "I'll clean it up later": deferrals require follow-up items with self-assignment
- Dependency review and dead code hygiene
- Review speed: respond within one business day

## Document Structure (what the generated template will contain)

1. **Executive Summary** — 2-4 bullets: change under review, review outcome, blocking findings, verification summary
2. **Purpose, Scope, and Definitions** — why this record exists, in/out of scope, definitions (Change, Review Axis, Finding, Severity Label, Verification Story, Review Round)
3. **Change Context** — the change under review:
   - Review identification table (review ID CR-XXX, PR/change ID, repo, branch, review date(s))
   - Change description (first line + body: what and why, per skill "Change Descriptions")
   - Change size (~lines, files, whether it fits sizing targets, split decision)
   - Spec / task / bug links and related documents
   - Author(s), reviewer(s) (incl. AI/model-assisted review note per Multi-Model pattern)
   - Review round log (round, date, reviewer, verdict, findings added)
4. **Review Criteria (Five-Axis Checklist)** — per axis (correctness, readability & simplicity, architecture, security, performance):
   - Checklist table (criterion, met?, notes) mirroring the skill's checklist
   - Guidance comments with the axis-specific review questions from the skill
   - Additional subsections: dependency review (new dependency checks) and dead code hygiene (identified dead code inventory)
5. **Review Findings** — findings inventory:
   - Findings table: FIND-XXX, severity label, axis, location (file/line), description, author action, status
   - Finding detail template (per finding: ID, severity, axis, location, description, evidence, required action, disposition)
   - Guidance: every comment must carry a severity label; quantify problems when possible
6. **Verification Story** — what the author verified: tests run, build result, manual verification, UI evidence (screenshots), before/after comparison, reviewer-verified checks
7. **Review Outcome and Decisions** — verdict (✅ Approve / ❌ Request Changes / 🔴 Block), per-axis summary, blocking findings list, deferral items (each deferred issue requires justification + follow-up item with self-assignment), disagreement notes (resolution hierarchy applied)
8. **Follow-up Management** — follow-up item inventory: FU-XXX, origin (deferral/deferral note), description, self-assigned to, due reference, status; deferral tracking rules
9. **Appendices** —
   - Appendix A: Five-Axis Review Checklist (reusable blank checklist)
   - Appendix B: Finding Severity Reference (label table from the skill)
   - Appendix C: Disagreement Resolution Reference (hierarchy from the skill)
10. **Document History**

Every `## N.` section carries a guidance comment block with expected content; all table cells use `<!-- comment -->` placeholders.

## Implementation Steps

1. Write `templates/development/code-review.md` with the full structure above:
   - Blockquote header: Template Version 1.0, Last Updated `<!-- date -->`, Document Status `<!-- Draft | Under Review | Approved | Baselined -->`
   - Metadata table (project name, system/application, project type, roles incl. reviewers, classification, related documents: SRS / architecture / test concept / environment setup)
   - TOC with anchors matching the numbered sections
   - Sections 1-9 as detailed above with guidance comments and placeholder tables
   - Document History table
2. Do NOT modify other files (README template list update is out of scope unless explicitly requested)

## Validation

- Markdown TOC anchors resolve to headings (slug check via script)
- Structure/style consistency against `templates/development/environment-setup.md` and `templates/testing/test-concept.md` (header format, metadata fields, comment style, Document History)
- Terminology alignment check against `skills/development/code-review-and-quality/SKILL.md` (five axes, severity labels, approval standard, deferral rules)

## Open Questions

None material. Recommended defaults:
- File name: `code-review.md` (kebab-case, matches repo convention)
- Document title: "Code Review Document"
- Template version: 1.0
- Design: per-change review record (decision above)
