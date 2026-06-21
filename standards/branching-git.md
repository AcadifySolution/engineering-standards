# Git Branching & Commit Guidelines

To maintain continuous integration, clean release lineages, and simple rollbacks, all Acadify Solution projects follow a disciplined Git workflow.

---

## 🌿 Branching Model: Trunk-Based Development

We use a **Trunk-Based Development** branching strategy. Developers commit to short-lived feature branches, verify them, and merge them into `main` frequently.

### Branch Categories and Naming Conventions

All branch names must be lowercase, hyphen-delimited, and prefixed with a standardized type:

| Branch Prefix | Purpose | Example |
| :--- | :--- | :--- |
| `feat/` | A new feature or capability | `feat/llm-pii-masking` |
| `fix/` | A bug fix | `fix/oauth-refresh-token` |
| `refactor/` | Code refactoring without behavioral changes | `refactor/fastapi-routes` |
| `perf/` | Performance optimization | `perf/vector-query-indexing` |
| `docs/` | Documentation changes only | `docs/api-specs` |
| `chore/` | Maintenance tasks, dependency bumps | `chore/upgrade-playwright` |
| `ci/` | GitHub Actions or DevOps tooling changes | `ci/configure-lint-workflow` |
| `test/` | Adding or updating tests | `test/auth-integration` |

### Branch Lifecycle Guidelines

1. **Short Lifespan:** Keep branch lifetimes under 3 days. Large features should be broken down into smaller, self-contained sub-features controlled by feature flags.
2. **Synchronize Daily:** Rebase or merge `main` into your feature branch daily to prevent merge conflicts.
3. **Clean Up:** Automatically delete feature branches after they are merged to keep the remote repository clean.

---

## 🛡️ Branch Protection Rules

Our repositories enforce branch protection on the `main` branch to guarantee high stability:

1. **No Direct Commits:** All modifications must be submitted via a Pull Request. Direct pushes to `main` are blocked.
2. **Required Code Reviews:** At least **one (1) senior engineer approval** is required before a PR can be merged. Two (2) approvals are recommended for updates touching critical AI orchestration layers, HIPAA-compliant databases, or root Cloud Infrastructure (IaC).
3. **Required Status Checks:** All CI workflows (linting, unit tests, security audits, and Playwright suites) must pass successfully before merging.
4. **Enforce Linear History (Squash and Merge):** We squash-merge pull requests into `main`. This maintains a clean commit history on the main branch where each commit represents a single, complete logical change.
5. **Require Sign-off / Verification:** Commits must be signed (GPG) to ensure author authenticity, and administrators are subject to the same protection rules.

---

## 💬 Commit Message Convention: Conventional Commits

We follow the **Conventional Commits v1.0.0** specification. This allows automated changelog generation, automatic semantic versioning bumps, and consistent repository readability.

### Commit Format

```text
<type>(<scope>): <description>

[optional body]

[optional footer(s)]
```

* **Type (Required):** Must be one of the branch prefixes (e.g., `feat`, `fix`, `refactor`, `perf`, `docs`, `chore`, `ci`, `test`).
* **Scope (Optional but highly recommended):** The specific area of the codebase being changed (e.g., `auth`, `evals`, `gateway`, `db`, `iac`).
* **Description (Required):** A short description of the code change:
  * Use the imperative, present tense ("add" not "added", "fix" not "fixes").
  * Do not capitalize the first letter.
  * Do not end the description with a period.

### Examples

#### Simple Feature Commit

```text
feat(gateway): add custom PII masking interceptor for LLM payloads
```

#### Bug Fix with Scope

```text
fix(auth): correct token validation clock skew on zero-trust proxy
```

#### Commit with Detailed Body and Footer (e.g., Jira/GitHub Reference)

```text
refactor(db): migration to encrypted tables for HIPAA workloads

Implemented column-level encryption for the patient records schema using AWS KMS keys. 
All queries have been modified to leverage decrypt operations transparently through our ORM model layer.

Closes #412
```

#### Breaking Change

Breaking changes must include `BREAKING CHANGE:` at the beginning of the footer or a `!` after the type/scope.

```text
feat(evals)!: deprecate legacy LangChain validation pipeline

BREAKING CHANGE: The older LangChain verification wrapper has been completely removed in favor of our custom Evals SDK.
```

---

## 🛠️ Commit and Branch Hygiene

* **Stash often, commit small:** Keep commits atomic. One commit should change one thing.
* **No "work in progress" commits on main:** Never merge commits with messages like `wip`, `fix`, `debug`, or `temp`. Clean up (interactive rebase and squash) your branch before marking your PR as ready for review.
