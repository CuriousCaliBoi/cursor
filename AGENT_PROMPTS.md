# Agent Prompts for This Repository

This document provides prompts and guidelines for AI agents working in this Cursor best practices repository. Use these prompts to ensure consistent, high-quality contributions that align with the repository's educational mission.

## Repository Context

This repository teaches developers how to use Cursor (AI coding assistant) effectively. All content should:
- Be **practical and actionable** - developers should be able to apply lessons immediately
- Follow **progressive difficulty** - Level 1 (Foundation) → Level 4 (Mastery)
- Use **real-world examples** - avoid toy or abstract examples
- Be **copy-paste ready** - templates should work with minimal customization
- Maintain **consistency** - follow established patterns across all guides

## Core Principles for Agents

When working in this repository, always:

1. **Preserve the Educational Structure**
   - Maintain the progressive difficulty levels (1-4)
   - Keep sections consistent across guides
   - Ensure examples build on previous concepts

2. **Prioritize Practicality Over Theory**
   - Every example should be immediately applicable
   - Templates should require minimal customization
   - Show, don't just tell

3. **Maintain Consistency**
   - Follow naming conventions in examples
   - Use consistent formatting across guides
   - Keep language and tone uniform

4. **Test Examples**
   - Ensure code examples are syntactically correct
   - Verify commands work as written
   - Check that file paths make sense

## Specific Agent Prompts

### Prompt 1: Adding New Guide Content

```
Context:
This is a Cursor best practices repository. The [level-X-guide.md] file follows
a progressive structure: basics → intermediate → advanced → mastery.

Goal:
Add content about [topic] that:
- Fits the current level (foundation/intermediate/advanced/mastery)
- Includes practical examples with code snippets
- Provides exercises for hands-on practice
- Maintains consistency with existing sections
- Uses real-world, applicable scenarios

Constraints:
- Follow the existing section numbering (e.g., 3.1, 3.2, 3.3)
- Keep examples practical and immediately usable
- Match the writing style and tone of existing content
- Include both "what" and "why" explanations
- Add exercises that reinforce the concepts
- Update the "Deliverable Checklist" if adding major sections

Validation:
- Code examples are syntactically correct
- Commands match the Makefile.example patterns
- Examples use consistent naming conventions
- Content flows logically from previous sections
- Exercises are achievable and relevant

Deliverable:
- Updated guide file with new section
- Code examples that work as written
- At least one practical exercise
- Brief note on what level this targets
```

### Prompt 2: Updating Template Files

```
Context:
The [template file] (e.g., .cursorrules.example, CONTEXT.example.md) is a 
copy-paste ready template that developers will customize for their projects.

Goal:
[Update/improve/add to] the template to:
- Remain useful across different tech stacks where applicable
- Include clear placeholder text indicating what to customize
- Provide examples that illustrate best practices
- Keep comments and explanations helpful, not overwhelming

Constraints:
- Use [SPECIFY] or [specify: ...] format for placeholders
- Keep examples generic but realistic
- Don't include project-specific details
- Maintain the existing structure and organization
- Ensure all sections are actionable

Validation:
- Placeholders are clearly marked and obvious
- Examples compile/work as templates
- No hardcoded project-specific values
- Template is usable immediately after copy
- Comments explain "why" not just "what"

Deliverable:
- Updated template file
- Brief explanation of changes
- Notes on what developers should customize
```

### Prompt 3: Creating New Prompt Templates

```
Context:
The notepads/ folder contains reusable prompt templates that developers can
load into Cursor. These follow a structured format with clear sections.

Goal:
Create a new prompt template for [use case] that:
- Follows the established template structure
- Is immediately usable without customization
- Includes a complete example usage
- Covers edge cases and common variations
- Aligns with principles in thoughts.md

Constraints:
- Use the standard sections: Goal, Scope, Constraints, Given, Deliver
- Include an "Example Usage" section with filled-in example
- Keep placeholders in [brackets] for customization
- Make it specific enough to be useful, generic enough to reuse
- Align with the repository's principles (minimal diffs, test-first, etc.)

Validation:
- Template is complete and usable as-is
- Example demonstrates real-world usage
- Placeholders are clear and obvious
- Follows patterns from existing notepads/
- Works for common variations of the use case

Deliverable:
- New notepad file in notepads/ folder
- Clear filename indicating the use case
- Complete template with example
- Brief description in a comment header
```

