# Security Policy

At Acadify Solution, we build high-reliability AI products, scalable SaaS platforms, and secure cloud infrastructure. The security of our services and the privacy of our clients' data (including HIPAA-regulated workloads) are paramount.

This document outlines our policy for reporting security vulnerabilities. We appreciate the efforts of security researchers and developers who help us keep our systems safe.

---

## 🛡️ Supported Versions

We actively monitor and patch the following versions of our open-source blueprints and standards:

| Version  | Supported                |
| :------- | :----------------------- |
| >= 1.0.0 | Active Security Patches  |
| < 1.0.0  | Best Effort / Deprecated |

---

## 🚨 Reporting a Vulnerability

If you discover a security vulnerability or compliance breach in any of our repositories, applications, or infrastructure, **do not open a public issue.**

Please report it privately to our security coordination team:

- **Email:** <contact@acadifysolution.com>
- **Response Time:** You will receive an initial response acknowledging your report within **24 hours**.
- **PGP Key:** If you wish to encrypt your message, please contact us first to request our active public key.

### Please Include in Your Report

1. **Vulnerability Description:** A detailed explanation of the vulnerability or risk (e.g., SQL injection, authorization bypass, PII exposure).
2. **Steps to Reproduce:** Clear, step-by-step instructions (with proof-of-concept code, HTTP requests, or command-line logs if applicable).
3. **Potential Impact:** Your assessment of the severity and impact of the issue (e.g., user data exposure, remote code execution).
4. **Target Details:** The specific repository name, host URL, or API endpoint where the issue was found.

---

## 🤝 Our Commitment

If you follow these guidelines when reporting an issue, we commit to:

- **Prompt Communication:** Keeping you updated as we investigate and remediate the issue.
- **Remediation:** Deploying a fix within **30 days** for high/critical vulnerabilities, and up to **90 days** for low/medium issues.
- **Responsible Disclosure:** Coordinating a public disclosure timeline with you once the patch has been deployed to all production instances. We request that you do not publish the vulnerability details until a fix is released.
- **No Legal Action:** We will not pursue legal action against researchers who access data or systems in good faith for testing, provided they do not destroy data, execute denial of service attacks, or exploit vulnerabilities for malicious purposes.
