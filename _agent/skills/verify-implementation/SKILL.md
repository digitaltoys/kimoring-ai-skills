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

### 2단계: 자동 검증 스킬 실행

아래 등록된 검증 전용 스킬들을 순차적으로 실행하여 각 항목의 합격 여부를 판단합니다.

- [ ] `verify-project-rules`: 한글 주석 사용 및 SOLID 설계 원칙 준수 여부 점검
- [ ] (추가 예정) `verify-api-specs`: API 엔드포인트 규격 및 연동 상태 점검

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
