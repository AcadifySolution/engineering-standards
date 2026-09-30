# Acadify Solution — Engineering Standards

> A practical, versioned engineering handbook for building secure, maintainable, production-ready software at Acadify Solution.

[![Quality Checks](https://github.com/AcadifySolution/engineering-standards/actions/workflows/lint.yml/badge.svg)](https://github.com/AcadifySolution/engineering-standards/actions/workflows/lint.yml)
[![Handbook](https://img.shields.io/badge/handbook-living-0f172a.svg)](standards/)
[![Node](https://img.shields.io/badge/node-%3E%3D20-339933.svg)](package.json)

This repository is the shared engineering baseline for Acadify Solution. It turns engineering expectations into explicit, reviewable practices covering Git, coding, security, peer review, releases, and operational quality.

**The goal is simple: make good engineering the default.**

## At a Glance

| Area | Standard | Primary Outcome |
| --- | --- | --- |
| 🌿 Git & Branching | [Branching & Git](standards/branching-git.md) | Predictable collaboration and clean history |
| 🛡️ Code & Security | [Coding Practices](standards/coding-practices.md) | Secure, maintainable implementation |
| 👥 Reviews | [Peer Reviews](standards/peer-reviews.md) | Consistent PR quality and shared ownership |
| 🚀 Releases | [Release Management](standards/release-management.md) | Safer, repeatable releases and hotfixes |

## Engineering Principles

- **Clarity over cleverness** — code and decisions should be easy to understand.
- **Security by default** — least privilege and safe data handling are baseline requirements.
- **Automation over memory** — CI, hooks, templates, and checklists enforce repeatable quality.
- **Small, reversible changes** — short-lived branches and focused PRs reduce risk.
- **Evidence over assumptions** — important decisions should be supported by tests, telemetry, or documented rationale.
- **Production ownership** — shipping includes monitoring, rollback readiness, and post-release verification.

## How to Use This Repository

### Engineers

Start with the four standards above, then run:

```bash
npm install
npm run lint
```

### Reviewers

Use the [Pull Request template](.github/pull_request_template.md) to check implementation quality, testing, security considerations, and release readiness.

### Maintainers

Use [GOVERNANCE.md](GOVERNANCE.md) and [CONTRIBUTING.md](CONTRIBUTING.md) to evolve the handbook without unnecessary process.

## Repository Structure

```text
.
├── .github/
│   ├── ISSUE_TEMPLATE/
│   ├── CODEOWNERS
│   ├── pull_request_template.md
│   └── workflows/
├── .husky/
├── standards/
│   ├── branching-git.md
│   ├── coding-practices.md
│   ├── peer-reviews.md
│   └── release-management.md
├── SECURITY.md
├── GOVERNANCE.md
├── CONTRIBUTING.md
├── CHANGELOG.md
├── package.json
└── README.md
```

## Quality Gates

**Editor → Pre-commit → CI → Human Review → Release Verification**

EditorConfig and Prettier keep formatting consistent. Husky validates local changes. GitHub Actions validates pull requests. CODEOWNERS defines review ownership. Templates capture evidence and migration impact.

## Contributing

For meaningful changes, open a standards proposal, explain the problem and rationale, update the relevant documentation, run `npm run lint`, and submit a focused PR.

See [CONTRIBUTING.md](CONTRIBUTING.md) for the full workflow.

## Security

Security issues must **not** be reported through public issues. See [SECURITY.md](SECURITY.md) for the reporting process.

## Status

This is a **living engineering standard**. Rules may evolve as the organization's architecture, product scope, and operational requirements change.

**Current handbook version:** 1.1.0  
**Last reviewed:** 2026-09-30

© 2026 Acadify Solution
