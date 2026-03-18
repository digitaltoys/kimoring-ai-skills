---
name: merge-worktree
description: Squash-merge the current worktree branch into the main branch (or a specified target). Analyzes git history and source code to craft a comprehensive commit message.
argument-hint: "[target-branch]"
disable-model-invocation: true
---

# Merge Worktree

Squash-merge the current worktree branch back into the target branch with a comprehensive, structured commit message.

## Instructions

Follow these phases exactly, in order. Do NOT skip phases.

### Phase 1: Validation
1. **Verify worktree**: Check if the current git directory is a worktree.
2. **Identify current branch**: Get the worktree branch name.
3. **Resolve target branch**: Detect default branch (main/master).
4. **Identify the original repo path**.
5. **Clean working tree**: Ensure no uncommitted changes.

### Phase 2: Research
1. **Commit history**: Run `git log --oneline <target>..HEAD`.
2. **File change summary**: Run `git diff <target>...HEAD --stat`.
3. **Full diff**: Run `git diff <target>...HEAD`.
4. **Read key files**: Understand the full context.
5. **Categorize changes**: Feature, Fix, Refactor, etc.

### Phase 5: Craft commit message
write the commit message following this **exact structure**:

```
<type>: <concise summary in imperative mood, under 72 chars, no period>

<2-4 sentence paragraph explaining what was done and WHY.>

Changes:
- <grouped bullet points of what changed>

Co-Authored-By: Antigravity AI <noreply@google.com>
```

---

## Related Files

| File | Purpose |
|------|---------|
| `_agent/skills/merge-worktree/SKILL.md` | 이 파일 자체 |
| `README.md` | 프로젝트 가이드 |
