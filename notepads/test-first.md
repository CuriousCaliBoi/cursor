# Test-First Development Notepad

TDD Workflow: Write failing test, then implement minimal fix

Feature: [Brief description of feature or fix]

## Step 1: Write Failing Test
- Test file: @[path to test file]
- Test case: [What specific behavior to test]
- Expected behavior: [What should happen]
- Test should fail initially (red)

Test Structure:
```typescript
describe('[Feature Name]', () => {
  it('should [expected behavior]', () => {
    // Arrange
    // Act
    // Assert
    expect(...).toBe(...)
  })
})
```

## Step 2: Implement Minimal Fix
- Implementation file: @[path to source file]
- Keep diff tight (only what's needed to make test pass)
- Make test pass (green)
- Don't optimize or refactor yet

## Step 3: Refactor (if needed)
- Improve implementation while keeping tests passing
- Clean up code
- Maintain test coverage
- Tests should still pass (green)

## Test Coverage
Ensure tests cover:
- [ ] Happy path (normal case)
- [ ] Error cases (invalid input, failures)
- [ ] Edge cases (boundary conditions)
- [ ] Integration points (if applicable)

## Validation
- Run: `make test` (all tests pass)
- Coverage: [target coverage if applicable]
- Manual verification: [if needed]

Example Usage:
```
Feature: User email validation

Step 1: Write failing test in @src/utils/validation.test.ts
- Test that validateEmail() returns false for invalid emails
- Test that it returns true for valid emails
- Test edge cases: empty string, null, malformed emails

Step 2: Implement in @src/utils/validation.ts
- Minimal regex or validation logic
- Just enough to make tests pass

Step 3: Refactor if needed
- Improve regex pattern
- Add better error messages
- Keep tests passing

Validation:
- make test (all validation tests pass)
- Manual: Test with various email formats
```

