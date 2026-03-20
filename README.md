# 🚀 Open Source Contributions – AsyncAPI Generator

This repository documents my contributions to the **AsyncAPI Generator** project.  
My work primarily focused on **test reliability, CI workflow optimization, and documentation fixes**, with an emphasis on improving maintainability and engineering quality.

---

## 📌 Contribution Summary

- Improved **test isolation and determinism**
- Increased **test coverage for critical components**
- Introduced **better CI workflow design (parallelization + isolation)**
- Fixed **documentation inconsistencies**
- Followed **production-grade testing practices (mocking, snapshot validation, edge-case handling)**

---

## 🔧 Contributions in Detail

---

### 1. CI Workflow Optimization (Matrix Strategy)

🔗 PR: https://github.com/asyncapi/generator/issues/1995

#### 📍 Problem
The acceptance tests for multiple languages (JavaScript, Python, Java) were executed **sequentially within a single job**.

This caused:
- Failure in one language blocking others
- No per-language visibility in PR checks
- Slower CI due to lack of parallelism
- Harder debugging due to mixed logs

#### ⚙️ Solution
Refactored the workflow to use **GitHub Actions matrix strategy**, enabling:
- Parallel execution per language
- Isolated job environments
- Independent status reporting per language

#### 💡 Key Engineering Insight
This change improves **CI scalability and fault isolation**, aligning with modern CI/CD practices where independent test dimensions should not be coupled.

#### ✅ Impact
- Faster CI pipelines
- Improved debugging clarity
- Better contributor experience via granular feedback

---

### 2. Test Isolation for `utils.exists()`

🔗 PR: https://github.com/asyncapi/generator/pull/1982

#### 📍 Problem
Tests relied on the **real filesystem (`process.cwd`, actual files)**, causing:
- Non-deterministic behavior
- Environment-dependent failures
- Fragile test design

#### ⚙️ Solution
- Replaced real FS usage with **mocked `fs.promises.stat`**
- Used `jest.spyOn` for controlled mocking
- Covered both execution paths:
  - File exists → `true`
  - File does not exist → `false`
- Ensured proper **mock cleanup** to avoid cross-test pollution

#### 💡 Key Engineering Insight
Tests should be **pure and deterministic**, independent of external systems like filesystem or environment.

#### ✅ Impact
- Fully deterministic tests
- Improved reliability in CI
- Alignment with mock-driven testing practices

---

### 3. Snapshot Tests for CoreMethods Component

🔗 PR: https://github.com/asyncapi/generator/pull/1954

#### 📍 Problem
The `CoreMethods` README component lacked proper validation of rendered output across supported languages.

#### ⚙️ Solution
- Added **snapshot tests** to validate rendered output
- Covered:
  - Supported languages (JavaScript, Python)
  - Unsupported/missing language scenarios
- Ensured consistent output structure

#### 💡 Key Engineering Insight
Snapshot testing is effective for **UI/markdown output stability**, especially in documentation generators.

#### ✅ Impact
- Increased confidence in rendering logic
- Prevented regressions in multi-language support

---

### 4. Unit Tests for Installation README Component

🔗 PR: https://github.com/asyncapi/generator/pull/1945

#### 📍 Problem
The Installation README component had **language-dependent logic** but lacked direct test coverage.

#### ⚙️ Solution
- Added unit tests validating:
  - Language-specific rendering (Python vs JavaScript)
  - Output correctness of generated documentation
- Covered real rendering scenarios instead of shallow checks

#### 💡 Key Engineering Insight
Testing **rendered output instead of implementation details** ensures higher confidence in user-facing features.

#### ✅ Impact
- Improved coverage for critical public-facing component
- Reduced risk of documentation inconsistencies

---

### 5. Documentation Fix – Broken AsyncAPI Link

🔗 PR: https://github.com/asyncapi/generator/pull/1891

#### 📍 Problem
A documentation link pointed to a **non-existent path**, resulting in a 404 error.

Root cause:
- Duplicate path segment in URL

#### ⚙️ Solution
- Corrected the link to the valid path (`asyncapi-document`)

#### 💡 Key Engineering Insight
Even small documentation issues degrade **developer trust and onboarding experience**.

#### ✅ Impact
- Fixed broken navigation
- Improved documentation reliability

---

## 🧠 Key Learnings

- Importance of **test isolation and mocking strategy**
- Avoiding **global side effects in unit tests**
- Designing **scalable CI workflows using matrix strategy**
- Writing tests that validate **behavior, not just implementation**
- Maintaining **clean, minimal, and review-friendly PRs**

---

## 📈 Overall Impact

These contributions collectively improved:
- Test reliability and coverage
- CI performance and structure
- Developer experience
- Codebase maintainability

---

## 🔗 Repository

AsyncAPI Generator:  
https://github.com/asyncapi/generator

---
