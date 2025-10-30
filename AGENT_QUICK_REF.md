# Quick Reference: Agent Prompts for This Repo

Quick copy-paste prompts for common tasks in this Cursor best practices repository.

## Core Principle
Every change should make Cursor more practical and immediately usable for developers. Prioritize actionable content over theory.

## Template: Adding Guide Content

```
Add a section about [topic] to [level-X-guide.md]:

- Section number: [X.Y] (follow existing structure)
- Difficulty level: [Foundation/Intermediate/Advanced/Mastery]
- Include:
  * Practical explanation with "why" not just "how"
  * Real-world code examples (not foo/bar/baz)
  * At least one hands-on exercise
  * Success criteria for the exercise
  * Update deliverable checklist if major section

Constraints:
- Code examples must work if copy-pasted (with appropriate setup)
- Use consistent naming: camelCase for variables, PascalCase for classes
- Examples should demonstrate actual use cases developers face
- Maintain progression from previous sections
- Keep tone consistent with existing content

Validation:
- Example code compiles/runs
- Exercise is achievable for target level
- Cross-references are accurate
- Matches writing style of guide
```

## Template: Updating Templates

```
Update [template file] to [improvement]:

- Keep all placeholders in [SPECIFY] or [specify: options] format
- Ensure template is copy-paste ready after customization
- Add helpful comments explaining "why" where needed
- Maintain existing structure and organization
- Make placeholders obvious and actionable

Validation:
- Template works immediately after copy
- Placeholders are clearly marked
- No hardcoded project-specific values
- Examples illustrate best practices
```

## Template: Creating Prompt Notepads

```
Create a new notepad template in notepads/ for [use case]:

Structure:
- Goal (what to accomplish)
- Scope (what files/areas to touch)
- Constraints (what not to do)
- Given (required context)
- Deliver (expected output)
- Example Usage (filled-in example)

Requirements:
- Immediately usable without customization
- Includes complete, realistic example
- Aligns with principles from thoughts.md
- Specific enough to be useful, generic enough to reuse
- Filename clearly indicates use case

Validation:
- Template is complete as-is
- Example demonstrates real usage
- Placeholders are clear
- Follows patterns from existing notepads/
```

## Template: Fixing Inconsistencies

```
Review and fix inconsistencies across all guide files:

Focus on:
- Terminology (e.g., "Agent Mode" not "agent mode")
- Code example patterns (consistent naming, style)
- Section structure alignment
- Cross-reference accuracy
- File path examples

Constraints:
- Don't change content meaning, only style/formatting
- Preserve educational progression
- Update cross-references if structure changes
- Maintain backward compatibility

Deliverable:
- List of fixes made
- Updated files
- Brief explanation of standardization decisions
```

## Template: Improving Examples

```
Improve the example at [location] to be more practical:

Requirements:
- Use realistic names (userService, authMiddleware, not foo/bar)
- Include necessary context (imports, types)
- Show actual use cases developers face
- Demonstrate best practices, not just syntax
- Complete enough to work if copy-pasted

Constraints:
- Keep focused (don't show entire applications)
- Match difficulty level of current section
- Include error handling where realistic
- Show "why" not just "how"

Validation:
- Code is syntactically correct
- Names are professional and realistic
- Context makes example meaningful
- Demonstrates best practices
```

## Key Quality Checks

Before any change:
- [ ] Practical and immediately applicable?
- [ ] Consistent with existing patterns?
- [ ] Examples work as written?
- [ ] Clear for target skill level?
- [ ] Complete with all necessary context?
- [ ] Appropriate difficulty level?
- [ ] Follows repository structure?

## Anti-Patterns

❌ Abstract: "Here's a function that does something"
✅ Concrete: "Here's a function that validates JWT tokens"

❌ Toy: "Create a todo app"  
✅ Real: "Add authentication to existing API endpoint"

❌ Incomplete: Functions without imports
✅ Complete: Include imports, types, context

❌ Vague: "Make it better"
✅ Specific: "Refactor to async/await, add error handling"

## File Purposes

- `level-1-foundation-guide.md`: Basics, setup, core features
- `level-2-intermediate-guide.md`: Agent Mode, Composer, workflows
- `level-3-advanced-guide.md`: Custom modes, memories, prompts
- `level-4-mastery-guide.md`: Codebase intelligence, orchestration
- `.cursorrules.example`: Project-specific Cursor rules template
- `CONTEXT.example.md`: Project context documentation template
- `Makefile.example`: Standardized commands template
- `thoughts.md`: Core principles and prompt patterns
- `notepads/`: Reusable prompt templates
- `AGENT_PROMPTS.md`: Full agent guidelines (this is quick ref)

---

**Remember**: This repo helps developers ship faster with Cursor. Every change = more practical, immediately usable content.
