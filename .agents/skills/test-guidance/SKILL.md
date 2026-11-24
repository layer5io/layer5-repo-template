---
name: test-guidance
description: Testing standards, test execution, and evidence collection for Layer5 repositories. Use when writing, running, debugging, or verifying unit, integration, or e2e tests.
---

# Test Guidance Skill

Instructions for running tests and verifying behavioral correctness.

## Test Workflow

1. **Discovery**:
   - Check `Makefile` for test targets (`make test`, `make unit-test`, `make integration-test`).
   - Identify language test runners (`go test ./...`, `npm test`, `pytest`).

2. **Execution**:
   - Run tests locally before opening a pull request.
   - Keep test execution deterministic: avoid hardcoded local paths, fixed ports, or race conditions.

3. **Test Evidence**:
   - Record test pass status in PR descriptions.
   - If UI or CLI output changes, provide clear execution outputs or screenshots.
