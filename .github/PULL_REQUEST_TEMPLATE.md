# Pull Request Template

Thank you for your contribution to **VideoSum-AI-Video-Summarizer-Mobile-App**!

Please review the following checklist before submitting your pull request:

## Checklist

- [ ] **Reasonable Change:** My changes are well-reasoned and address the issue/feature described.
- [ ] **Self-Contained:** My changes are not overly broad and focus on a single concern.
- [ ] **Tests:** I have added or updated unit/integration tests to cover my changes.
- [ ] **Documentation:** I have updated relevant documentation (if applicable).
- [ ] **Code Style:** My code follows the project's established code style (linted by Ruff, formatted by Ruff).
- [ ] **Build & Test:** My changes pass all CI checks and tests locally (`pytest`, `npm test`).
- [ ] **Dep Updates:** I have updated dependencies if necessary and verified compatibility.
- [ ] **AI Agent Alignment:** My changes align with the **AGENTS.md** directives and maintain the Apex Technical Authority standards.

## Description

Please provide a clear and concise description of your changes. What problem does this pull request solve? What new feature does it introduce?

**Related Issue(s):** (Link to any relevant GitHub issues, e.g., `Fixes #123`)

## Type of Change

- [ ] Bug fix (non-breaking change which fixes an issue)
- [ ] New feature (non-breaking change which adds functionality)
- [ ] Breaking change (fix or feature that would cause existing functionality to not work as expected)
- [ ] Documentation update
- [ ] Refactoring
- [ ] Performance improvement

## How Has This Been Tested?

Describe the tests that you ran to verify your changes. Please also note any relevant testing configurations.

- **Local Testing:**
  - Unit Tests: `pytest`
  - E2E/Integration Tests: `npm run test:e2e` (or relevant command)
  - Manual Testing:
    - **iOS Simulator/Device:** [Describe steps]
    - **Android Emulator/Device:** [Describe steps]

- **CI/CD Pipeline:** The pipeline will run tests and checks on the repository `https://github.com/chirag127/VideoSum-AI-Video-Summarizer-Mobile-App`.

## Screenshots (If Applicable)

If your changes affect the UI, please provide screenshots or a video recording of the changes.

## Additional Context

Add any other context about the problem or your solution here.
