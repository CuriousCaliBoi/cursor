# Git Worktrees + Cursor Agents: The Master Workflow

## The Mental Model

**Git Worktrees** let you check out multiple branches of the same repository in different directories. Combined with Cursor Agents, this creates isolated, parallel development environments.

### Core Concept

Instead of:
- Switching branches (slow, loses context)
- Git stash/unstash (error-prone)
- Multiple clones (wasteful)

You:
- Keep multiple checked-out versions
- Work on different features simultaneously
- Let Cursor maintain separate context per directory
- No switching delays or context loss

## Quick Start

### Basic Setup

```bash
# Your main repo (already exists)
cd ~/projects/myapp

# Create a worktree for a new feature
git worktree add ../myapp-feature-auth feature/auth-system

# Now you have two directories:
# ~/projects/myapp (checkout of main branch)
# ~/projects/myapp-feature-auth (checkout of feature/auth-system)

# Work in the feature
cd ../myapp-feature-auth

# Create another worktree for a bugfix
git worktree add ../myapp-bugfix-1234 bugfix/issue-1234

# Now THREE parallel environments
```

### Cursor Integration

**Key Insight**: Cursor indexes each directory independently. Each worktree gets its own context.

**Setup per worktree**:
```bash
# In ~/projects/myapp-feature-auth
cp ../myapp/.cursorrules .
# Cursor automatically uses this directory's context

# Can use different .cursorrules per worktree if needed
cp ../myapp/.cursorrules.example .cursorrules
# Customize for this specific feature
```

**Why this works**:
- Cursor indexes by directory path
- Each worktree is a separate directory
- `.cursorrules`, `CONTEXT.md` per worktree = isolated context
- Agent Mode operates on the current directory's codebase

## The Master Workflow

### Scenario: Multiple Active Features

```bash
# Main development repo
~/projects/myapp/           # main branch

# Feature branches (parallel)
~/projects/myapp-auth/      # feature/auth-system  
~/projects/myapp-payments/  # feature/payment-flow
~/projects/myapp-ui/        # feature/new-dashboard

# Bugfix (urgent)
~/projects/myapp-hotfix/    # bugfix/critical-bug
```

**Your Day**:

**Morning** (9am):
```bash
# Open Cursor in auth worktree
cd ~/projects/myapp-auth
cursor .

# Start Agent Mode
# "Implement OAuth integration"
# Agent plans, executes, validates
```

**Mid-Morning** (10am - urgent bug):
```bash
# Switch to hotfix worktree (without leaving auth context open!)
cd ~/projects/myapp-hotfix
# Open new Cursor window (Cmd+N)
cursor .

# Load surgical-fix notepad
# Cursor has clean context for this bug
# Agent fixes quickly
```

**Afternoon** (1pm - back to auth):
```bash
# Return to original Cursor window
cd ~/projects/myapp-auth
# Your auth work is still there, unchanged
# Continue where you left off
```

**Key Benefit**: **Zero context switching overhead**. No stashing, no switching branches, no losing your place.

## Advanced Patterns

### Pattern 1: Feature + Bugfix Simultaneously

**Challenge**: Working on a feature when a critical bug appears.

**Without worktrees**:
```
1. Stash changes
2. Switch to main
3. Create bugfix branch
4. Fix bug
5. Switch back to feature
6. Unstash
7. Hope nothing broke
```

**With worktrees**:
```bash
# Feature already in progress
cd ~/projects/myapp-feature-auth
# Keep working...

# Bugfix (separate terminal/window)
git worktree add ../myapp-bugfix-1234 bugfix/issue-1234
cd ../myapp-bugfix-1234
# Fix bug with full Cursor context
# Submit PR

# Return to feature - nothing changed
```

### Pattern 2: Parallel Feature Development

**Setup**:
```bash
git worktree add ../myapp-feature-a feature/a
git worktree add ../myapp-feature-b feature/b
git worktree add ../myapp-feature-c feature/c
```

**Cursor Tab Strategy** (Level 2 technique):
- **Tab 1**: Feature A context (worktree A)
- **Tab 2**: Feature B context (worktree B)  
- **Tab 3**: Feature C context (worktree C)

**Agent Orchestration**:
- Each tab has Cursor with that worktree's context
- Agent Mode per tab runs independently
- No confusion between features
- Can work on all three in parallel

### Pattern 3: Release Preparation

```bash
# Main development
~/projects/myapp/           # main branch

# Current release being stabilized
~/projects/myapp-v2.0/      # release/v2.0

# Next release starting
~/projects/myapp-v2.1/      # develop branch
```

