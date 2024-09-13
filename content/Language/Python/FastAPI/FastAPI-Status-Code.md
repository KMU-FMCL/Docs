---
title: Status Code
tag: Python/FastAPI
---

## Status Code

### Default

- **Normal** : `200`
- **Exception** : `4xx`

### 지정 방법

- Path Decorator 에서 직접 지정 가능
- 모든 것이 정상일 때 Return 할 Code 명시
  - Exception 은 자체 Code 를 생성해 재정의

> [!Tip] HTTP Status Code
>
> > [!example] hello.py
> >
> > ```python
> > @app.get("/happy")
> > def happy(status_code=200):
> >     retrun ":)"
> > ```
>
> > [!check] HTTPie
> >
> > ```zsh
> > http localhost:8000/happy
> > ```
