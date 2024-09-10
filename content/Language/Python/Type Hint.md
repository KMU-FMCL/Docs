---
title: Type Hint
tag: Language/Python
---

## Type Hint

### 도입

- Python 3.6 부터 Type Hint 기능이 Add

### 목적

- Variable 이 Reference 하는 Object 의 Type 을 선언하기 위함

### 특징

- 실행 중인 Python Interpreter 에 영향 X
- Variable 사용의 일관성 유지를 위한 Tool 로 활용
- `mypy` 같은 Standard Type 검사기와 함께 사용 가능

### 장점

- Programmer 의 실수 방지에 도움[^1]
- Code 의 가독성과 유지보수성 향상

### Caution

- 강제성이 없는 선택적 기능
- Lint Tool 과 유사하지만 예상치 못한 용도로도 사용 가능
- Code 의 품질을 높이는 데 도움을 주지만, &nbsp;Python 의 동작 특성을 해치지 않는 선에서 적절히 사용할 것

[^1]: Ex) <var>count: int</var> 와 같이 Variable 의 Type 을 명시할 수 있음
