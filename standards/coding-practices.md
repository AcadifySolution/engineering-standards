# Coding & Security Practices

All Acadify Solution developers must write code that is secure, compliant, and optimized for high performance. This document outlines our engineering standards for AI/LLM development, compliance-by-design (HIPAA/SOC2), database operations, and SaaS architecture.

---

## 🤖 AI & LLM Infrastructure Standards

When building and maintaining LLM-based pipelines, agents, and RAG systems, developers must design for unpredictability, latency, and compliance.

### 1. Personally Identifiable Information (PII) Masking

To maintain absolute compliance, **no raw PII must ever be sent to third-party LLM providers** (e.g., OpenAI, Anthropic, Gemini) or captured in application logs.

* **Custom Interceptors:** All outbound model requests must route through our PII masking middleware.
* **Sanitization Rules:** Detect and mask Name, SSN, Credit Card numbers, Phone numbers, Email addresses, and medical/financial identifier patterns.
* **De-identification:** Use hashing or placeholder tokens (e.g., `[CUSTOMER_NAME_1]`) so context is preserved for the model, and then reverse-map the masked fields locally when processing the output.

### 2. Prompt Sanitization & Defensive Input Control

* **Prompt Injection Mitigation:** Treat user prompts as untrusted input. Validate and sanitize input strings to strip system prompt override attempts.
* **Structured Formatting:** Use structured templates (like system/user message splits) rather than raw string concatenation.
* **Strict JSON Out:** Enforce structured outputs (e.g., JSON schema validation or tool calling) to ensure deterministic parsing.

### 3. Reliability & Gateway Resilience

* **Timeouts and Retries:** Set standard timeouts (max 15s) for API calls. Implement exponential backoff with jitter to handle rate limits (`HTTP 429`).
* **Fallback Strategies:** Provide fallback models (e.g., failing over to a lighter model) or user-facing error limits if the main model gateway is unavailable.
* **Observability:** Log latency, token count, cache hit rates, and model cost. Do not log the actual inputs or outputs if they contain customer workloads.

---

## 🛡️ Security & Compliance (HIPAA / SOC2)

As an engineering partner building clinical and financial infrastructure, zero-trust is our default operating standard.

### 1. HIPAA Compliance & Patient Privacy

* **Data at Rest:** All databases, caches (Redis), and disk storage containing Protected Health Information (PHI) must use AES-256 encryption.
* **Data in Transit:** Force TLS 1.3 for all internal and external communication. Disable deprecated SSL and TLS protocols (TLS 1.0, 1.1).
* **Row-Level Security (RLS):** Enable RLS on Postgres tables storing tenant or patient records to prevent cross-tenant leakages.

### 2. SOC2 Least-Privilege & Auditability

* **Structured Audit Logs:** Every security-sensitive action (authentication, privilege escalation, export of records, or encryption key rotations) must generate an immutable log event including:
  * Timestamp (UTC)
  * Actor ID (User or Service Account)
  * Action description
  * IP address and agent telemetry
* **Credential Management:** Never hardcode secrets, API keys, or database credentials. Use AWS Secrets Manager, GCP Secret Manager, or HashiCorp Vault. Pull secrets at runtime using environment variables.

---

## 💻 SaaS Architecture & API Design

### 1. Framework-Specific Standards

* **FastAPI (Python):**
  * Enforce request/response serialization using **Pydantic v2** schemas.
  * Utilize dependency injection (`Depends`) for sharing database sessions, authentication context, and service states.
  * Avoid using global state pools.
* **Go (Golang):**
  * Explicitly handle all errors; do not ignore errors with `_`.
  * Pass `context.Context` through all service functions and database queries to support timeout propagation and request cancellation.
  * Avoid package-level variables; use constructor injection (`NewService(...)`).

### 2. Error Handling & Response Design

* **Structured JSON Errors:** API errors must return a standard schema:

    ```json
    {
      "success": false,
      "error": {
        "code": "ERR_PII_SANCTITY_VIOLATION",
        "message": "Outbound prompt contains unmasked identifiers.",
        "details": {
          "field": "prompt.user_input"
        }
      }
    }
    ```

* **No Raw Stack Traces:** Never bubble raw database exceptions (e.g., `pgx` or `sqlalchemy` stack traces) to the client. Wrap exceptions in localized error contexts at the service boundary.

### 3. Testing Benchmarks

* **Unit Tests:** Must test all logic boundaries using mock interfaces (such as PyTorch mocks for data loaders or mock DB connections).
* **E2E Testing:** Playwright suites must run against staging targets to verify key user flows (login, billing, LLM interaction).
* **Coverage Baseline:** A minimum of **80% code coverage** is required on all new pull requests.
