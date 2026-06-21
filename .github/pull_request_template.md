# Pull Request Template

## Description

Please provide a clear and concise description of the changes proposed in this PR. Detail the problem being solved and the technical approach chosen.

## Type of Change

- [ ] 🚀 Feature (New capability for AI, SaaS, or Infrastructure)
- [ ] 🐛 Bug Fix (Resolves an active issue)
- [ ] 🔒 Security / Compliance (Addresses HIPAA/SOC2/PII vulnerability or control)
- [ ] ⚙️ Refactor / Chore (Clean up, performance optimization, dependency bump)
- [ ] 📝 Documentation (Updates to setup, standards, or API docs)

## Scope of Impact

- [ ] **AI & LLM Infrastructure:** PyTorch pipelines, model gateways, RAG, custom agents.
- [ ] **Product & SaaS Platform:** Next.js UI, FastAPI/Go backend services, database migrations.
- [ ] **Cloud & DevOps Automation:** Terraform IaC, Kubernetes configurations, GitHub Actions.
- [ ] **Security & Compliance:** PII masking middleware, authorization rules, auditing tools.

---

## SDLC Quality Checklist

Please verify that each of the following requirements is completed before marking this PR as ready for review:

### 1. Code Quality & Formatting
- [ ] Code compiles and builds locally without errors or warnings.
- [ ] Code styles adhere to the language-specific formatting standard (Prettier, Black, Go fmt).
- [ ] No temporary debug logs, print statements, or commented-out code blocks are left in.

### 2. Testing & Verification
- [ ] Unit tests written and passing for all modified logic (FastAPI, Go, PyTorch).
- [ ] Integration or E2E tests run successfully (Playwright, regression suites).
- [ ] Test coverage meets the team threshold (minimum 80% coverage on new code).

### 3. Compliance & Security by Design
- [ ] **PII Masking:** Verified that personal data (PII) is sanitized before transit to LLMs or external logging.
- [ ] **Security Scans:** Local dependency vulnerability scanning run and verified clean (e.g., `npm audit`, `safety check`).
- [ ] **HIPAA/SOC2:** Audited modifications against least-privilege policies, secure database queries, and log auditing.

### 4. Release Readiness
- [ ] Release checklist followed (see [release-management.md](file:///Users/acadify/Desktop/engineering%20standards/standards/release-management.md)).
- [ ] SemVer impact identified: [Major / Minor / Patch].
- [ ] Changelog draft or release notes draft included below (if applicable).

---

## Verification Evidence

Provide outputs, command logs, or screenshots confirming that the changes have been verified. For UI changes, please attach screenshots or screen recordings showing the UI behavior in different viewports.

### Local Test Output Snippet
```bash
# Paste test run results here
```
