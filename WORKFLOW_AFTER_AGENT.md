# Workflow: What to Do After An Agent Finishes

Quick guide for handling agent-generated changes.

## The 3-Step Review

### 1. Review the Changes

**In Cursor:**
```bash
# See what changed
git diff level-4-mastery-guide.md

# Or use Cursor's built-in diff view
# Click the file in the sidebar → view diff
```

**Look for:**
- ✅ Does it solve what you asked?
- ✅ Is the code quality good?
- ✅ Does it follow project patterns?
- ✅ Any obvious bugs or issues?

### 2. Test/Validate (if applicable)

**For code changes:**
```bash
make test
make lint
make typecheck
```

**For documentation:**
- Check links work
- Verify examples are correct
- Ensure formatting is consistent

### 3. Decide: Keep, Edit, or Discard

**Option A: Keep it** ✅
```bash
# Stage the changes
git add level-4-mastery-guide.md

# Commit
git commit -m "Add Git worktrees option to parallel development section"

# Push
git push
```

**Option B: Edit it** ✏️
```bash
# Make manual edits in Cursor
# Then commit normally
git add .
git commit -m "Refined agent changes: [describe]"
```

**Option C: Discard it** ❌
```bash
# Revert the changes
git restore level-4-mastery-guide.md
```

## When to Create a PR?

### Create a PR if:
- You want code review before merging to main
- Team requires PRs for all changes
- Changes are substantial or risky
- Working in a branch (not main)

### Skip the PR if:
- Small documentation fixes
- Personal/work-in-progress repo
- Already working directly on main
- You're the sole reviewer

### Your Current Situation

**You're on `main` branch** with modified files:
- `level-4-mastery-guide.md` (modified)
- Plus other untracked files

**Recommended workflow:**

**Option 1: Commit directly to main** (simplest)
```bash
# If this is your repo and changes are good
git add level-4-mastery-guide.md
git commit -m "Add Git worktrees section to level 4 guide"
git push
```

**Option 2: Create a PR** (more formal)
```bash
# Create a branch
git checkout -b docs/add-git-worktrees-section

# Stage and commit
git add level-4-mastery-guide.md
git commit -m "Add Git worktrees section to level 4 guide"

# Push branch
git push origin docs/add-git-worktrees-section

# Create PR on GitHub/GitLab
```

## Key Insight: Agent Changes ARE Your Changes

**Important:** Files modified by an agent aren't special. They're just files that you saved.

```bash
# Agent creates/modifies a file
# You review it
# You save it (or Cursor auto-saves)
# Now it's YOUR change in your working directory

# Git sees the same file whether you:
# - Typed it manually
# - Copied from Stack Overflow  
# - Generated with Cursor Agent
# - Generated with GPT-4 via API
```

**The file modification happens in your local repo** - the same as if you edited it yourself.

## Best Practice Workflow

### Typical Flow:

```bash
# 1. Agent finishes task
# ✓ Files are now in your working directory
# ✓ Modified files show in git status

# 2. You review in Cursor
# ✓ Look at the diff
# ✓ Check if it's what you wanted
# ✓ Maybe make small edits

# 3. You validate
# ✓ Run tests (if code change)
# ✓ Lint (if applicable)

# 4. You commit
# ✓ git add [files]
# ✓ git commit -m "Meaningful message"
# ✓ git push (or create PR)

# 5. Agent context is done
# ✓ Close agent chat if not needed
# ✓ Move on to next task
```

## Pro Tips

### Use Background Agents + Multiple Tabs
```bash
# While agent runs in background, work on something else
# Agent will notify when complete
# Review when convenient
```

### Leverage Git Worktrees
```bash
# Don't switch branches for each feature
# Use worktrees for true parallelism
# See GIT_WORKTREES.md for full guide
```

### Review Checklist
```
After agent completes, verify:
- [ ] Changes solve the problem
- [ ] Code follows project style
- [ ] Tests pass (if applicable)
- [ ] No breaking changes
- [ ] Documentation updated
- [ ] Git status is clean
```

## When Things Go Wrong

**Agent made bad changes:**
```bash
git restore [file]
# Ask agent to try again with more constraints
```

**Agent left files in weird state:**
```bash
git status
git diff
git restore .  # Nuke all changes
```

**Want to see what agent did step-by-step:**
- Agent Mode shows its plan in the chat
- Review the chat history to understand reasoning
- Use this to improve future prompts

---

**TL;DR:**
1. Review changes (git diff)
2. Test if needed (make test)
3. Commit or discard (your choice)
4. Create PR if your workflow requires it
5. Agent changes are just... changes. Treat them normally!

