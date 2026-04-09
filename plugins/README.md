# Plugins

Claude Code 플러그인 모음. 스킬과 달리 여러 스킬/에이전트/커맨드를 하나로 묶은 패키지.

> 출처: [team-attention/plugins-for-claude-natives](https://github.com/team-attention/plugins-for-claude-natives)

---

## 스킬 vs 플러그인

| | 스킬 | 플러그인 |
|--|------|---------|
| 위치 | `~/.claude/skills/` | `~/.claude/plugins/` |
| 구성 | SKILL.md 단일 파일 | 스킬 + 에이전트 + 커맨드 묶음 |
| 설치 | 파일 복사/링크 | `/plugin install` 또는 직접 복사 |

**호출 방식은 동일** — SKILL.md의 `description`에 trigger 조건이 있어서 해당 상황이 되면 자동 활성화.

---

## 플러그인 목록

### 개발 워크플로우

| 플러그인 | 트리거 | 설명 |
|---------|--------|------|
| [clarify](clarify/) | "요구사항 명확히", "뭘 원하는 건지", `/clarify` | 모호한 요구사항을 구체적 스펙으로 정리 (3종 스킬) |
| [dev](dev/) | `/dev-scan` | 코드베이스 탐색 + 기술 결정 분석 멀티에이전트 |
| [doubt](doubt/) | 프롬프트에 `!rv` 추가 | Claude 응답을 강제로 재검증 |
| [session-wrap](session-wrap/) | "세션 마무리", "wrap up" | 세션 종료 시 5개 에이전트가 학습/자동화/문서 분석 |
| [interactive-review](interactive-review/) | `/review` | 마크다운 문서를 웹 UI로 인터랙티브 리뷰 |
| [agent-council](agent-council/) | `/agent-council` | Claude + Codex + Gemini에게 동시에 질문해서 의견 종합 |
| [team-assemble](team-assemble/) | `/team-assemble` | 태스크에 맞는 전문 에이전트 팀을 동적으로 구성 |

### 요구사항 분석 (clarify 세부)

| 스킬 | 트리거 | 설명 |
|------|--------|------|
| `clarify:vague` | "뭘 원하는 건지", "요구사항 정리" | 모호한 요청을 가설 기반 질문으로 구체화 |
| `clarify:unknown` | "뭘 모르는지 모르겠어", "전략 점검", "blind spots" | Known/Unknown 4분면으로 숨겨진 가정 발굴 |
| `clarify:metamedium` | "형식을 바꿔볼까", "다른 방법 없을까" | 내용(what) vs 형식(how) 관점 전환 |

### 외부 서비스 연동

| 플러그인 | 트리거 | 설명 |
|---------|--------|------|
| [gmail](gmail/) | "메일 확인", "이메일 보내줘" | Gmail 읽기/검색/전송 (멀티 계정) |
| [google-calendar](google-calendar/) | "오늘 일정", "미팅 추가해줘" | Google Calendar 조회/생성/수정 |
| [kakaotalk](kakaotalk/) | "카톡 보내줘", "채팅 읽어줘" | macOS 카카오톡 메시지 전송/읽기 |

### 콘텐츠 생성

| 플러그인 | 트리거 | 설명 |
|---------|--------|------|
| [youtube-digest](youtube-digest/) | "유튜브 정리", "영상 요약", YouTube URL 전달 | 영상 트랜스크립트 분석 → 요약/인사이트/퀴즈 생성 |
| [podcast](podcast/) | "팟캐스트 만들어줘", "이거 오디오로" | URL/기사/PDF → 한국어 팟캐스트 스크립트 + TTS + YouTube 업로드 |
| [say-summary](say-summary/) | 자동 (항상 활성화) | Claude 응답을 macOS TTS로 음성 요약 (한국어: Yuna, 영어: Samantha) |

---

## 설치

```bash
# 레포 클론 후 플러그인 디렉토리 연결
git clone https://github.com/treejh/ai-agent-skills.git ~/ai-agent-skills

# 원하는 플러그인만 선택해서 설치
cp -r ~/ai-agent-skills/plugins/clarify ~/.claude/plugins/clarify
cp -r ~/ai-agent-skills/plugins/session-wrap ~/.claude/plugins/session-wrap

# 또는 전체 설치
cp -r ~/ai-agent-skills/plugins/* ~/.claude/plugins/
```

---

## 추천 조합

### 개발 세션 기본 세트

```
doubt       ← 응답 재검증 (프롬프트에 !rv)
clarify     ← 요구사항 불명확할 때 자동 개입
session-wrap ← 세션 마무리 시 자동 분석
```

### 아이디어 → 구현 플로우

```
clarify:vague     ← 아이디어를 구체적 스펙으로
  ↓
clarify:unknown   ← 놓친 가정/리스크 발굴
  ↓
agent-council     ← Claude + Codex + Gemini 의견 수렴
  ↓
team-assemble     ← 구현 에이전트 팀 구성
```

### 학습/정리 플로우

```
youtube-digest  ← 강의/발표 영상 요약
  ↓
podcast         ← 내용을 팟캐스트로 변환
  ↓
say-summary     ← Claude 응답을 음성으로 확인
```