### Prompt 4: Maintaining Consistency Across Files

```
Context:
This repository contains multiple guide files (level-1 through level-4),
template files, and example files. Consistency across all files is critical
for usability.

Goal:
[Review/update] content to ensure consistency:
- Terminology matches across all guides
- Code examples use similar patterns
- Section structures align where appropriate
- Examples build on each other logically
- File references are accurate

Constraints:
- Don't change content meaning, only style/formatting
- Preserve educational progression
- Keep examples practical and applicable
- Maintain backward compatibility with existing content
- Update cross-references if files change

Validation:
- Terminology is consistent (e.g., "Agent Mode" not "agent mode" or "agent mode")
- Code examples use similar patterns
- Section numbers and structure align
- Cross-references point to correct locations
- File paths in examples are consistent

Deliverable:
- List of inconsistencies found and fixed
- Updated files with consistent formatting
- Brief explanation of standardization decisions
```

### Prompt 5: Improving Examples

```
Context:
Examples in guides and templates should be immediately applicable and
realistic. They should demonstrate best practices, not just show syntax.

Goal:
Improve [specific example] to:
- Use realistic variable/function names
- Demonstrate actual use cases developers face
- Show both correct usage and common mistakes
- Include context that makes the example meaningful
- Be complete enough to work if copy-pasted

Constraints:
- Keep examples focused (don't show entire applications)
- Use consistent naming conventions across examples
- Include error handling where appropriate
- Show the "why" not just the "how"
- Match the difficulty level of the current guide section

Validation:
- Examples are syntactically correct
- Variable names are realistic (not `foo`, `bar`, `baz`)
- Context makes the example meaningful
- Examples demonstrate best practices
- Code would work if copy-pasted (with appropriate setup)

Deliverable:
- Improved example code
- Brief explanation of improvements
- Note on what lesson the example teaches
```

### Prompt 6: Adding Exercises

```
Context:
Each guide section should include hands-on exercises that reinforce concepts.
Exercises should be achievable, relevant, and build confidence.

Goal:
Add exercises for [section/topic] that:
- Reinforce the concepts just explained
- Are achievable for the target skill level
- Provide clear success criteria
- Build on previous exercises where applicable
- Can be completed in reasonable time (10-60 minutes)

Constraints:
- Provide clear instructions
- Include success indicators
- Make exercises relevant to real work
- Build from simple to complex
- Don't require extensive setup

Validation:
- Exercises are achievable for the target level
- Instructions are clear and unambiguous
- Success criteria are measurable
- Exercises reinforce key concepts
- Time estimates are reasonable

Deliverable:
- Exercise description with clear instructions
- Success criteria/indicators
- Estimated completion time
- Optional: sample solution or hints
```

### Prompt 7: Refactoring for Clarity

```
Context:
This is educational content. Clarity and readability are paramount. Sometimes
content needs refactoring to improve understanding without changing meaning.

Goal:
Refactor [section] to improve clarity by:
- Simplifying complex explanations
- Breaking long paragraphs into shorter ones
- Using bullet points for lists
- Adding code examples where concepts are abstract
- Improving transitions between ideas

Constraints:
- Don't change the meaning or remove important information
- Maintain the educational progression
- Keep practical focus
- Preserve code examples (improve if needed, don't remove)
- Maintain existing structure where possible

Validation:
- Content is easier to understand
- Key concepts are still covered
- Examples still work
- Flow is logical and smooth
- No information was lost

Deliverable:
- Refactored section
- Brief explanation of clarity improvements
- Confirmation that all key points remain
```

### Prompt 8: Cross-Referencing and Navigation

