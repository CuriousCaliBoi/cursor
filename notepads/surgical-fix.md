# Surgical Fix Notepad

Goal: Fix [specific issue] with minimal changes

Scope: Only touch [file(s)]. Do not change public APIs.

Constraints:
- Minimal diff required
- Preserve existing naming conventions
- Keep existing code style
- No unrelated changes or "improvements"
- Don't refactor unless explicitly asked

Given:
- Error: [paste error message or stack trace]
- Command to reproduce: [exact command]
- Relevant code: @[file paths or code snippets]
- Expected behavior: [what should happen]
- Actual behavior: [what's happening instead]

Deliver:
- Brief reasoning (1-2 lines explaining the fix)
- The patch (minimal code changes)
- Files modified (list with one-line summary per file)
- Validation steps (how to verify the fix works)

Example Usage:
```
Goal: Fix null pointer exception in user lookup
Scope: Only touch src/services/user.service.ts
Constraints: Minimal diff, no refactoring

Given:
- Error: "Cannot read property 'id' of undefined at UserService.getUser"
- Command: npm test -- user.service.test.ts
- Relevant code: @src/services/user.service.ts (lines 45-50)
- Expected: Return user object or null
- Actual: Throws error when user not found

Deliver: Minimal fix to handle undefined case
```

