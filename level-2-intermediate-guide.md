# Level 2 Intermediate: Workflow Optimization Guide

## 2.1 Agent Mode Mastery

### Understanding Agent Mode

Agent Mode delegates complex tasks to Cursor's AI, which can:
- Plan the implementation
- Make changes across multiple files
- Run terminal commands
- Validate changes with tests
- Track dependencies between files
- Execute in the background

### Agent Task Scoping Formula

**Structure your requests as**:
```
Implement [specific feature/goal] in [location/scope] 
following [constraints/patterns]. 
Validate with [tests/checks/requirements].
```

**Examples**:

✅ **Good**:
```
Implement user authentication in src/auth/ following our JWT pattern.
Include login, logout, and token refresh endpoints.
Add unit tests for auth middleware.
Validate by running `make test`.
```

❌ **Bad**:
```
Add authentication
```

### Progressive Complexity

**Level 1: Single File Feature**
```
Implement a function to calculate user ratings in src/utils/ratings.ts.
Use the existing Rating type from types.ts.
Add JSDoc comments.
```

**Level 2: Multi-File Feature**
```
Implement email notifications for order confirmations.
- Create email templates in src/templates/
- Add email service in src/services/email.ts
- Integrate with existing order service
- Use the SMTP config from .env
```

**Level 3: Full Feature with Testing**
```
Implement password reset flow:
- Add endpoints: /auth/reset-request and /auth/reset-confirm
- Create database migration for reset tokens
- Add email templates
- Write integration tests
- Follow our error handling patterns
```

### Background Agent Usage

**When to use Background Agent**:
- Large refactors (100+ lines across multiple files)
- Generating comprehensive test suites
- Batch changes (updating all API calls, renaming patterns)
- Long-running tasks you want to monitor

**How to Use**:
1. Start Agent Mode in Chat
2. Give the task
3. When prompted, choose "Run in Background"
4. Continue working in other tabs
5. Monitor progress in the Background Agent panel

**Example**:
```
Agent, run in background:
Generate unit tests for all functions in src/utils/.
Follow our Jest patterns. Target 80% coverage.
Report when complete.
```

### Agent Validation Loops

**Set up automatic validation** so Agent checks its work:

**In `.cursorrules`**:
```
After making changes, always run:
1. `make typecheck` to verify types
2. `make lint` to check style
3. `make test` to verify functionality

If any fail, fix the issues before reporting completion.
```

**In your prompts**:
```
Implement feature X. After completion, run `make test` and `make lint`.
If errors occur, fix them and re-validate.
```

**Exercise**:
1. Create a simple feature request for Agent
2. Include validation steps in your prompt
3. Observe Agent running validation
4. Review Agent's changes before accepting

---

## 2.2 Composer & Multi-File Editing

### Composer Basics (Cmd+I)

**Composer** is Cursor's multi-file editing mode that maintains context across files.

**When to use Composer**:
- Coordinated changes across 3+ files
- Refactoring a pattern used in multiple places
- Implementing features that span components/services/tests
- Ensuring consistency across related changes

### Strategic Context Loading

**Use File Selectors (`@filename`)**:
```
@api.ts @types.ts
Update the User API to include email verification status.
Update the User type accordingly.
```

**Context Rules**:

✅ **Include**:
- Files you're directly modifying
- Related type definitions
- Test files for those modules
- Configuration files that affect behavior
- Documentation you're updating

❌ **Exclude**:
- Unrelated modules
- Generated code
- Vendor dependencies
- Large data files
- Files in `.cursorignore`

**Example Session**:
```
# Composer (Cmd+I)

Update the authentication system to support OAuth:
@auth.service.ts @auth.types.ts @auth.test.ts @config.ts

Changes needed:
1. Add OAuth providers (Google, GitHub) to types
2. Implement OAuth flow in service
3. Update tests
4. Add OAuth config to config.ts

Follow existing JWT patterns for consistency.
```

### Composer Workflows

