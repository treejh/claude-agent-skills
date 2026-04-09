# test-driven-development

테스트를 먼저 작성하고, 실패를 확인하고, 최소한의 코드로 통과시키는 TDD 워크플로우 스킬.

> 원본 출처: [obra/superpowers](https://github.com/obra/superpowers/tree/main/skills/test-driven-development)

## 기능

- Red → Green → Refactor 사이클 강제
- 테스트 없이 구현 코드 작성하지 않도록 가이드
- 안티패턴 감지 및 경고 (테스트 없는 구현, 테스트 실패 확인 생략 등)

## 설치

```bash
ln -s ~/ai-agent-skills/skills/test-driven-development ~/.claude/skills/test-driven-development
```

## 사용법

```
/test-driven-development
```

새 기능 구현이나 버그 수정 시, 코드 작성 전에 실행.

## TDD 사이클

```
1. 실패하는 테스트 작성
2. 테스트 실행 → 실패 확인 (이 단계 필수!)
3. 테스트를 통과하는 최소한의 코드 작성
4. 테스트 실행 → 통과 확인
5. 리팩토링 (필요하면)
6. 커밋
```

## 언제 사용하나

- 새 기능 추가
- 버그 수정
- 리팩토링
- writing-plans 스킬로 계획 수립 후 구현 단계에서 사용하면 효과적
