# writing-plans

코드를 작성하기 전에 구체적인 구현 계획을 문서로 작성하는 스킬.

> 원본 출처: [obra/superpowers](https://github.com/obra/superpowers/tree/main/skills/writing-plans)

## 기능

- 스펙이나 요구사항을 받아서 단계별 구현 계획 생성
- 각 태스크를 2-5분 단위 bite-sized step으로 분해
- 코드베이스 컨텍스트, 어떤 파일을 수정해야 하는지, 테스트 방법까지 문서화
- 계획 파일 저장 경로: `docs/plans/YYYY-MM-DD-<feature-name>.md`

## 설치

```bash
ln -s ~/ai-agent-skills/skills/writing-plans ~/.claude/skills/writing-plans
```

## 사용법

```
/writing-plans
```

요구사항이나 스펙을 가지고 있을 때, 코드 작성 전에 실행.  
Claude가 계획 문서를 생성한 후 구현을 시작함.

## 언제 사용하나

- 여러 파일을 수정해야 하는 중간 규모 이상의 태스크
- 새 기능 추가 시 설계를 먼저 정리하고 싶을 때
- test-driven-development 스킬과 함께 사용하면 효과적