**Workflow**:
1. Fix critical bugs in v2.0 (release candidate)
2. Merge to main
3. Continue v2.1 development in separate worktree
4. No branch conflicts, clean context per worktree

### Pattern 4: PR Review + Development

```bash
# Your feature
~/projects/myapp-feature/   # feature/new-feature

# Review someone's PR (their branch)
git worktree add ../myapp-pr-review feature/their-feature
cd ../myapp-pr-review

# Load code-review notepad in Cursor
# Review with full context
# Comment on PR

# Return to your feature
cd ~/projects/myapp-feature
# Your work unchanged
```

## Cursor Agent Optimization

### Agent Mode + Worktrees

**Key Benefits**:

1. **Isolated Agent Context**
   ```
   Each worktree = separate codebase in Cursor's understanding
   Agent plans based on that worktree's files only
   No confusion from other branches
   ```

2. **Background Agents Per Worktree**
   ```
   Worktree A: Background Agent running tests
   Worktree B: Background Agent refactoring code
   Worktree C: Background Agent generating tests
   
   All running simultaneously, independently
   ```

3. **Composer Multi-File Edits**
   ```
   Cursor's @filename selectors work perfectly
   No branch conflicts to worry about
   Agent can modify multiple files safely
   ```

### Validation Per Worktree

**Each worktree can have different**:

```bash
# .cursorrules per worktree
~/projects/myapp-feature-auth/.cursorrules
  → "Auth-specific patterns and constraints"

~/projects/myapp-hotfix/.cursorrules  
  → "Minimal diff, surgical fixes only"
```

**Makefile targets work per worktree**:
```bash
cd ~/projects/myapp-feature-auth
make test   # Runs tests for this branch

cd ~/projects/myapp-hotfix
make test   # Runs tests for this branch
```

**Agent validation loops** (Level 2):
```
Agent in worktree A:
"After changes, run make test"

Agent in worktree B:
"After changes, run make lint && make typecheck"

Each worktree has independent validation
```

## Best Practices

### Directory Organization

**Recommended**:
```bash
# Base project
~/projects/myapp/

# Worktrees as siblings or in subdirectory
~/projects/myapp-auth/
~/projects/myapp-payments/
# OR
~/projects/worktrees/myapp-auth/
~/projects/worktrees/myapp-payments/
```

**Avoid**:
```bash
# Don't nest worktrees inside main repo
~/projects/myapp/auth/        # ❌ This will confuse Git
```

### Context Management

**Per Worktree**:
- `CONTEXT.md` - Current work context
- `.cursorrules` - Worktree-specific rules (optional)
- Makefile - Standardized commands

**Shared** (optional):
- `notepads/` - Common prompt templates (can symlink)
- Documentation - Usually shared

### Cleanup

**After merging PR**:
```bash
# Feature is merged, delete worktree
cd ~/projects/myapp
git worktree remove ../myapp-feature-auth

# Or if you already deleted the directory:
git worktree prune
```

**List all worktrees**:
```bash
git worktree list
```

**Remove stale worktrees**:
```bash
git worktree prune
```

### Security

**Per Worktree Environment**:
```bash
# Each worktree can have different .env files
~/projects/myapp-auth/.env          # Auth testing env
~/projects/myapp-payments/.env      # Payment testing env

# Cursor respects .gitignore per worktree
# Secrets won't leak between worktrees
```

## Real-World Example

**Monday Morning**:

```bash
# Three features to work on this week
git worktree add ../myapp-sso sso/implementation
git worktree add ../myapp-notifications notifications/email
git worktree add ../myapp-api-v2 api/version2
```

**Morning Session**:
```bash
cd ~/projects/myapp-sso
cursor .
# Cursor Tab 1: SSO implementation
# Agent Mode: "Implement SSO with Okta"
```

**Afternoon** (blocked on SSO, switch focus):
```bash
# New Cursor window (Cmd+N)
cd ~/projects/myapp-notifications
cursor .
# Cursor Tab 1: Email notifications
# Agent Mode: "Create email notification system"
```

**Evening** (SSO unblocked):
```bash
# Switch back to first window
cd ~/projects/myapp-sso
# Context is still there, continue work
```

**Tuesday** (unplanned bug):
```bash
cd ~/projects/myapp
git worktree add ../myapp-hotfix hotfix/critical
cd ../myapp-hotfix

# Load surgical-fix notepad
cursor .
# Quick fix with Agent
# Submit PR immediately
git worktree remove ../myapp-hotfix
```

