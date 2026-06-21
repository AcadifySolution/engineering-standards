# Acadify Solution — Engineering Standards & Practices

Welcome to the **Acadify Solution Engineering Standards** repository. This centralized resource defines our internal engineering policies, code quality guidelines, and compliance requirements.

As a distributed team of senior developers building high-reliability AI systems, secure cloud architectures, and scalable SaaS platforms, we hold ourselves to rigorous development standards. Adhering to these guidelines ensures our code is secure, scalable, maintainable, and aligned with industry compliance standards (including HIPAA and SOC2).

---

## 🗺️ Standards Navigation

Our development practices are structured into four main areas:

| Standards Document | Key Topics Covered |
| :--- | :--- |
| 🌿 **[Branching & Git Guidelines](standards/branching-git.md)** | Branching models (Trunk-Based / Git Flow), Branch Protection policies, and Conventional Commits. |
| 🛡️ **[Coding & Security Practices](standards/coding-practices.md)** | AI/LLM safety, PII Masking, HIPAA/SOC2 design rules, SaaS patterns, and static analysis benchmarks. |
| 👥 **[Peer Reviews & PR Guidelines](standards/peer-reviews.md)** | PR criteria, Author self-audits, Reviewer responsibilities, and PR templates. |
| 🚀 **[Release & Versioning](standards/release-management.md)** | Semantic Versioning (SemVer), release checklists, changelog management, and hotfix paths. |

---

## 🛠️ Automated Quality & Tooling

To minimize manual overhead and maintain a consistent baseline, we enforce automatic linting and code styles across all repositories via git hooks and CI checkups.

### Local Environment Setup

When you clone any Acadify repository (including this standards repo), follow these steps to initialize the automated quality tools:

#### Prerequisites

* Node.js (LTS version 20+)
* pnpm / npm / yarn (We recommend `npm` or `pnpm` depending on repository configurations)

#### Step 1: Install Dependencies

This project uses DevDependencies to lint documentation files using `markdownlint-cli` and manage git hooks using `husky`.

```bash
npm install
```

#### Step 2: Enable Git Hooks (Husky)

Husky will automatically configure hook directories based on the `"prepare"` script in `package.json`. If it does not run, you can initialize it manually:

```bash
npx husky
```

### Formatting and Linting Checks

#### Manual Check

You can run the markdown lint checks on demand:

```bash
# Run lint check
npm run lint

# Auto-fix fixable markdown format issues
npm run lint:fix
```

#### Commit-time Hooks

Husky prevents malformed documentation commits by automatically running `markdownlint` before your commit goes through. If linting fails, resolve the errors indicated in the command-line output and re-run your `git commit` command.

#### Continuous Integration (CI)

A GitHub Actions workflow (`.github/workflows/lint.yml`) runs on every pull request targeting `main`. PRs cannot be merged if the linting checks fail.

---

## 🤝 Contribution Guidelines

We treat our standards as living documentation. If you spot a gap, outdated practice, or have an optimization proposal:

1. Create a branch named `refactor/standards-update-<topic>`.
2. Propose the standard updates and verify they comply with the markdown linting rules.
3. Open a Pull Request and assign it to the engineering leads for review.

---

© 2026 Acadify Solution. All rights reserved. Distributed engineering partner.
