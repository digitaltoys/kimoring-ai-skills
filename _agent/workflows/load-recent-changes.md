---
description: 최근 변경 이력 및 커밋 로그를 확인하여 문맥을 파악합니다.
---

이 워크플로우는 프로젝트의 최근 변경 사항을 요약하여 보여줍니다.

// turbo
1. 최근 커밋 로그 확인
```bash
git log --oneline -10
```

2. 최근 변경된 파일 통계
```bash
git diff HEAD~5 --stat 2>/dev/null || git diff --stat
```

3. (선택) CHANGELOG 확인
```bash
cat docs/CHANGELOG.md | tail -n 20 2>/dev/null || echo "CHANGELOG.md 파일이 없습니다."
```
