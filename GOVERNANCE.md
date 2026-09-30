# Engineering Standards Governance

## Purpose

This handbook is a maintained engineering baseline, not a static document. Rules should be introduced when they solve a recurring engineering problem and can be adopted consistently.

## Standard Lifecycle

### Propose → Review → Adopt → Communicate → Measure → Refine

The standard lifecycle is:

1. **Propose** — create a standards proposal describing the problem, proposed rule, rationale, scope, and adoption impact.
2. **Review** — changes to standards require review by the owners defined in CODEOWNERS. Security-sensitive changes should include the appropriate security owner.
3. **Adopt** — a rule is considered adopted when the relevant documentation is merged and affected teams have been informed.
4. **Communicate** — for material changes, publish a concise migration note in the pull request and relevant team channels.
5. **Measure** — where practical, attach evidence such as incident reduction, review-cycle improvements, defect trends, or developer feedback.
6. **Refine** — remove or revise rules that no longer serve the engineering organization.

## Ownership

- Engineering leadership owns the overall handbook.
- Security owners review security and compliance guidance.
- DevOps owners review automation, CI, and repository governance.

See [CODEOWNERS](.github/CODEOWNERS) for the current review mapping.

## Versioning

The repository version in `package.json` tracks handbook revisions. Material policy changes should be documented in [CHANGELOG.md](CHANGELOG.md).

## Design Principle

**Standards should reduce ambiguity, not create bureaucracy.**
