# Public repository maintenance — 14 October 2026

This pass covers the nine public engineering repositories listed below and the
organisation profile. It excludes every private repository, `demo-repository`,
`Impactbridge-CSR-Tool`, and all personal-account content. No cloud infrastructure
was deployed. These results describe local validation of the proposed changes;
GitHub Actions and merge status must be checked on each pull request.

| Repository                   | Main correction                                                                             | Local validation                                                                                            |
| ---------------------------- | ------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------- |
| `.github`                    | Accurate organisation profile and complete eligible project directory                       | Markdown and project links checked                                                                          |
| `Sales-Automation`           | Follow-up imports work both as a module and a script                                        | 2 import regression tests and the CI smoke import                                                           |
| `aegis-mvp-launchpad`        | Restore missing estimation implementation; update backend dependencies                      | 5 tests, backend lint, frontend production build; runtime dependency audit reports no known vulnerabilities |
| `ai-evals-framework`         | Repair malformed package files and explicit package discovery                               | Editable install, CLI help, 11 tests, lint, Terraform validation                                            |
| `asr-feedback`               | Fix Markdown configuration and broken anchors; validate schema examples                     | Documentation lint, 3 schema/example pairs, JavaScript and Python syntax                                    |
| `autonomous-agent-swarm`     | Persist and migrate task priority; clear recovered assignments; queue compatibility         | 36 tests and lint                                                                                           |
| `engineering-standards`      | Repair formatting and upgrade documentation tooling                                         | Markdown lint and Prettier checks                                                                           |
| `enterprise-rag-boilerplate` | Retain scope filters during sibling expansion; fix phone masking and local answer synthesis | 14 tests and lint                                                                                           |
| `fine-tuning-pipeline`       | Install actual CPU test dependencies in CI and fix lint/formatting                          | 5 tests, config parsing, lint, Terraform validation                                                         |
| `llm-security-proxy`         | Repair syntax and injection regexes; validate Terraform syntax in CI                        | 20 tests, lint, Terraform validation; runtime dependency audit reports no known vulnerabilities             |

## Follow-up requiring a separately tested dependency migration

- Aegis frontend: after compatible updates, npm audit reports **6 high and
  3 moderate** development-tool dependency findings. The reported fixes include
  major Tailwind and Vite upgrades. A production build succeeds, but that does not
  resolve the advisories. Test the CSS/build migration and browser behavior before
  changing major versions. Do not expose the development server publicly.
- Engineering Standards: the refreshed documentation stack reports **3 moderate
  and 3 low** transitive dependency findings, with no high or critical findings.
  Keep the exact lockfile and recheck upstream fixes. Do not equate a passing
  Markdown check with a clean dependency audit.

## Repeating a maintenance pass

1. Discover public organisation repositories and apply exclusions before reading contents.
2. Check existing PRs and branch heads; continue relevant work instead of duplicating it.
3. Work on focused branches from the current default branch and preserve unrelated changes.
4. Fix observed defects, run project-specific checks, and document limitations.
5. Push descriptive commits and open PRs with validation evidence. Respect review and CI gates.
6. Record actual merged state separately from open proposals and local checks.

The current projects already cover evaluation, retrieval, adaptation, orchestration,
security, feedback, planning, sales workflows, and engineering guidance. This pass
did not identify a concrete need for another repository.
