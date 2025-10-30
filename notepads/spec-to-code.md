# Spec to Code Notepad

Spec:
- User story: [As a {user}, I want {goal} so that {benefit}]
- Acceptance criteria:
  1. [Specific, testable criterion]
  2. [Another criterion]
  3. [Edge case handling]
- Inputs/outputs with examples:
  - Input: [example input]
  - Output: [example output]
- Non-goals: [What NOT to implement]
- Constraints: [Technical limitations, dependencies, etc.]

Request:
1. Propose file changes (list with one-line summary per file)
2. Implement in small, incremental steps
3. Add/extend tests to cover all acceptance criteria
4. Ask ONE clarifying question if any ambiguity remains (don't proceed with assumptions)
5. Follow existing project patterns and conventions

Validation:
- All acceptance criteria are met
- Tests pass: [test command]
- Code style verified: [lint command]
- Type checking passes: [typecheck command]

Example Usage:
```
Spec:
- User story: As a developer, I want to filter API logs by date range so that I can debug issues in a specific time period
- Acceptance criteria:
  1. Can filter logs by start date and end date
  2. Returns only logs within date range (inclusive)
  3. Handles invalid date formats gracefully
- Inputs/outputs:
  - Input: { startDate: "2024-01-01", endDate: "2024-01-31" }
  - Output: Array of log entries within date range
- Non-goals: Don't implement pagination or sorting (future work)
- Constraints: Use existing date utility functions, maintain API response format

Request: Implement date filtering for logs API endpoint
```

