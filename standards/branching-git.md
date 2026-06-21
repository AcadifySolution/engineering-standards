# Git Branching & Commit Guidelines

To maintain continuous integration, clean release lineages, and straightforward rollbacks, all Acadify Solution projects follow a disciplined Git workflow.

---

## 🌿 Branching Model: Trunk-Based Development

We follow a **Trunk-Based Development** model. Developers work in short-lived feature branches, merge them into `main` frequently, and avoid long-running divergence.

### Branch Categories and Naming Conventions

All branch names must be lowercase, hyphen-delimited, and prefixed with a standardized type:

| Branch Prefix | Purpose                                     | Example                      |
| :------------ | :------------------------------------------ | :--------------------------- |
| `feat/`       | A new feature or capability                 | `feat/llm-pii-masking`       |
| `fix/`        | A bug fix                                   | `fix/oauth-refresh-token`    |
| `refactor/`   | Code refactoring without behavioral changes | `refactor/fastapi-routes`    |
| `perf/`       | Performance optimization                    | `perf/vector-query-indexing` |
| `docs/`       | Documentation changes only                  | `docs/api-specs`             |
| `chore/`      | Maintenance tasks, dependency bumps         | `chore/upgrade-playwright`   |
| `ci/`         | GitHub Actions or DevOps tooling changes    | `ci/configure-lint-workflow` |
| `test/`       | Adding or updating tests                    | `test/auth-integration`      |

### Branch Lifecycle & Rebase Strategy

1. **Keep Lifespan Short:** Do not let feature branches diverge from `main` for more than 3 days. If a feature requires more time, merge it incrementally using feature flags.
2. **Rebase, Don't Merge:** Use `git rebase main` instead of `git merge main` to keep your branch history linear and up-to-date.
3. **Force-With-Lease:** When updating a remote feature branch after a rebase, never use `git push --force`. Always use `git push --force-with-lease` to avoid overwriting commits pushed by collaborators.

---

## 🛡️ Branch Protection Rules

Our GitHub repositories enforce strict protection on the `main` branch to guarantee system stability:

1. **No Direct Commits:** All modifications must go through a Pull Request. Direct pushes to `main` are blocked.
2. **Required Code Reviews:** At least **one (1) senior engineer approval** is required before a PR can be merged. Two (2) approvals are required for changes touching our core AI pipelines, HIPAA-compliant databases, or root cloud infrastructure (IaC).
3. **Required Status Checks:** All unit tests, compliance scans, and Playwright integration suites must pass successfully before a merge is enabled.
4. **Enforce Linear History (Squash and Merge):** We squash-merge pull requests into `main` to maintain a clean git history.

---

## 💬 Commit Message Convention: Conventional Commits

We follow the **Conventional Commits v1.0.0** specification. Consistent commit messaging allows us to generate changelogs and determine semantic version bumps automatically.

### Commit Format

```text
<type>(<scope>): <description>

[optional body]

[optional footer(s)]
```

- **Type (Required):** Must be one of the branch prefixes (e.g., `feat`, `fix`, `refactor`, `perf`, `docs`, `chore`, `ci`, `test`).
- **Scope (Optional but recommended):** The specific area of the codebase being changed (e.g., `auth`, `evals`, `gateway`, `db`, `iac`).
- **Description (Required):** A short summary of the code change:
  - Use the imperative, present tense ("add" not "added", "fix" not "fixes").
  - Do not capitalize the first letter.
  - Do not end the description with a period.

### Examples

#### Feature Implementation

```text
feat(gateway): add custom PII masking interceptor for LLM payloads
```

#### Bug Fix

```text
fix(auth): correct token validation clock skew on zero-trust proxy
```

#### Breaking Change

Breaking changes must include `BREAKING CHANGE:` at the beginning of the footer or a `!` after the type/scope:

```text
feat(evals)!: deprecate legacy LangChain validation pipeline

BREAKING CHANGE: The legacy validation pipeline has been removed. Switch to the Evals SDK.
```

---

## 🛠️ Squash-Merge & Clean-Up Hygiene

### Cleaning Up Squash Commit Messages

When merging a PR via the GitHub UI, **do not accept the default aggregated commit message** (which contains a list of intermediate commits like "wip", "fixed lint", or "test again").

- The merger must rewrite the squash commit title to match the **Conventional Commits** format.
- The body of the squash commit should summarize the overall feature, referencing Jira tickets or GitHub issue numbers (e.g., `Closes #123`).

### Branch Cleanup

Always delete the local and remote feature branch immediately after a merge.

```bash
# Delete remote branch
git push origin --delete feat/my-feature-branch

# Delete local branch
git branch -d feat/my-feature-branch
```
