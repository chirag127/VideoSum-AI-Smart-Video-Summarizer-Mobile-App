# Security Policy for VideoSum-AI-Powered-Video-Summarization-Mobile-Platform

As the Apex Technical Authority, security is a foundational, non-negotiable aspect of this mobile platform. We operate under the principle of **Security by Design** and adhere to the latest industry best practices for cross-platform mobile applications interacting with backend AI services.

## 1. Supported Versions

This project prioritizes security patching for actively maintained versions of React Native/Expo and the underlying TypeScript tooling.

| Version | Status | Support Updates |
| :--- | :--- | :--- |
| Latest Stable | Supported | Critical & High Severity Fixes |
| Previous Stable | Maintenance | Critical Severity Fixes Only |
| Older Versions | Unsupported | None |

## 2. Reporting Vulnerabilities

We value proactive security reporting. If you discover a vulnerability in `VideoSum-AI-Powered-Video-Summarization-Mobile-Platform`, please follow these steps immediately:

1.  **DO NOT** create a public issue or commit a fix before notifying the maintainers.
2.  Email the dedicated security channel: `security+videosum@users.noreply.github.com`. Please use clear subject lines such as `[SECURITY REPORT] VideoSum Vulnerability`.
3.  Include detailed, step-by-step instructions to reproduce the vulnerability, the affected component (e.g., Expo configuration, native module linkage, API handling), and the potential impact.
4.  We will acknowledge receipt within 48 hours.

## 3. Security Auditing and Practices

### A. Mobile Application Security (React Native/Expo)

*   **Dependency Scanning:** Continuous scanning of the dependency tree using tools integrated into our CI pipeline (`.github/workflows/ci.yml`) to detect known CVEs in JavaScript/TypeScript packages.
*   **Sensitive Data Handling:** All locally stored sensitive data (e.g., API keys, user tokens) must be managed via secure storage solutions appropriate for iOS (Keychain) and Android (Keystore), typically abstracted through specialized React Native libraries.
*   **Insecure Data Transmission:** All communication with the summarization backend API **MUST** occur over TLS 1.3+. We strictly forbid non-HTTPS communication.

### B. Backend/AI Service Interaction

*   **API Key Management:** Production API keys for external AI services (e.g., OpenAI, Gemini) are **NEVER** hardcoded in the mobile client. They are managed server-side (proxied) or securely injected at build time only for non-sensitive public keys.
*   **Input Sanitization:** All user-submitted data intended for backend processing (e.g., video URLs) undergoes rigorous server-side sanitization to prevent injection attacks against the summarization pipeline.

### C. Supply Chain Security (CI/CD)

Our Continuous Integration process (`.github/workflows/ci.yml`) enforces the following:

1.  **Automated Checks:** Biome formatting and linting checks must pass (Zero Errors).
2.  **Testing Threshold:** Code Coverage must remain above **85%** (verified via Codecov badge).
3.  **Signed Commits:** For critical branches, signed commits are highly encouraged to ensure author authenticity.

## 4. Responsible Disclosure Policy

We commit to resolving security issues promptly based on severity. We will maintain transparency throughout the remediation process, communicating updates only through the established private channels until a fix is deployed to production and appropriate public advisories are issued. Any external researcher adhering to this policy will be publicly acknowledged upon resolution (if they desire) in the project's release notes.