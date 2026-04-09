# cnotion

오늘 작업(git 커밋 + 세션 대화)을 분석해서 Notion DB에 엔지니어링 블로그 스타일로 업로드하는 스킬.

## 기능

- 오늘의 git 커밋을 분석해 카테고리별 Notion 페이지 생성
- 세션 대화에서 인사이트, 설계 결정, 트러블슈팅 내용 추출
- 엔지니어링 블로그 스타일 (왜→무엇→어떻게→효과 구조)
- `/cnotion analyze` — 세션 인사이트만 추출해서 별도 페이지 업로드

### 자동 생성 카테고리

| 태그 | 내용 |
|------|------|
| 기능 구현 | 새 기능, API, 로직 추가 |
| 트러블슈팅 | 버그 발견 → 근본 원인 → 해결 |
| 인프라 | CI/CD, Docker, GitHub Actions, AWS |
| 리팩토링 | 코드 구조 개선 |
| 인사이트 | 오늘 배운 것 (항상 생성) |
| 다음 과제 | 미해결 이슈, 다음 할 일 (항상 생성) |

## 사전 요구사항

- Claude Code (claude.ai/code 또는 CLI)
- [Notion MCP](https://github.com/anthropics/claude-code/blob/main/docs/mcp.md) 연결 및 인증 완료

## 설치

```bash
# 1. 레포 클론 (또는 이미 있다면 skip)
git clone https://github.com/treejh/ai-agent-skills.git ~/ai-agent-skills

# 2. 스킬 연결
ln -s ~/ai-agent-skills/skills/cnotion ~/.claude/skills/cnotion
```

## Notion DB 설정

### 1. Notion DB 만들기

아래 스키마로 Notion Database를 생성:

| 필드 | 타입 | 비고 |
|------|------|------|
| 내용 | title | 작업 주제 |
| 제목 | text | 한 줄 요약 |
| 날짜 | date | 작업 날짜 |
| 태그 | multi_select | 기능 구현 / 트러블슈팅 / 인프라 / 리팩토링 / 인사이트 / 다음 과제 |

### 2. SKILL.md에 ID 입력

`SKILL.md`의 `Notion DB Info` 섹션에서 아래 값을 본인 DB로 교체:

```
- DB page: https://www.notion.so/<YOUR_DB_PAGE_ID>
- DB parent page ID: <YOUR_PARENT_PAGE_ID>
- Data Source ID: collection://<YOUR_COLLECTION_ID>
```

**ID 찾는 방법:**
- `<YOUR_DB_PAGE_ID>`: Notion DB 페이지 URL에서 마지막 32자리
- `<YOUR_PARENT_PAGE_ID>`: Notion API로 DB 조회 시 `parent.page_id` 값
- `<YOUR_COLLECTION_ID>`: Notion API로 DB 조회 시 collection ID

## 사용법

Claude Code 세션에서:

```
/cnotion
```

오늘 작업한 프로젝트 디렉토리에서 실행하면 git 커밋 + 세션 대화를 분석해 Notion에 업로드.

```
/cnotion analyze
```

현재 세션 대화만 분석해서 인사이트 페이지 하나 생성.

## 출력 예시

```
[기능 구현] MDC roomCode 로깅 추가
[트러블슈팅] WebSocket 스레드 MDC 누락 원인 분석
[인사이트] ExecutorChannelInterceptor vs TaskDecorator 설계 판단
[다음 과제] 스테이징 배포 후 로그 검증 필요
```