**Complex Feature Development**:

**Session 1: Define Interfaces**
```
@types.ts @interfaces.ts
Define types and interfaces for the new payment system:
- PaymentMethod interface
- Transaction type
- PaymentStatus enum
```

**Session 2: Implement Core Logic**
```
@payment.service.ts @payment.repository.ts
Implement payment processing using the types from Session 1.
Include error handling following our patterns.
```

**Session 3: Add Tests & Integration**
```
@payment.test.ts @payment.controller.ts
Add comprehensive tests and API endpoints.
Integrate with existing order system.
```

**Exercise**:
Refactor a function used in 5 different files:
1. Use Composer with `@filename` selectors
2. Make coordinated changes
3. Ensure consistency across all usages
4. Verify with tests

---

## 2.3 Chat Tabs & Parallel Workflows

### Tab Organization Strategy

**Separate Concerns**:

**Tab 1: Current Feature Work**
- Active development
- Feature-specific context
- Implementation questions

**Tab 2: Bug Investigation**
- Error analysis
- Debugging queries
- Stack trace investigation

**Tab 3: Architecture Questions**
- Design decisions
- Pattern exploration
- Codebase navigation

**Tab 4: Code Review**
- Reviewing generated code
- Refinement requests
- Optimization questions

### Context Preservation Per Tab

**Use `@file` mentions** to maintain context:
```
# Tab 1 (Feature Work)
@user.service.ts @user.controller.ts
Implement user profile update endpoint

# Tab 2 (Bug Investigation)  
@error.log @auth.middleware.ts
Why are we getting 401 errors for valid tokens?

# Tab 3 (Architecture)
@project-structure.md
How should we organize the new notification module?
```

**Benefits**:
- Each tab maintains its own context
- No confusion between different tasks
- Can reference previous tab conversations
- Parallel progress on multiple concerns

### Parallel Workflow Example

**Scenario**: Working on a feature while investigating a bug

**Tab 1**: Feature implementation
```
@order.service.ts
Add functionality to cancel orders with refund processing
```

**Tab 2**: Bug investigation (in parallel)
```
@payment.webhook.ts @error.log
Why are payment webhooks timing out?
```

**Tab 3**: Quick architecture question
```
@CONTEXT.md
Should the new notification service be a separate microservice?
```

**Exercise**:
1. Open 3 chat tabs
2. Assign different concerns to each
3. Work on them in parallel
4. Practice switching context between tabs

---

## 2.4 Notepads & Prompt Libraries

### Creating Reusable Notepads

**Notepads** are saved prompts you can reuse across projects and sessions.

### Essential Notepad Templates

#### 1. `surgical-fix.md`
```
Goal: Fix [specific issue] with minimal changes
Scope: Only touch [file(s)]. Do not change public APIs.
Constraints: 
- Minimal diff
- Preserve naming
- Keep existing style
- No unrelated changes

Given:
- Error: [paste error]
- Command to repro: [command]
- Relevant code: @[files]

Deliver:
- Brief reasoning (1-2 lines)
- The patch
- Validation steps
```

#### 2. `spec-to-code.md`
```
Spec:
- User story: [description]
- Acceptance criteria:
  1. [criterion]
  2. [criterion]
- Inputs/outputs: [examples]
- Non-goals: [what not to implement]
- Constraints: [limitations]

Request:
1. Propose file changes (list with one-line summaries)
2. Implement in small steps
3. Add/extend tests to cover acceptance criteria
4. Ask 1 clarifying question if ambiguity remains
```

#### 3. `refactor-safe.md`
```
Objective: Improve [readability/structure/performance] without changing behavior

Guardrails:
- Keep public APIs stable
- Retain all tests (update if needed, don't remove)
- Small, atomic commits
- Document behavior changes (if any)

Checklist:
- [ ] Identify seams to isolate
- [ ] Propose rename/move plan
- [ ] Apply changes incrementally
- [ ] Note risks and rollback plan
- [ ] Run full test suite

Approach:
[Specify: Extract function? Move to module? Simplify logic?]
```

