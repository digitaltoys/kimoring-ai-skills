---
name: manage-skills
description: 세션 변경사항을 분석하여 검증 스킬 누락을 탐지합니다. 기존 스킬을 동적으로 탐색하고, 새 스킬을 생성하거나 기존 스킬을 업데이트한 뒤 README.md를 관리합니다.
disable-model-invocation: true
argument-hint: "[선택사항: 특정 스킬 이름 또는 집중할 영역]"
---

# 세션 기반 스킬 유지보수

## 목적

현재 세션에서 변경된 내용을 분석하여 검증 스킬의 드리프트를 탐지하고 수정합니다:

1. **커버리지 누락** — 어떤 verify 스킬에서도 참조하지 않는 변경된 파일
2. **유효하지 않은 참조** — 삭제되거나 이동된 파일을 참조하는 스킬
3. **누락된 검사** — 기존 검사에서 다루지 않는 새로운 패턴/규칙
4. **오래된 값** — 더 이상 일치하지 않는 설정값 또는 탐지 명령어

## 실행 시점

- 새로운 패턴이나 규칙을 도입하는 기능을 구현한 후
- 기존 verify 스킬을 수정하고 일관성을 점검하고 싶을 때
- PR 전에 verify 스킬이 변경된 영역을 커버하는지 확인할 때
- 검증 실행 시 예상했던 이슈를 놓쳤을 때
- 주기적으로 스킬을 코드베이스 변화에 맞춰 정렬할 때

## 등록된 검증 스킬

현재 프로젝트에 등록된 검증 스킬 목록입니다. 새 스킬 생성/삭제 시 이 목록을 업데이트합니다.

(아직 등록된 검증 스킬이 없습니다)

<!-- 스킬이 추가되면 아래 형식으로 등록:
| 스킬 | 설명 | 커버 파일 패턴 |
|------|------|---------------|
| `verify-example` | 예시 검증 | `src/example/**/*.ts` |
-->

## 워크플로우

### Step 1: 세션 변경사항 분석

현재 세션에서 변경된 모든 파일을 수집합니다:

```bash
# 커밋되지 않은 변경사항
git diff HEAD --name-only

# 현재 브랜치의 커밋 (main에서 분기된 경우)
git log --oneline main..HEAD 2>/dev/null

# main에서 분기된 이후의 모든 변경사항
git diff main...HEAD --name-only 2>/dev/null
```

### Step 2: 등록된 스킬과 변경 파일 매핑

위의 **등록된 검증 스킬** 섹션에 나열된 스킬을 참조하여 파일-스킬 매핑을 구축합니다.

#### Sub-step 2a: 등록된 스킬 확인

**등록된 검증 스킬** 테이블에서 각 스킬의 이름과 커버 파일 패턴을 읽습니다.

등록된 스킬이 0개인 경우, Step 4 (CREATE vs UPDATE 결정)로 바로 이동합니다. 모든 변경 파일이 "UNCOVERED"로 처리됩니다.

등록된 스킬이 1개 이상인 경우, 각 스킬의 `_agent/skills/verify-<name>/SKILL.md`를 읽고 파일 경로 패턴을 추출합니다.

### Step 6: 새 스킬 생성

새로 생성할 각 스킬에 대해:

1. **탐색** — 관련 변경 파일을 읽어 패턴을 깊이 이해합니다

2. **생성** — `_agent/skills/verify-<name>/SKILL.md`를 다음 템플릿에 따라 생성합니다.

3. **연관 스킬 파일 업데이트** — 새 스킬 생성 후 반드시 아래 3개 파일을 업데이트합니다:

   **4a. 이 파일 자체 (`_agent/skills/manage-skills/SKILL.md`) 업데이트**
   **4b. `_agent/skills/verify-implementation/SKILL.md` 업데이트**
   **4c. `README.md` 업데이트**

## Related Files

| File | Purpose |
|------|---------|
| `_agent/skills/verify-implementation/SKILL.md` | 통합 검증 스킬 |
| `_agent/skills/manage-skills/SKILL.md` | 이 파일 자체 |
| `README.md` | 프로젝트 지침 및 스킬 목록 유지 |
