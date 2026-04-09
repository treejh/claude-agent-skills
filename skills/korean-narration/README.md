# korean-narration

Claude가 툴(Bash, Read, Edit, Write, Grep, Glob 등)을 실행할 때마다 지금 무엇을 하고 있는지 한국어로 한 줄 설명을 추가하는 스킬.

## 기능

모든 툴 호출 바로 아래에 의미 중심의 한국어 설명을 자동으로 추가.

```
Bash(git log ...)
→ PR 커밋 목록을 가져오는 중입니다.

Read(src/main/java/...)
→ 파일 내용을 읽는 중입니다.

Edit(build.gradle)
→ 의존성을 추가하는 중입니다.
```

## 설치

```bash
# 1. 레포 클론 (또는 이미 있다면 skip)
git clone https://github.com/treejh/ai-agent-skills.git ~/ai-agent-skills

# 2. 스킬 연결
ln -s ~/ai-agent-skills/skills/korean-narration ~/.claude/skills/korean-narration
```

## 적용 방법

스킬을 연결하면 Claude Code가 자동으로 인식해서 모든 툴 실행 시 적용.  
별도로 `/korean-narration` 을 호출할 필요 없이 항상 활성화됨.

또는 `CLAUDE.md`에 직접 명시:

```markdown
## 툴 실행 narration
Bash, Read, Edit 등 툴을 실행할 때마다 툴 호출 아래에 한국어로 한 줄 설명을 추가한다.
```
