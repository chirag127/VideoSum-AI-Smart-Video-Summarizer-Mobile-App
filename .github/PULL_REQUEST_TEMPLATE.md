# PR Title Convention

Use Conventional Commits: `type(scope): subject`

**Examples:**
*   `feat(auth): implement biometric login using local storage`
*   `fix(parser): resolve edge case for empty video titles`
*   `refactor(ui): standardize all button styles to Tailwind utility class v4`

---

## 🚀 Feature/Fix Overview

**BLUF (Bottom Line Up Front):** Summarize the core purpose of this PR in one sentence. What does this change achieve?

<!-- Briefly describe the motivation and context. Why is this change necessary? -->

---

## ✅ Checklist: The Apex Gate

Ensure all mandatory architecture and quality gates have been passed before requesting review.

### Code Quality & Architecture
- [ ] **SOLID Principles:** Adherence checked (SRP enforced for new modules).
- [ ] **CQS Enforced:** Commands only mutate state; Queries only return data.
- [ ] **DRY/KISS:** Logic is not duplicated and complexity is minimal.
- [ ] **Input Sanitization:** All external inputs (API, user, config) are validated/sanitized.
- [ ] **Error Handling:** Critical paths use `try/catch/finally` or appropriate Rust/Go error handling.

### Testing & Verification
- [ ] **Unit Tests:** Added/Updated tests in `tests/` corresponding to all logic changes.
- [ ] **Coverage:** Target coverage is maintained or improved (minimum 85%).
- [ ] **E2E Test Snippet:** (If UI/Flow change) A brief description of the manual E2E steps required for verification.
- [ ] **Linting:** `biome check --apply` passed successfully locally.

### Documentation & Metadata
- [ ] **README.md:** Updated if new features, dependencies, or architectural shifts occurred.
- [ ] **AGENTS.md:** Updated if core language stack changed (Not applicable for minor fixes).
- [ ] **Dependencies:** New packages added or updated are reviewed for security and performance.

---

## 🧠 Detailed Changes (Structured Log)

Use this section to detail the technical implementation, architectural choices, and dependency impact.

### 1. Architectural Decisions

<!-- e.g., Switched from Redux to Zustand Signals for global state management in the Auth feature due to performance bottlenecks. -->

### 2. Dependencies Impact

<!-- List any new packages or major version bumps affecting the ecosystem (e.g., React Native 0.74 -> 0.75). -->

### 3. Testing Strategy

<!-- Specific mocks used, isolated test setup, or integration points tested. -->

---

## ⚙️ Reviewer Instructions

1.  **Focus Area:** Please prioritize reviewing the logic within `src/features/[module]/...`.
2.  **Performance Check:** Verify that the new UI elements maintain an INP score below 200ms.
3.  **Security:** Pay close attention to data serialization/deserialization around the summarization API calls.

**Thank you for enforcing the Zero-Defect standard.**