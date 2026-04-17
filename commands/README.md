# Commands

Claude Code slash command 모음. `~/.claude/commands/`에 설치해서 `/커맨드명`으로 호출.

## 설치

```bash
# 전체 커맨드 설치
ln -s ~/ai-agent-skills/commands/ccm.md ~/.claude/commands/ccm.md
ln -s ~/ai-agent-skills/commands/cpr.md ~/.claude/commands/cpr.md
ln -s ~/ai-agent-skills/commands/code-review.md ~/.claude/commands/code-review.md
```

---

## ccm — Conventional Commit Manager

변경된 파일을 분석해서 기능 단위로 분리된 커밋을 생성하는 커맨드.

### 기능

- 변경 파일을 기능 단위로 자동 그룹화
- Conventional Commits 규칙으로 커밋 메시지 생성 (한국어)
- 브랜치명에서 이슈 번호 자동 추출 → `(#123)` 포함
- **커밋 계획을 먼저 보여주고 승인 후 실행** (실수 방지)

### 사용법

```
/ccm
```

`git add` 없이 실행하면 현재 변경사항을 분석해서 커밋 계획을 제안.

### 커밋 태그

| 태그 | 사용 시점 |
|------|----------|
| `feat:` | 새로운 기능 추가 |
| `fix:` | 버그 수정 |
| `refactor:` | 기능 변화 없이 리팩터링 |
| `chore:` | 패키지, 설정 파일 변경 |
| `docs:` | 문서/주석 수정 |
| `style:` | 코드 스타일, 포맷팅 |
| `release:` | 버전 릴리즈 |
| `merge:` | 브랜치 병합 |

### 출력 예시

```
=== 커밋 계획 ===

[커밋 1]
feat: 게임 종료 이벤트 로깅 추가 (#42)

[커밋 2]
fix: MDC roomCode 누락 수정 (#42)
- WebSocket 스레드에서 MDC 전파 안 되던 문제 해결

이대로 커밋을 진행할까요? (수정이 필요하면 말씀해 주세요)
```

---

## code-review — PR 자동 코드 리뷰

PR을 5개 병렬 에이전트가 독립적으로 검토하고, 신뢰도 80+ 이슈만 **한국어로** GitHub에 코멘트를 달아주는 커맨드.

> 원본: `code-review@claude-plugins-official` (Boris Cherny, Anthropic)  
> 커스텀: GitHub 코멘트를 한국어로 출력하도록 수정

### 기능

- 5개 에이전트 병렬 리뷰 (CLAUDE.md 준수, 버그, git 히스토리, 이전 PR 코멘트, 코드 주석)
- 각 이슈 0-100 신뢰도 채점 → 80 미만 자동 필터링
- 내 PR / 남의 PR 모두 가능
- Draft·Closed·이미 리뷰한 PR은 자동 스킵

### 사전 요구사항

- [GitHub CLI (`gh`)](https://cli.github.com/) 설치 및 로그인
- GitHub 저장소

### 사용법

```
/code-review          ← 현재 브랜치 PR 자동 감지
/code-review 123      ← PR 번호 지정
```

---

## cpr — Create Pull Request

현재 브랜치의 커밋을 분석해서 PR 설명을 한국어로 작성하고 실제 PR을 생성하는 커맨드.

### 기능

- `origin/develop` 기준으로 커밋 목록 및 diff 분석
- Conventional Commits 태그로 PR 제목 생성
- 변경 항목별 배경/이유/변경 내용 정리
- **PR 내용 확인 후 승인 받고 생성** (실수 방지)
- 브랜치명에서 이슈 번호 추출 → `resolved #123` 자동 추가

### 사전 요구사항

- [GitHub CLI (`gh`)](https://cli.github.com/) 설치 및 로그인
- 브랜치가 remote에 push된 상태

### 사용법

```
/cpr
```

### PR 본문 구조

```markdown
# PR

## PR 요약
전체 변경사항 2-3문장 요약

## 변경된 점

### 1. [변경 이름] (`관련 클래스`)
- **배경/이유**: 왜 이 변경이 필요했는지
- **변경 내용**: 구체적으로 무엇이 추가/변경되었는지

## 이슈 번호
resolved #42
```
