---
name: verify-implementation
description: 프로젝트의 모든 verify 스킬을 순차 실행하여 통합 검증 보고서를 생성합니다. 기능 구현 후, PR 전, 코드 리뷰 시 사용.
disable-model-invocation: true
argument-hint: "[선택사항: 특정 verify 스킬 이름]"
---

# 구현 검증

## 목적

프로젝트에 등록된 모든 `verify-*` 스킬을 순차적으로 실행하여 통합 검증을 수행합니다.

## 실행 대상 스킬

이 스킬이 순차 실행하는 검증 스킬 목록입니다. `manage-skills`가 스킬을 생성/삭제할 때 이 목록을 자동 업데이트합니다.

(아직 등록된 검증 스킬이 없습니다)

<!-- 스킬이 추가되면 아래 형식으로 등록:
| # | 스킬 | 설명 |
|---|------|------|
| 1 | `verify-example` | 예시 검증 설명 |
-->

## 워크플로우

### Step 1: 실행 대상 확인
`_agent/skills/` 내의 `verify-`로 시작하는 스킬들을 탐색합니다.

### Step 2: 순차 실행
각 스킬의 `SKILL.md`를 읽고 Workflow 섹션에 정의된 검사를 실행합니다.

---

## Related Files

| File | Purpose |
|------|---------|
| `_agent/skills/manage-skills/SKILL.md` | 스킬 유지보수 |
| `_agent/skills/verify-implementation/SKILL.md` | 이 파일 자체 |
| `README.md` | 프로젝트 지침 |
