# Contribution [#206]: Add compatibility test for $binarySize

**Contribution Number:** 1  
**Student:** Enrique Carrillo 
**Issue:** [[GitHub issue link] ](https://github.com/documentdb/functional-tests/issues/206) 
**Status:** Phase III in progress

---

## Why I Chose This Issue
I chose this issue as it presents a common scenario that I will be facing throughout my career. That issue/task being writing tests to ensure correct code functionality. By working on this task I hope to gain hands on experience with writing tests and how compatibility works. As a CS student in college this will help enchance my code comprehension skills and allow me to contribute more meaningful to other open source projects.


## Understanding the Issue

### Problem Description
Currently there is no issue present, what is missing is a compability test for the $binarySize function which needs to ensure that the function works the same between documentDB and mongoDB, not actually checking wether the function works as intended or not.

### Expected Behavior

The function $binarySize should work the same on both documentDB and mongoDB.

### Current Behavior

There is a possiblity that the function does not work the same on both documentDB and mongoDB which is why the compability test is needed.

### Affected Components

Many files are included but the main files are documentdb_tests and more specifically binarySize which is under documentdb_tests.

## Reproduction Process

### Environment Setup

Thankfully I faced no issues in setting up the enviroment. The CONTRIBUTING.md is very detailed and clear in what to do allowing for a smooth enviroment setup.

### Steps to Reproduce
As there is no current issue but the exact file can be difficult to find, here is the file tree to explore the get to the binarySize folder quickly.
  documentdb_tests/compatibility/tests/core/operator/expressions/misc/binarySize/

### Reproduction Evidence

- **Commit showing reproduction:** [Link to commit in your fork]
- **Screenshots/logs:** [If applicable]
- **My findings:** [What you discovered during reproduction]

---

## Solution Approach

### Analysis

[Your analysis of the root cause - what's causing the issue?]

### Proposed Solution

[High-level description of your fix approach]

### Implementation Plan

**Understand:**
$binarySize is an expression operator with well-defined behavior that currently lacks thorough test coverage. The goal is to close that gap by verifying DocumentDB and MongoDB behave identically across all meaningful input scenarios.

**Match:**
New tests mirror the structure and patterns already established by the $strLenBytes compatibility tests, which is a closely related operator with a complete test suite. The same conventions, utilities, and assertion helpers are reused for consistency.

**Plan:** [Step-by-step implementation plan]
Six new test files covering: byte counting (strings and binary data), null/missing inputs, input forms, type errors, and arity errors. A shared utilities module and a new named error code constant round out the additions. The existing smoke test will be left untouched.

**Implement:** 
https://github.com/enrique-c1/functional-tests/tree/fix-issue-206

**Review:** 
Tests follow project conventions: descriptive names, docstrings, one assertion per test, no magic numbers, and constants pulled from the shared framework. Commits are present-tense and concise, I will run pre-commit before pushing.

**Evaluate:**
Run the new test suite against both MongoDB and DocumentDB and confirm identical results. Any disagreement is either a real compatibility finding or an expectation to correct against MongoDB's behavior.

---

## Testing Strategy

### Unit Tests

- [ ] Compatibility tests for the $binarySize operator: verifying DocumentDB and MongoDB return identical byte sizes for string (UTF-8 byte count) and BinData (payload length) inputs
- [ ] Test case 2: [Description]
- [ ] Test case 3: [Description]

### Integration Tests

- [ ] Integration scenario 1
- [ ] Integration scenario 2

### Manual Testing

[What you tested manually and results]

---

## Implementation Notes

### Week 1 Progress

Added compatibility tests for the $binarySize operator, verifying DocumentDB and MongoDB return identical byte sizes for string (UTF-8 byte count) and BinData (payload length) inputs, with MongoDB as the reference. Created 21 parametrized cases covering ASCII/multibyte strings, embedded nulls, and binary payloads across different subtypes. The main challenge was the validation environment: a free Atlas M0 cluster rejected every test because its 38-byte database-name cap is smaller than the framework's auto-generated names, so I switched to a local MongoDB instance where all 21 passed. Some decisions I made were: centralizing the shared test dataclass in utils/ to avoid duplication across rounds, keeping UTF-8 cases representative rather than exhaustive (that encoding behavior is covered elsewhere).

### Week [2] Progress

WIP

### Code Changes

- **Files modified:** test_binarySize_byte_counts.py
- **Key commits:** https://github.com/enrique-c1/functional-tests/tree/fix-issue-206
- **Approach decisions:** I chose to treat any DocumentDB-only failure as a real compatibility finding rather than loosening assertions, this was because if there was a failure but only on DocumentDB it meant that there was a discrepancy between documentDB and mongoDB, loosening assertions would only defeat the purpose of the compability tests.


---

## Pull Request

**PR Link:** [GitHub PR URL when submitted]

**PR Description:** [Draft or final PR description - much of the content above can be adapted]

**Maintainer Feedback:**
- [Date]: [Summary of feedback received]
- [Date]: [How you addressed it]

**Status:** [Awaiting review / Iterating / Approved / Merged]

---

## Learnings & Reflections

### Technical Skills Gained

[What you learned technically]

### Challenges Overcome

[What was hard and how you solved it]

### What I'd Do Differently Next Time

[Reflection on your process]

---

## Resources Used

- [Link to helpful documentation]
- [Tutorial or Stack Overflow post that helped]
- [GitHub issues or discussions that helped]