#### 4. `test-first.md`
```
TDD Workflow: Write failing test, then implement

Feature: [description]

Step 1: Write failing test
- Test file: @[test-file]
- Test case: [what to test]
- Expected behavior: [description]

Step 2: Implement minimal fix
- Implementation file: @[source-file]
- Keep diff tight
- Make test pass

Step 3: Refactor (if needed)
- Improve implementation
- Keep tests passing

Validation:
- Run: `make test`
- Verify: [specific checks]
```

#### 5. `code-review.md`
```
Code Review Checklist for: [PR/Change Description]

Functionality:
- [ ] Does it solve the stated problem?
- [ ] Are edge cases handled?
- [ ] Error handling appropriate?

Code Quality:
- [ ] Follows project style guide
- [ ] No code duplication
- [ ] Appropriate abstractions
- [ ] Clear naming

Testing:
- [ ] Tests added/updated
- [ ] Coverage maintained/improved
- [ ] Integration tests if needed

Architecture:
- [ ] Fits existing patterns
- [ ] No breaking changes (or documented)
- [ ] Performance acceptable

Security:
- [ ] No sensitive data exposed
- [ ] Input validation
- [ ] Authentication/authorization if needed

Suggestions:
[Reviewer feedback]
```

### Notepad Composition

**Complex Task Workflow**:

1. **Load Context Notepad**
   - Loads project context
   - Sets up understanding

2. **Load Planning Notepad**
   - Creates implementation plan
   - Identifies files to modify

3. **Load Execution Notepad**
   - Implements changes
   - Follows plan

4. **Load Validation Notepad**
   - Runs tests
   - Checks quality gates

**Example**:
```
# Load in sequence:
1. Load: project-context.md (sets foundation)
2. Load: spec-to-code.md (creates plan)
3. Execute implementation
4. Load: code-review.md (validates output)
```

**Exercise**:
1. Create all 5 notepad templates
2. Save them in Cursor Notepads
3. Use each notepad for a real task
4. Practice composing multiple notepads for a complex feature

---

## Deliverable Checklist

Before moving to Level 3, complete:

- [ ] Successfully delegated 5 Agent tasks with validation loops
- [ ] Completed a feature spanning 5+ files using Composer
- [ ] Managed 3 parallel workflows using Chat Tabs
- [ ] Created library of 5 reusable notepad templates
- [ ] Used notepad composition for a complex task
- [ ] Mastered file selectors (`@filename`) in Composer
- [ ] Used Background Agent for a long-running task

**Success Indicators**:
- You instinctively use Agent Mode for multi-file tasks
- Composer feels natural for coordinated changes
- You manage multiple concerns simultaneously
- Your notepad library saves time on repetitive tasks
- You compose notepads for complex workflows

---

## Advanced Tips

### Agent Mode Pro Tips

1. **Break Down Large Tasks**: Instead of "implement entire feature," break into:
   - Phase 1: Setup and types
   - Phase 2: Core logic
   - Phase 3: Integration
   - Phase 4: Tests

2. **Use Agent for Exploration**: "Analyze this codebase and identify refactoring opportunities"

3. **Set Expectations**: "This should take ~100 lines, focus on X, don't worry about Y"

### Composer Pro Tips

1. **Iterative Refinement**: Start broad, then narrow context
2. **Use Comments**: Add comments in Composer to guide AI reasoning
3. **Chain Sessions**: Build complexity across sessions

### Chat Tabs Pro Tips

1. **Name Your Tabs**: Use descriptive names (Cmd+Click on tab)
2. **Pin Important Context**: Use `@file` to pin frequently-referenced files
3. **Export Conversations**: Save valuable exchanges for future reference

---

## Next Steps

Once Level 2 is complete, you're ready for Level 3: Advanced Pattern Recognition & Automation, where you'll create custom modes, build memory systems, and master advanced prompt engineering.

