# Coding & Security Practices

All Acadify Solution developers must write code that is secure, compliant, and optimized for high-performance workloads. This document details our engineering policies for AI/LLM integration, HIPAA/SOC2 compliance, database hygiene, API error design, and testing protocols.

---

## 🤖 AI & LLM Infrastructure Standards

When building and maintaining LLM-based agents, evaluation runs, and RAG pipelines, developers must design for latency, rate limits, and compliance.

### 1. Zero-Trust PII Masking Interceptors

**No Protected Health Information (PHI) or Personally Identifiable Information (PII) must ever reach external model provider gateways** (e.g., OpenAI, Anthropic, Gemini).

- **Outbound Gateways:** All outbound prompt payloads must route through our PII masking interceptor library.
- **Tokenization & Re-identification:** Use local regex engines (e.g., Presidio or custom regex) to extract SSNs, emails, credit cards, dates of birth, and names. Replace these tokens with placeholder identifiers (e.g., `{{DOB_1}}`, `{{NAME_2}}`) before dispatching to external APIs.
- **Reverse Mapping:** Retain the mapping in-memory or in an encrypted Redis cache. Rehydrate the masked details into the response locally after receiving the model's output.

### 2. Defensive Prompt Design

- **Prompt Injection Safeguards:** Sanitize user input text to prevent jailbreaks or prompt injections. Never embed raw, unsanitized user strings directly into system prompts. Use structured templates (like message lists or function parameters) to isolate user inputs from model instructions.
- **Deterministic Output Parsing:** Configure APIs to enforce structured formats (JSON Schema or tool/function calling) to prevent parser failures. Always implement recovery parsing logic when raw LLM strings are returned.

### 3. Rate-Limiting & Gateway Failovers

- **Adaptive Backoff:** Model providers enforce rate limits (`HTTP 429`). Use exponential backoff with jitter to retry transient rate-limit errors.
- **Fallback Fallback Routing:** If a primary model (e.g., GPT-4o) fails or times out, implement an automatic fallback path to a local or alternative model (e.g., Gemini Flash) or return a clean, structured validation failure to the user rather than an application crash.

---

## 🛡️ Security & Compliance (HIPAA / SOC2)

As a development partner handling clinical and financial workloads, security controls must be designed into every component.

### 1. Data Encryption & Storage

- **Encryption at Rest:** Ensure AES-256 encryption is active on all data stores (PostgreSQL, Redis, Elasticsearch).
- **Encryption in Transit:** Force TLS 1.3 for external endpoints and internal service-to-service communication. Disable TLS 1.0, 1.1, and 1.2 across all load balancers.
- **Row-Level Security (RLS):** Enable RLS on Postgres databases. All queries must resolve tenant context dynamically to prevent cross-tenant data leakages.

### 2. Audit Trails & Logs

- **Immutable Security Logs:** Log all authentication attempts, authorization failures, encryption key rotations, and direct reads of sensitive medical/financial data.
- **Sanitized Application Logs:** Verify that application logs do not capture API keys, tokens, session cookies, passwords, or customer PII. Run daily automated log scans to identify and flag leaks.

---

## 💻 Database & Connection Lifecycle

Improper database connection pooling and dangling transactions are major sources of staging and production degradations.

### 1. Connection Pool Sizing

- Do not set database connection pools to arbitrarily high limits. Limit connections to `(2 * CPU cores) + disk speed factor` to prevent query queue serialization.
- Configure connection timeouts: Set a connection acquisition timeout (max 5s) and query runtime timeouts (max 15s) to prevent slow queries from locking database worker threads.

### 2. Transaction Safety & Timeouts

- Keep database transactions as short as possible. Never make outbound API calls (e.g., to LLM providers or payment gateways) from inside a database transaction block. Doing so keeps database locks open, leading to starvation.
- **Idle Transaction Timeouts:** Configure `idle_in_transaction_session_timeout = 10000` (10 seconds) on Postgres instances. This automatically kills connections that are left hanging in uncommitted transaction blocks.

---

## ⚙️ API Error Design & Consistency

### 1. Error Code Hierarchy

API endpoints must return standard HTTP status codes accompanied by a structured JSON error body. Do not return raw exceptions (e.g., database stack traces) to client interfaces.

```json
{
  "success": false,
  "error": {
    "code": "ERR_PII_DETECTION_TRIGGERED",
    "message": "Prompt execution aborted. Outbound payload contains unmasked personal identifiers.",
    "details": {
      "detected_fields": ["phone_number"],
      "action_required": "Please filter inputs or register masking overrides."
    }
  }
}
```

---

## 🧪 Testing and Preventing Test Flakiness

### 1. Playwright E2E Best Practices

Flaky integration tests waste developer time and degrade CI confidence.

- **No Arbitrary Sleeps:** Never use `page.waitForTimeout(3000)` or similar hardcoded delays. They slow down CI runs and fail under load.
- **State-driven Waiting:** Always wait for specific DOM elements, network events, or URL changes (e.g., `page.locator('button').click()`, followed by `expect(page.locator('.toast-success')).toBeVisible()`).
- **Mock Network Latency:** When testing loading states or edge cases, mock network responses instead of slowing down actual backends.

### 2. Unit Test Mocking Boundaries

- Unit tests must remain fast and execute locally without dependencies on databases or external networks.
- Use libraries like `pytest-mock` or Go interfaces to mock API callouts, file system interactions, and model loader states. Mock all external HTTP calls using tools like `responses` or `nock`.
