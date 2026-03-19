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

### 단계 1: 준비 및 검증 (Validation)
1. **워크트리 확인**: 현재 디렉토리가 유효한 Git 워크트리인지 확인합니다.
2. **미커밋 변경 사항 처리**: **중요**: 워크트리 내부에서 `git add` 및 `git commit`을 먼저 수행하여 모든 작업 내용을 브랜치에 안전하게 기록합니다. 커밋되지 않은 작업 내용은 병합 시 유실될 수 있습니다.
3. **타겟 브랜치 확인**: 병합될 대상 브랜치(기본: main)를 확인합니다.

### 단계 2: 차이점 분석 (Research)
1. **커밋 이력 조회**: `git log --oneline main..HEAD`를 통해 변경 내역을 파악합니다.
2. **변경 통계 확인**: `git diff main...HEAD --stat`으로 수정된 파일 목록을 확인합니다.
3. **코드 상세 분석**: 주요 수정 파일의 내용을 직접 읽어 변경 취지를 완벽히 이해합니다.

### 단계 3: 병합 수행 (Merge)
1. **사용자 최종 확인**: **중요**: 병합을 진행하기 전, 변경 사항(`git diff`)을 사용자에게 보여주고 병합 승인을 반드시 요청합니다. 사용자의 명시적인 승인 없이는 병합을 진행하지 않습니다.
2. **메인 브랜치 이동**: 메인 폴더로 이동하여 `git checkout main`을 수행합니다.
3. **스쿼시 병합**: `git merge --squash <branch-name>`을 실행합니다.

### 단계 4: 결과 검증 및 최종 커밋 (Verification)
1. **파일 내용 확인**: **중요**: `read_file` 도구를 사용하여 병합된 주요 파일(예: 수정된 핵심 로직)의 내용이 실제로 반영되었는지 직접 확인합니다. "Already up to date" 메시지에만 의존하지 마십시오.
2. **최종 커밋**: 병합이 확인되면 한국어 템플릿에 맞춰 커밋을 수행합니다.

### 단계 5: 안전한 정리 (Cleanup)
1. **워크트리 삭제**: 모든 병합과 커밋이 완료된 것을 확인한 후 `git worktree remove`를 수행합니다. 데이터 유실 위험이 있으므로 병합 확인 전에는 `--force`를 사용하지 않습니다.
2. **브랜치 삭제**: `git branch -D`로 작업 브랜치를 정리합니다.

### 단계 5: 커밋 메시지 작성
다음 **정해진 구조**에 따라 한국어로 커밋 메시지를 작성하십시오:

```
<type>: <72자 이내의 간결한 요약, 마침표 없음>

<무엇을 왜 변경했는지 설명하는 2~4문장의 상세 설명.>

변경 사항:
- <그룹화된 변경 내용의 불렛 포인트>

Co-Authored-By: Antigravity AI <noreply@google.com>
```

---

## Related Files

| File | Purpose |
|------|---------|
| `_agent/skills/merge-worktree/SKILL.md` | 이 파일 자체 |
| `README.md` | 프로젝트 가이드 |
