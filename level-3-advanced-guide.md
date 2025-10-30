# Level 3 Advanced: Pattern Recognition & Automation Guide

## 3.1 Custom Modes

### Understanding Custom Modes

**Custom Modes** are specialized AI configurations tailored to specific task types. They combine:
- Specific instructions/prompts
- Tool configurations
- Model preferences
- Context filters

**When to Create Custom Modes**:
- You repeatedly perform the same type of task
- Tasks require different approaches (debugging vs. architecture)
- You want consistent behavior across similar tasks
- Team wants standardized workflows

### Mode Design Patterns

#### 1. Debugging Mode

**Purpose**: Focus on error analysis, stack traces, and log inspection.

**Configuration**:
```
Focus Areas:
- Error messages and stack traces
- Log files and debugging output
- Code paths that lead to errors
- State at time of failure

Approach:
- Start with error message analysis
- Trace execution flow
- Identify root cause before suggesting fixes
- Propose minimal changes to fix issue
- Consider edge cases that might cause similar issues

Output Format:
1. Error Analysis: [what the error means]
2. Root Cause: [why it's happening]
3. Solution: [how to fix]
4. Prevention: [how to avoid in future]
```

**Use Cases**:
- Investigating production bugs
- Analyzing test failures
- Understanding unexpected behavior
- Performance debugging

#### 2. Testing Mode

**Purpose**: Prioritize test generation, coverage, and edge cases.

**Configuration**:
```
Focus Areas:
- Test coverage and gaps
- Edge cases and boundary conditions
- Test quality and maintainability
- Integration scenarios

Approach:
- Always consider edge cases first
- Write tests before fixes when possible (TDD)
- Ensure tests are readable and maintainable
- Verify test isolation and independence
- Check for test coverage of error paths

Output Format:
- Test strategy: [what to test]
- Test cases: [specific scenarios]
- Implementation: [test code]
- Coverage analysis: [what's covered/missing]
```

**Use Cases**:
- Adding tests for new features
- Improving test coverage
- Writing regression tests
- Test refactoring

#### 3. Refactoring Mode

**Purpose**: Emphasize safety, behavior preservation, and incremental steps.

**Configuration**:
```
Focus Areas:
- Code quality and maintainability
- Architecture improvements
- Performance optimizations
- Technical debt reduction

Approach:
- Preserve behavior above all else
- Make incremental, safe changes
- Verify with tests before and after
- Document risks and rollback plans
- Prefer small commits over large refactors

Safety Checklist:
- [ ] All tests pass before starting
- [ ] Changes are backward compatible
- [ ] Public APIs unchanged (or deprecated properly)
- [ ] No behavior changes unless explicitly intended
- [ ] Rollback plan documented

Output Format:
1. Refactoring Plan: [what to change and why]
2. Risk Assessment: [what could break]
3. Incremental Steps: [how to do it safely]
4. Validation: [how to verify success]
```

**Use Cases**:
- Improving code structure
- Extracting common patterns
- Simplifying complex logic
- Migrating to new patterns

#### 4. Architecture Mode

**Purpose**: Focus on design patterns, boundaries, and dependencies.

**Configuration**:
```
Focus Areas:
- System design and architecture
- Module boundaries and interfaces
- Dependency management
- Scalability and maintainability

Approach:
- Consider system-wide implications
- Evaluate multiple design options
- Document trade-offs and decisions
- Consider future extensibility
- Ensure clear boundaries between modules

Output Format:
1. Problem Analysis: [what we're solving]
2. Design Options: [alternatives considered]
3. Recommendation: [chosen approach with rationale]
4. Implementation Plan: [how to build it]
5. Migration Strategy: [if replacing existing]
```

**Use Cases**:
- Planning new features
- Evaluating architectural decisions
- Designing new modules
- System-wide refactoring

### Mode Switching Strategy

**Workflow Example**:

1. **Start in Architecture Mode**
   ```
   (Architecture Mode)
   "Design a new notification system for our app"
   → Get architectural proposal
   ```

2. **Switch to Implementation** (Regular Chat or Agent)
   ```
   (Agent Mode)
   "Implement the notification system as designed"
   → Execute implementation
   ```

3. **Switch to Testing Mode**
   ```
   (Testing Mode)
   "Add comprehensive tests for the notification system"
   → Generate test suite
   ```

4. **Switch to Debugging Mode** (if issues arise)
   ```
   (Debugging Mode)
   "Why are notifications not being sent?"
   → Investigate and fix
   ```

### Creating Custom Modes in Cursor

**Steps**:
1. Settings → Cursor → Modes
2. Click "New Mode"
3. Name your mode (e.g., "Debugging")
4. Add mode-specific instructions
5. Configure tools and context preferences
6. Save and test

**Exercise**:
1. Create all 4 modes (Debugging, Testing, Refactoring, Architecture)
2. Test each mode with appropriate tasks
3. Refine mode instructions based on results
4. Document when to use each mode

---

## 3.2 Memories & Personalization

### Understanding Memories

**Memories** allow Cursor to remember facts from conversations and apply them automatically in future sessions.

