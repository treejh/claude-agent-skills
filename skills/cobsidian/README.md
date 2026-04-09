# cobsidian

오늘 작업(git 커밋 + 세션 대화)을 분석해서 `~/devlog/` 로컬 디렉토리에 카테고리별 마크다운 파일로 저장하는 스킬.  
Notion 연동 없이 로컬에 엔지니어링 데브로그를 쌓고 싶을 때 사용. [Obsidian](https://obsidian.md) vault와 연동하기 좋음.

## 기능

- 오늘의 git 커밋을 분석해 카테고리별 마크다운 파일 생성
- 세션 대화에서 인사이트, 설계 결정, 트러블슈팅 내용 추출
- 엔지니어링 블로그 스타일 (왜→무엇→어떻게→효과 구조)
- 저장 경로: `~/devlog/{repo-name}/{YYYY-MM-DD}/`

### 자동 생성 파일

| 파일명 | 내용 |
|--------|------|
| `기능구현-{제목}.md` | 새 기능 구현 내용 |
| `트러블슈팅-{제목}.md` | 버그 발견 → 근본 원인 → 해결 |
| `인프라-{제목}.md` | 인프라/배포 변경 |
| `리팩토링-{제목}.md` | 코드 구조 개선 |
| `인사이트.md` | 오늘 배운 것 (항상 생성) |
| `다음과제.md` | 미해결 이슈, 다음 할 일 (항상 생성) |

## 사전 요구사항

- Claude Code (claude.ai/code 또는 CLI)

## 설치

```bash
# 1. 레포 클론 (또는 이미 있다면 skip)
git clone https://github.com/treejh/ai-agent-skills.git ~/ai-agent-skills

# 2. 스킬 연결
ln -s ~/ai-agent-skills/skills/cobsidian ~/.claude/skills/cobsidian
```

## 설정

`SKILL.md`의 `Config` 섹션에서 본인 환경으로 교체:

```yaml
Author filter: <YOUR_NAME> / <YOUR_EMAIL>
Active projects:
  - /path/to/your/project1
  - /path/to/your/project2
```

- **Author filter**: `git log --format="%an %ae" -1` 로 확인 가능
- **Active projects**: 스케줄 실행 시 처리할 프로젝트 경로 목록

## 사용법

Claude Code 세션에서 작업한 프로젝트 디렉토리로 이동 후:

```
/cobsidian
```

오늘 git 커밋 + 세션 대화를 분석해서 `~/devlog/{repo-name}/{오늘날짜}/` 에 마크다운 파일 생성.

## 저장 구조 예시

```
~/devlog/
  my-backend/
    2025-01-15/
      트러블슈팅-MDC-roomCode-누락.md
      기능구현-게임시작-로그.md
      인사이트.md
      다음과제.md
```

## Obsidian 연동

Obsidian vault 루트를 `~/devlog/`로 설정하면 자동으로 모든 데브로그가 Obsidian에서 열림.

```
Settings → Vault → Open folder as vault → ~/devlog
```
