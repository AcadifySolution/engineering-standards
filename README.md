# Acadify Solution — Engineering Standards & Practices

This repository serves as the definitive reference for engineering standards, development workflows, and compliance baselines at Acadify Solution.

As a distributed team of senior developers building high-reliability AI products, scalable SaaS platforms, and secure cloud infrastructure, we hold our codebases to rigorous production-grade standards. Consistent execution of these practices ensures security, maintainability, and alignment with critical HIPAA and SOC2 compliance targets.

---

## 🗺️ Standards Navigation

Our core engineering guidelines are divided into four primary domains:

| Standard Guide                                                      | Core Subjects                                                                 |
| :------------------------------------------------------------------ | :---------------------------------------------------------------------------- |
| 🌿 **[Branching & Git Guidelines](standards/branching-git.md)**     | Branching topologies, PR size constraints, and Conventional Commits.          |
| 🛡️ **[Coding & Security Practices](standards/coding-practices.md)** | PII masking filters, HIPAA/SOC2 design rules, and framework architectures.    |
| 👥 **[Peer Reviews & PR Guidelines](standards/peer-reviews.md)**    | Self-review benchmarks, reviewer responsibilities, and PR templates.          |
| 🚀 **[Release & Versioning](standards/release-management.md)**      | SemVer 2.0.0 compliance, deployment vs. release separation, and hotfix paths. |

---

## 🛠️ Onboarding & Local Setup

Every repository at Acadify Solution enforces formatting and linting rules locally using Git hooks and in CI workflows using GitHub Actions.

### Development Environment Setup

To configure your local environment for automated style enforcement:

#### 1. Prerequisites

Ensure you have the following installed on your development machine:

- Node.js (LTS v20+)
- npm (pre-packaged with Node.js) or `pnpm`

#### 2. Install Development Dependencies

Clone this repository and install the development packages (Prettier for formatting, Markdownlint for structure checking, and Husky for hook automation):

```bash
npm install
```

#### 3. IDE Integration (Recommended)

This repository contains a `.editorconfig` file that automatically configures text formatting rules (spaces vs. tabs, indentation depth, line endings) for your editor. We recommend installing the corresponding plugin if your IDE does not support EditorConfig natively:

- **VS Code:** Install the `EditorConfig for VS Code` and `Prettier - Code formatter` extensions.
- **JetBrains (IntelliJ/WebStorm):** EditorConfig support is enabled out-of-the-box.

---

## 🤖 Validation Pipelines

We run three validation layers to prevent formatting discrepancies or broken documentation structures from entering production:

### 1. Editor Formatting

Rules configured in `.editorconfig` and `.prettierrc` format your files automatically on save.

### 2. Pre-Commit Verification (Husky)

A local pre-commit hook runs `npm run lint` on staged files before allowing commits:

```bash
# Run syntax and formatting verification manually
npm run lint

# Auto-correct formatting and fixable markdown structure issues
npm run lint:fix
```

### 3. Continuous Integration (GitHub Actions)

The workflow in `.github/workflows/lint.yml` executes formatting and syntax checks on all pull requests targeting the `main` branch. PR merges are blocked until all checks pass.

---

## 📝 Amending the Standards

We maintain our standards as living documentation. To propose updates or refinements:

1. Review the [Security Policy](SECURITY.md) to ensure no internal security procedures are leaked.
2. Open an issue using the [Standards Amendment Template](.github/ISSUE_TEMPLATE/standards_proposal.md).
3. Following consensus, create a branch named `refactor/standards-update-<topic>` and submit a Pull Request.

---

© 2026 Acadify Solution. All rights reserved. Globally distributed team.
