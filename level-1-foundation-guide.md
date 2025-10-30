# Level 1 Foundation: Core Competency Guide

## 1.1 Master the Fundamentals

### Tab Autocomplete Mastery

**What it is**: Cursor's Tab autocomplete predicts your next lines of code as you type, similar to GitHub Copilot but optimized for your codebase.

**When to use**:
- ✅ Writing boilerplate code (function signatures, class definitions)
- ✅ Following existing patterns in the codebase
- ✅ Completing obvious next steps (imports, error handling)
- ✅ Standard library operations

**When to ignore**:
- ❌ Tab suggestions are going in the wrong direction
- ❌ You need to think through complex logic yourself
- ❌ Tab is suggesting changes to unrelated code
- ❌ The suggestion conflicts with your architecture

**Practice Exercise**:
1. Open a file and start typing a function
2. Observe when Tab suggestions appear and are helpful
3. Notice when you instinctively ignore suggestions
4. Try accepting suggestions more often to build trust in the model

**Advanced Configuration**:
- Settings → Cursor → Autocomplete
  - Adjust suggestion delay (default: usually instant)
  - Configure model preferences
  - Set context window size

**Keyboard Shortcut**: `Tab` (accept) or `Esc` (ignore)

---

### Chat Basics

**Three Interaction Modes**:

#### 1. Inline Edit (`Cmd+K` on Mac, `Ctrl+K` on Windows/Linux)
- **Use for**: Small, focused changes (<10 lines)
- **Best for**: Renaming variables, fixing syntax errors, small refactors
- **How**: Select code, press `Cmd+K`, type instruction, accept/reject

**Example**:
1. Select: `const data = fetchData()`
2. Press `Cmd+K`
3. Type: "add error handling with try-catch"
4. Review and accept/reject

#### 2. Chat (`Cmd+L` on Mac, `Ctrl+L` on Windows/Linux)
- **Use for**: Medium-sized features, questions, explanations
- **Best for**: Understanding code, implementing features (1-3 files), debugging
- **How**: Open chat, type question/request, review response

**Example**:
- "Explain how the authentication middleware works"
- "Add a new API endpoint for user profiles"
- "Why is this component re-rendering unnecessarily?"

#### 3. Agent Mode (Cmd+Shift+A or via Chat)
- **Use for**: Large refactors, multi-file features, complex tasks
- **Best for**: Tasks spanning 5+ files, end-to-end features, background work
- **How**: Start chat, use `/agent` or say "use agent mode"

**Example**:
- "Implement user authentication system with JWT tokens"
- "Refactor all database queries to use the new repository pattern"
- "Migrate all components from class to function components"

**Decision Tree**:
```
Is it a single-line fix?
  Yes → Inline Edit (Cmd+K)

Is it 1-3 files and <100 lines?
  Yes → Chat (Cmd+L)

Is it multiple files or complex?
  Yes → Agent Mode
```

**Practice Exercise**:
Complete 10 small tasks using each mode:
- 3 tasks with Inline Edit
- 4 tasks with Chat
- 3 tasks with Agent Mode

---

### Codebase Indexing

**What it is**: Cursor builds an embedding of your codebase to understand context across files.

**Why it matters**: Better indexing = better AI understanding = better suggestions and responses.

**Setup Checklist**:

1. **Create `.cursorignore`**
   ```bash
   cp .cursorignore.example .cursorignore
   # Edit to exclude node_modules, dist, etc.
   ```

2. **Verify Indexing Status**
   - Settings → Cursor → Features
   - Check "Indexing" status
   - Ensure your project root is indexed

