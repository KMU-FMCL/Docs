---
title: Status Code
tag: Python/FastAPI
---

## Status Code

기본적으로 FastAPI 는 `200` 상태 코드를 반환하지만 예외는 `4xx` 코드를 반환한다.

경로 데코레이터에서 모든 것이 정상으로 진행되면 반환해야 하는 HTTP 상태 코드를 지정한다.[^1]

[^1]: 예외는 자체 코드를 생성해 재정의한다.

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