**Types of Memories**:
1. **Global Memories**: Apply across all projects
2. **Project Memories**: Specific to current codebase
3. **Session Memories**: Temporary for current conversation

### Memory Strategy

#### Personal Coding Preferences

**Examples**:
- "I prefer async/await over Promises.then()"
- "Use TypeScript strict mode"
- "Always use const unless reassignment needed"
- "Prefer named exports over default exports"
- "Use 2 spaces for indentation, not tabs"

**How to Create**:
- Cursor can automatically create memories from your preferences
- Or manually add: Chat → "Remember that I prefer..."

#### Codebase-Specific Knowledge

**Examples**:
- "This codebase uses Redux for state management, not Context API"
- "Authentication is handled in src/auth/middleware.ts"
- "API errors are logged to Sentry, never console.error"
- "All database queries use the repository pattern"
- "Component tests use React Testing Library, not Enzyme"

**When to Create**:
- Important architectural decisions
- Common patterns in the codebase
- Gotchas that trip up developers
- Team conventions

#### Team Conventions

**Examples**:
- "Our team uses semantic commit messages"
- "Pull requests require 2 approvals"
- "We deploy on Fridays, avoid breaking changes on Thursday"
- "Use Jira ticket numbers in commit messages"

#### Personal Productivity Patterns

**Examples**:
- "I work on features in the morning, refactoring in the afternoon"
- "I prefer to review code changes before Agent applies them"
- "Always run tests before committing"

### Building Your Memory System

**Week 1: Core Preferences**
- [ ] Coding style preferences (5-10 memories)
- [ ] Editor preferences (2-3 memories)
- [ ] Workflow preferences (3-5 memories)

**Week 2: Project Knowledge**
- [ ] Architectural decisions (5-7 memories)
- [ ] Common patterns (5-7 memories)
- [ ] Gotchas and workarounds (3-5 memories)

**Week 3: Team Context**
- [ ] Team conventions (3-5 memories)
- [ ] Process preferences (2-3 memories)

**Week 4: Refinement**
- [ ] Review and update memories
- [ ] Remove outdated memories
- [ ] Consolidate overlapping memories

### Memory Best Practices

**Do**:
- ✅ Be specific: "Use TypeScript strict mode" not "use TypeScript properly"
- ✅ Include context: "In this project, use X because Y"
- ✅ Update regularly: Remove outdated memories
- ✅ Organize logically: Group related memories

**Don't**:
- ❌ Create conflicting memories
- ❌ Be too vague: "write good code"
- ❌ Over-memorize: Let some things be explicit in prompts
- ❌ Ignore memory conflicts: Resolve them

**Exercise**:
1. Create 10 memories covering:
   - 3 coding style preferences
   - 4 project-specific patterns
   - 2 team conventions
   - 1 workflow preference
2. Test by asking Cursor to implement something and verify it follows memories
3. Review and refine memories weekly

---

## 3.3 Advanced Prompt Engineering

### Structured Prompt Formula

**The Formula**:
```
Context: [What Cursor needs to know]
Goal: [Specific, measurable outcome]
Constraints: [What NOT to do, limits, guardrails]
Validation: [How to verify success]
Deliverable: [Format of output expected]
```

### Breaking Down Each Component

#### Context
**What to Include**:
- Relevant files (`@filename`)
- Related code snippets
- Current state or problem
- Background information
- Constraints from `.cursorrules` or project patterns

**Example**:
```
Context:
- Current implementation: @auth.service.ts (lines 45-60)
- Related types: @auth.types.ts
- Existing pattern: All services use dependency injection
- Current issue: Authentication is synchronous, needs to be async
```

#### Goal
**Characteristics of Good Goals**:
- Specific: "Add JWT token validation" not "improve auth"
- Measurable: "Reduce API response time by 50%" not "make it faster"
- Achievable: Realistic scope
- Relevant: Aligned with project needs

**Example**:
```
Goal:
- Convert authentication service to async/await pattern
- Add JWT token validation before processing requests
- Maintain backward compatibility with existing API calls
- Complete in auth.service.ts and auth.middleware.ts only
```

#### Constraints
**Types of Constraints**:
- Scope: "Only modify these files"
- Style: "Follow existing patterns"
- Performance: "Must complete in <100ms"
- Compatibility: "Don't break existing APIs"
- Resources: "Don't add new dependencies"

**Example**:
```
Constraints:
- Do not modify the public API interface
- Maintain existing error handling patterns
- Do not add new npm packages
- Keep changes to auth.service.ts and auth.middleware.ts only
- Preserve all existing tests (update if needed, don't remove)
```

#### Validation
**Validation Methods**:
- Automated: "Run `make test`"
- Manual: "Verify X happens when Y"
- Code review: "Ensure it follows Z pattern"
- Performance: "Check response time is <X"

**Example**:
```
Validation:
- All existing tests pass: `make test`
- No new linting errors: `make lint`
- Manual test: Login flow works end-to-end
- Performance: Auth check adds <10ms latency
```

#### Deliverable
**Output Formats**:
- Code changes: "Implement X in file Y"
- Documentation: "Create README explaining Z"
- Tests: "Add test suite covering A, B, C"
- Analysis: "Report on X with recommendations"

