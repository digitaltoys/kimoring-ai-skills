---
description: 세션 종료 시 변경사항을 스테이징하고 임시 커밋을 생성합니다.
---

이 워크플로우는 현재 세션의 모든 변경사항을 `WIP` 커밋으로 저장합니다.

// turbo
1. 모든 변경사항 스테이징 및 커밋 생성
```bash
git add -A
FILE_COUNT=$(git diff --cached --name-only | wc -l | tr -d ' ')
if [ $FILE_COUNT -gt 0 ]; then
  git commit -m "wip: update $FILE_COUNT files (auto-commit)" --no-verify
  echo "✅ $FILE_COUNT 개의 파일이 WIP 커밋되었습니다."
else
  echo "이미 모든 변경사항이 커밋되어 있습니다."
fi
```

2. 변경 이력 확인
```bash
git log --oneline -3
```