3. **Optimize Indexing**
   - Exclude large generated files
   - Exclude test fixtures that aren't code
   - Exclude vendor dependencies (they're in node_modules anyway)
   - Keep: Source code, tests, config files, docs

4. **Monitor Indexing**
   - Large codebases may take time
   - Check status indicator in status bar
   - Re-index if you notice poor context understanding

**Troubleshooting**:
- If AI suggests code that doesn't match your codebase style → re-index
- If context seems limited → check `.cursorignore` isn't too aggressive
- If indexing is slow → exclude more files, focus on source code

---

## 1.2 Project Configuration

### `.cursorrules` Deep Dive

**Purpose**: Teach Cursor your project's patterns, constraints, and preferences.

**Key Sections**:
1. **Project Overview**: Stack, frameworks, tools
2. **Architecture**: Patterns, boundaries, data flow
3. **Style**: Naming, formatting, conventions
4. **Safety**: Constraints, what not to do
5. **Validation**: How to verify changes

**Best Practices**:
- Start minimal, iterate as you discover patterns
- Be specific: "Use async/await, not Promises.then()" not "use modern JS"
- Include examples of preferred patterns
- Document "why" for important decisions
- Update as architecture evolves

**Example Evolution**:
```text
# Week 1: Basic
- Use TypeScript
- Follow Prettier config
- Write tests

# Week 4: Refined
- Use TypeScript with strict mode
- Follow Prettier config in .prettierrc
- Write tests using Jest, prefer describe/it pattern
- When creating API routes, include rate limiting
- Never mutate props in React components
```

**Exercise**:
1. Copy `.cursorrules.example` to your project
2. Fill in your stack and patterns
3. Add 3 project-specific rules
4. Test by asking Cursor to implement a feature and observe if it follows rules

---

### `CONTEXT.md` Creation

**Purpose**: Quick grounding document for Cursor (and humans) to understand the project.

**Template Location**: See `CONTEXT.example.md`

**Key Sections**:
1. **What This Project Does**: One paragraph summary
2. **Key Domains & Modules**: Core components and their locations
3. **How to Run**: Commands for setup, dev, test, deploy
4. **Architecture Highlights**: Design decisions, data flow
5. **Known Tricky Areas**: Gotchas and workarounds

**When to Update**:
- Major architectural changes
- New modules or integrations
- Discovered gotchas
- Changed deployment process

**Exercise**:
Create a `CONTEXT.md` for your project. Then ask Cursor:
- "Explain the architecture of this project"
- "How do I run the tests?"
- "What's the tricky part about authentication?"

Verify Cursor can answer using `CONTEXT.md`.

---

### Standardized Commands

**Purpose**: Make common operations discoverable to Cursor and consistent for your team.

**Options**:
1. **Makefile** (works on Unix/Mac, cross-platform with Make)
2. **justfile** (modern make alternative)
3. **package.json scripts** (for Node.js projects)
4. **Documentation** in README.md

**Required Commands**:
- `setup`: Install dependencies
- `run`: Start development server
- `test`: Run tests
- `lint`: Check code style
- `fmt`: Format code
- `typecheck`: Type checking
- `build`: Production build
- `deploy`: Deploy (optional)

**Why This Matters**:
- Cursor can run these commands automatically
- Agent Mode can validate changes with `make test`
- Consistency across team members
- Easier onboarding

**Exercise**:
1. Copy `Makefile.example` to your project (or create equivalent)
2. Customize for your stack
3. Test each command works
4. Ask Cursor: "Run the tests" and verify it uses your Makefile

---

## Deliverable Checklist

Before moving to Level 2, complete:

- [ ] Successfully used Tab autocomplete for 10 tasks
- [ ] Used Inline Edit (Cmd+K) for 3 small fixes
- [ ] Used Chat (Cmd+L) for 4 medium tasks
- [ ] Used Agent Mode for 3 complex tasks
- [ ] Created `.cursorignore` and verified indexing
- [ ] Created and customized `.cursorrules` for your project
- [ ] Created `CONTEXT.md` with project overview
- [ ] Set up standardized commands (Makefile or equivalent)
- [ ] Tested that Cursor understands your project context

**Success Indicators**:
- Cursor suggests code that matches your project's style
- Cursor can answer questions about your codebase architecture
- Cursor follows your `.cursorrules` constraints
- You instinctively choose the right interaction mode for each task

---

## Common Mistakes to Avoid

1. **Over-indexing**: Including too much in `.cursorignore` limits context
2. **Vague `.cursorrules`**: "Write good code" is useless; be specific
3. **Outdated `CONTEXT.md`**: Update when architecture changes
4. **Ignoring Tab suggestions**: Sometimes they're faster than typing
5. **Using wrong mode**: Chat for single-line fixes wastes time
6. **Not standardizing commands**: Cursor can't help if commands are inconsistent

---

## Next Steps

Once Level 1 is complete, you're ready for Level 2: Intermediate Workflow Optimization, where you'll learn to orchestrate multi-file changes, manage parallel workflows, and build reusable prompt libraries.

