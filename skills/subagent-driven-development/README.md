# subagent-driven-development

독립적인 태스크들을 여러 서브에이전트에게 병렬로 위임해서 구현하는 스킬.

> 원본 출처: [obra/superpowers](https://github.com/obra/superpowers/tree/main/skills/subagent-driven-development)

## 기능

- 구현 계획의 독립 태스크를 서브에이전트에게 분배
- 각 에이전트에게 명확한 스펙, 컨텍스트, 완료 기준 전달
- 구현 완료 후 코드 품질 검토 에이전트 실행
- Git 안전 규칙 적용 (명시적 요청 없이 push/merge 금지)

## 포함 파일

| 파일 | 설명 |
|------|------|
| `SKILL.md` | 메인 스킬 정의 |
| `implementer-prompt.md` | 구현 에이전트 프롬프트 템플릿 |
| `spec-reviewer-prompt.md` | 스펙 검토 에이전트 프롬프트 |
| `code-quality-reviewer-prompt.md` | 코드 품질 검토 에이전트 프롬프트 |

## 설치

```bash
ln -s ~/ai-agent-skills/skills/subagent-driven-development ~/.claude/skills/subagent-driven-development
```

## 사용법

```
/subagent-driven-development
```

`writing-plans`로 계획을 수립한 후, 독립적으로 실행 가능한 태스크가 여러 개 있을 때 사용.

## 추천 워크플로우

```
1. /writing-plans       → 구현 계획 수립
2. /subagent-driven-development  → 독립 태스크 병렬 구현
3. /test-driven-development      → 각 태스크 TDD로 구현
```