```
Context:
The repository has multiple guide files that build on each other. Clear
navigation and cross-references help readers progress through levels.

Goal:
[Add/update] cross-references to:
- Link related concepts across guides
- Point to prerequisites in earlier levels
- Reference templates and examples
- Create clear learning path
- Help readers navigate the repository

Constraints:
- Use relative paths for markdown links
- Keep descriptions concise
- Only link when genuinely helpful
- Update links if file structure changes
- Test all links work

Validation:
- Links are accurate and work
- Cross-references are helpful, not distracting
- Navigation path is clear
- Related concepts are connected
- Prerequisites are obvious

Deliverable:
- Updated files with cross-references
- Brief map of navigation structure
- Confirmation all links work
```

## Quality Checklist for All Changes

Before submitting any changes, verify:

- [ ] **Practicality**: Can a developer apply this immediately?
- [ ] **Consistency**: Matches existing patterns and style?
- [ ] **Accuracy**: Examples and commands work as written?
- [ ] **Clarity**: Easy to understand for target skill level?
- [ ] **Completeness**: All necessary context provided?
- [ ] **Structure**: Follows existing organization patterns?
- [ ] **Progression**: Appropriate for the difficulty level?
- [ ] **Testing**: Examples have been verified to work?

## Common Patterns

### Naming Conventions in Examples
- Use realistic names: `userService`, `authMiddleware`, `paymentProcessor`
- Avoid: `foo`, `bar`, `baz`, `example`, `test123`
- Be consistent: if using camelCase in one example, use it throughout

### Code Examples
- Always include relevant context
- Show imports where needed
- Include error handling for realistic examples
- Add comments explaining non-obvious parts
- Use complete, runnable snippets when possible

### Command Examples
- Use `make` commands matching Makefile.example
- Include expected output for validation commands
- Show both success and error cases where relevant
- Provide alternatives for different stacks when applicable

### Template Placeholders
- Use `[SPECIFY]` for required customization
- Use `[specify: option1, option2]` for choices
- Use `[optional: description]` for optional fields
- Keep placeholder text clear and actionable

## Anti-Patterns to Avoid

❌ **Abstract Examples**: "Here's a function that does something..."
✅ **Concrete Examples**: "Here's a function that validates JWT tokens..."

❌ **Toy Projects**: "Create a todo app"
✅ **Real Scenarios**: "Add authentication to an existing API endpoint"

❌ **Incomplete Code**: Functions without imports or context
✅ **Complete Snippets**: Include imports, types, and context

❌ **Vague Instructions**: "Make it better"
✅ **Specific Guidance**: "Refactor to use async/await, add error handling"

❌ **Theoretical Explanations**: Long paragraphs without examples
✅ **Practical Demonstrations**: Show the code, then explain why

## Working with This Repository

### When Adding New Content
1. Identify the appropriate level (1-4)
2. Check existing content to avoid duplication
3. Ensure it builds on previous concepts
4. Include practical examples and exercises
5. Update checklists and cross-references

### When Updating Existing Content
1. Preserve the educational structure
2. Maintain consistency with related sections
3. Improve clarity without changing meaning
4. Update cross-references if structure changes
5. Verify examples still work

### When Creating Templates
1. Make them copy-paste ready
2. Use clear placeholder format
3. Include complete examples
4. Follow established patterns
5. Test that customization is obvious

## Quick Reference: File Purposes

- **level-1-foundation-guide.md**: Basics, Tab autocomplete, Chat basics, setup
- **level-2-intermediate-guide.md**: Agent Mode, Composer, Chat tabs, Notepads
- **level-3-advanced-guide.md**: Custom Modes, Memories, Advanced prompts
- **level-4-mastery-guide.md**: Advanced patterns (if exists)
- **.cursorrules.example**: Template for project-specific Cursor rules
- **CONTEXT.example.md**: Template for project context documentation
- **Makefile.example**: Template for standardized commands
- **thoughts.md**: Core principles and reusable prompt patterns
- **notepads/**: Reusable prompt templates for Cursor
- **AGENT_PROMPTS.md**: This file - guidelines for AI agents

## Success Indicators

You know you're doing well when:
- Developers can copy-paste examples and they work
- Content builds logically from simple to complex
- Examples use realistic, professional naming
- Templates require minimal customization
- Cross-references help navigation
- Exercises reinforce concepts effectively
- Consistency is maintained across all files

---

**Remember**: This repository exists to help developers ship faster with Cursor. Every change should serve that goal with practical, immediately applicable content.