**Example**:
```
Deliverable:
- Updated auth.service.ts with async methods
- Updated auth.middleware.ts with JWT validation
- Brief summary of changes (1 paragraph)
- Updated test file if needed
```

### Complete Example

**Full Structured Prompt**:
```
Context:
@auth.service.ts @auth.middleware.ts @auth.types.ts
Current authentication uses synchronous calls. We need to switch to async
to support new JWT validation that requires database lookups.

Goal:
Convert authentication service to async/await pattern. Add JWT token
validation that checks token signature and expiration, plus verifies user
still exists in database. Maintain backward compatibility where possible.

Constraints:
- Only modify auth.service.ts and auth.middleware.ts
- Do not change public method signatures (use overloads if needed)
- Follow existing error handling patterns (throw AuthError for failures)
- Do not add new npm packages (use existing jsonwebtoken library)
- All existing tests must still pass

Validation:
- Run `make test` - all auth tests pass
- Run `make lint` - no new errors
- Manual: Login, token refresh, and logout all work
- Performance: Auth check adds <15ms latency

Deliverable:
1. Updated auth.service.ts with async methods
2. Updated auth.middleware.ts with JWT validation
3. One-line summary of changes
4. Note any breaking changes (if any)
```

### Progressive Disclosure

**Technique**: Build complex prompts incrementally.

**Step 1: Broad Request**
```
"Add user authentication to the app"
```

**Step 2: Add Context**
```
@user.model.ts @api.routes.ts
"Add user authentication to the app. Use the existing User model."
```

**Step 3: Add Constraints**
```
"Add user authentication. Use the existing User model. Don't use external
auth libraries, implement JWT ourselves."
```

**Step 4: Add Validation**
```
"Add user authentication. Use User model. Implement JWT ourselves.
After implementation, run tests and verify login/logout work."
```

**Step 5: Add Specifics**
```
"Add user authentication with JWT. Use User model. Implement ourselves.
Include login, logout, token refresh endpoints. Add tests. Verify with
`make test`. Follow our existing API patterns."
```

### Error Recovery

**Diagnosing AI Mistakes**:

1. **Wrong Context?**
   - Symptom: AI makes changes to wrong files
   - Fix: Add more specific `@file` selectors, check `.cursorignore`

2. **Vague Instruction?**
   - Symptom: AI does something unexpected
   - Fix: Be more specific, add examples, use structured format

3. **Model Limitation?**
   - Symptom: AI can't understand complex requirement
   - Fix: Break into smaller steps, simplify requirement

4. **Conflicting Constraints?**
   - Symptom: AI seems confused or asks many questions
   - Fix: Review constraints for conflicts, clarify priorities

**Recovery Process**:
```
1. Identify what went wrong
2. Diagnose the cause (context/vague/limitation/conflict)
3. Adjust prompt accordingly
4. Iterate with targeted correction
```

**Example Recovery**:
```
# First attempt (too vague):
"Fix the authentication bug"

# AI asks: "What bug? What's the error?"

# Second attempt (more specific):
"The login endpoint returns 500 errors. Check @auth.controller.ts
and @auth.service.ts. Error log shows 'user is undefined'."

# AI suggests fix, but it's not quite right...

# Third attempt (corrective):
"The issue is in the JWT verification. The token payload doesn't
include the user ID. Update @auth.service.ts line 45 to extract
user ID from token.subject instead of token.userId."
```

**Exercise**:
1. Write 3 complex prompts using the structured formula
2. Practice progressive disclosure on one prompt
3. Intentionally create a vague prompt, then refine it based on AI responses
4. Practice error recovery: make a mistake, diagnose, and correct

---

## Deliverable Checklist

Before moving to Level 4, complete:

- [ ] Created 4 custom modes (Debugging, Testing, Refactoring, Architecture)
- [ ] Tested mode switching in a real workflow
- [ ] Built memory system with 10+ relevant memories
- [ ] Memories covering: coding style, project patterns, team conventions
- [ ] Written 3 complex prompts using structured formula
- [ ] Practiced progressive disclosure
- [ ] Successfully recovered from AI mistakes using diagnostic process
- [ ] Refined modes and memories based on usage

**Success Indicators**:
- You instinctively switch modes based on task type
- Cursor remembers and applies your preferences automatically
- Your prompts consistently produce desired results
- You can quickly diagnose and fix AI misunderstandings
- Your modes and memories save significant time

---

## Advanced Techniques

### Mode Combinations

Combine modes for complex workflows:
- Architecture → Refactoring → Testing
- Debugging → Testing → Refactoring

### Memory Templates

Create memory templates for new projects:
- Copy relevant memories to new project
- Adapt to project specifics
- Share with team

### Prompt Libraries

Beyond notepads, create:
- Prompt snippets for common patterns
- Reusable prompt components
- Team prompt standards

---

## Next Steps

Once Level 3 is complete, you're ready for Level 4: Mastery - First Principles Extension, where you'll leverage codebase-level intelligence, orchestrate complex workflows, and extend Cursor's capabilities.

