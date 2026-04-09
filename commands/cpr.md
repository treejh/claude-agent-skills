---
allowed-tools: Bash(git log:*), Bash(git diff:*), Bash(git branch:*), Bash(git status:*), Bash(gh pr create:*), Bash(gh pr view:*)
description: 현재 브랜치의 push된 커밋을 분석해서 PR 설명을 한국어로 작성하고 실제 PR을 생성합니다
---

## Context

- 현재 브랜치: !`git branch --show-current`
- 베이스 브랜치(develop)와의 커밋 목록: !`git log origin/develop..HEAD --oneline`
- 커밋 상세 내용: !`git log origin/develop..HEAD --pretty=format:"%h %s" --name-status`
- 변경된 파일 diff 요약: !`git diff origin/develop...HEAD --stat`

## Your task

다음 순서로 진행합니다.

### 1단계: PR 제목 작성

제목 형식: `<tag>: <subject>`

커밋 내역을 분석해서 아래 태그 중 가장 적합한 것을 선택합니다.

| 태그 | 사용 시점 |
|------|----------|
| `feat` | 새로운 기능 추가, 기존 기능의 요구 사항에 맞춘 수정 |
| `fix` | 기능에 대한 버그 수정 |
| `chore` | 패키지 매니저 수정, 기타 변경 사항 (예: .gitignore 수정) |
| `docs` | 문서(주석) 수정 |
| `style` | 코드 스타일, 포맷팅에 대한 수정 (기능 변경 없음) |
| `refactor` | 기능 변화 없이 코드 리팩터링 (예: 변수 이름 변경) |
| `release` | 버전 릴리즈 |
| `merge` | 자신의 브랜치에 다른 브랜치(예: develop)를 병합할 때 |

예시: `feat: pending 상태 API 추가 및 GameEnd 조건 확장`

- subject는 한국어로 간결하게 작성
- 제목에는 이슈 번호를 포함하지 않는다

### 2단계: PR 본문 작성

아래 양식으로 PR 설명을 **한국어**로 작성합니다.

```
# PR

## PR 요약
(전체 변경사항을 2~3문장으로 요약. 왜 이 변경이 필요했는지 배경과 목적 중심으로 작성.
리팩토링이 아닌 기능/동작 변경에 집중하여 작성)

## 변경된 점

각 변경 항목은 아래 형식으로 작성:

### N. [변경 이름] (`관련 클래스`, `관련 클래스`)

기능을 모르는 사람도 이해할 수 있도록:
- **배경/이유**: 왜 이 변경이 필요했는지
- **변경 내용**: 구체적으로 무엇이 추가/변경되었는지
- 주요 메서드/API/엔드포인트가 있으면 코드 블록으로 명시
  ```
  SEND /app/example
  { "field": value }
  ```
- 조건 변화가 있으면 Before/After 표 또는 명확한 비교로 표현
  | 조건 | 이전 | 이후 |
  |------|------|------|
  | ... | ... | ... |

### N. [변경 이름] ...

(위 형식 반복)

규칙:
- 단순 파일 나열 금지 — 기능/동작/로직 중심으로 설명
- 리팩토링 성격의 내부 구조 변경은 생략하거나 최소화
- 핵심적으로 동작이 달라지는 부분만 선별하여 상세히 작성
- 주요 Spring/WebSocket/도메인 메서드나 엔드포인트는 반드시 명시

## 이슈 번호
resolved #(브랜치명에서 이슈 번호 추출)
```

### 3단계: 사용자 확인 후 PR 생성

작성한 제목과 본문을 사용자에게 먼저 보여주고, 확인을 받은 후 PR을 생성합니다.

사용자가 확인하면 아래 명령어로 PR을 생성합니다.

```bash
gh pr create \
  --base develop \
  --title "<작성한 제목>" \
  --body "<작성한 본문 전체>"
```

PR 생성 완료 후 PR URL을 출력합니다.