**Wednesday** (continuing features):
```bash
# All three features still in progress
# Cursor context preserved
# No branch juggling
# Switch between worktrees instantly
```

## Common Workflows

### Daily Development Flow

```bash
# 1. Create worktree for day's work
git worktree add ../myapp-today feature/task-123

# 2. Open in Cursor
cd ../myapp-today
cursor .

# 3. Work with Agent Mode
# Use Level 2-4 techniques
# - Agent for multi-file changes
# - Composer for coordinated edits
# - Notepads for reusable patterns

# 4. Commit and push
git push origin feature/task-123

# 5. Create PR

# 6. Clean up after merge
cd ~/projects/myapp
git worktree remove ../myapp-today
```

### Experimental Branch Flow

```bash
# Try experimental idea
git worktree add ../myapp-experiment experimental/new-idea

cd ../myapp-experiment
# Experiment freely with Cursor Agent
# No risk to main work

# Keep if good, discard if not
cd ~/projects/myapp
git worktree remove ../myapp-experiment
# Or just rm -rf and prune
```

### Release Management Flow

```bash
# Stabilize release
git worktree add ../myapp-release release/v2.0

cd ../myapp-release
# Bug fixes only with Cursor
# Use surgical-fix notepad

# Continue developing in main worktree
cd ~/projects/myapp
# Development continues independently
```

## Mental Model Summary

**Think of worktrees as**:
- Separate "sandboxes" for each task
- Each with independent Cursor context
- Agent can work in parallel across worktrees
- Zero context-switching penalty

**Think of Cursor Agents as**:
- Operating within one worktree's context at a time
- Using that worktree's `.cursorrules`, `CONTEXT.md`
- Planning based on files in that worktree
- Validating with that worktree's tests

**Together they enable**:
- True parallel development
- No branch juggling
- Instant context switching
- Safer experimentation
- Better focus per task

## Integration with Level 2-4 Techniques

### Level 2: Chat Tabs + Worktrees

**Setup**: One tab per worktree
```
Tab 1: ~/myapp-auth/      → Auth feature
Tab 2: ~/myapp-payments/  → Payments feature
Tab 3: ~/myapp-bugfix/    → Bug investigation
```

### Level 2: Composer + Worktrees

**Per-worktree Composer sessions**:
```bash
cd ~/myapp-auth
# Composer (Cmd+I) for auth changes
# All @filename selectors relative to this worktree
```

### Level 3: Custom Modes + Worktrees

**Different modes per worktree**:
```
~/myapp-auth/        → Architecture Mode
~/myapp-bugfix/      → Debugging Mode  
~/myapp-refactor/    → Refactoring Mode
```

### Level 4: Codebase Queries + Worktrees

**Query per worktree context**:
```bash
cd ~/myapp-auth
# "Show me all integration points with payments"
# Cursor queries only this worktree's codebase
```

## Troubleshooting

**Problem**: Cursor confused between worktrees
**Solution**: Make sure each worktree is opened in separate Cursor window or clearly separated tabs

**Problem**: Changes in wrong worktree
**Solution**: Always verify you're in the correct directory (`pwd`)

**Problem**: Worktree directory deleted but Git still thinks it exists
**Solution**: `git worktree prune`

**Problem**: Can't create new worktree (branch already checked out)
**Solution**: Check existing worktrees with `git worktree list`

## Pro Tips

1. **Name worktrees descriptively**: `../myapp-feature-auth` not `../worktree-1`

2. **Use separate Cursor windows** for truly parallel work (Cmd+N on Mac)

3. **Symlink shared resources**: 
   ```bash
   ln -s ../../myapp/notepads notepads
   ```

4. **Track worktrees in team**:
   ```bash
   # Document active worktrees
   git worktree list > ACTIVE_WORKTREES.txt
   ```

5. **Clean up regularly**:
   ```bash
   # Weekly cleanup
   git worktree prune
   # Manually remove stale directories
   ```

## Exercise

**Goal**: Experience the power of parallel development

**Steps**:
1. Create two worktrees for different features
2. Open each in separate Cursor windows
3. Use Agent Mode in both simultaneously
4. Compare to traditional branch switching workflow
5. Measure time saved

**Success Criteria**:
- Can switch between features in <5 seconds
- No context loss when switching
- Cursor Agent works correctly in each worktree
- Can work on both features in same session

---

**Remember**: Worktrees + Cursor Agents = True parallel development without context switching overhead. Master this combination to ship faster.
