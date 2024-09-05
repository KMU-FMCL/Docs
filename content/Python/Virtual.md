---
title: Virtual Environment
---

## Virtual Environment

### 필요성

- **System Python** 설치에 영향을 주지 않고 **Package** 를 관리하기 위함

- **Project** 별 독립적인 **Python Environment** 를 만들기 위함

### 특징

- 특정 **Directory** 에 **Package** 를 설치하고 관리
- **Activate** 시 해당 **Environment** 의 **Package** 를 우선적으로 사용

### 장점

- 여러 **Version** 의 Python 사용 가능
- **Project** 별 **Package** 관리 용이
- 설치된 **Package** 의 명확한 파악 가능

### 생성 방법

- Python 3.4 이상에서는 `venv` Module 사용
- 독립 Program or **Python Module** 로 실행 가능

#### venv 독립 프로그램

```zsh
venv $name
```

#### venv Python Module

```zsh
python3 -m venv $name
```

#### Activate

```zsh
source $name/bin/activate
```

#### Deactivate

```zsh
deactivate
```

### 사용 시 주의사항

- **System Python File** 은 변경하지 말 것
- `pip` 는 기본적으로 **System Python** 에 영향을 주지 않음
