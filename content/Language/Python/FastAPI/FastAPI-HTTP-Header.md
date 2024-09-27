---
title: Header
tag: Python/FastAPI
---

## Header

- [[./FastAPI]] 에서는 **HTTP Header** 를 Function Parameter 로 쉽게 받을 수 있음 <p style='margin-top: 0.25em; margin-bottom: 0.25em'></p>
- `Header()` Function 를 사용하여 Specific Header Value 를 Parameter 로 받을 수 있음
  - Ex) `greeting` Argument 를 **HTTP Header** 로 전달

### Example

> [!Tip] Custom
>
> > [!example] Return String Header
> >
> > ```python
> > from fastapi import FastAPI, Header
> >
> > app = FastAPI()
> >
> > @app.get("/hi")
> > def greet(who: str = Header()):
> >     return f"Hello? {who}?"
> > ```
>
> - HTTP Header **'Name:Value'** 형태로 지정
>
> > [!check] HTTPie
> >
> > ```zsh
> > http -v localhost:8000/hi who:Mom
> > ```

> [!Tip] User-Agent
>
> - [[./FastAPI]] 는 HTTP Header Key 를 lowercase & hyphen( **-** ) 을 underline( **\_** ) 으로 Conversion 함
>
>   - 따라서 HTTP `User-Agent` Header Value 출력 가능
>
> > [!example] Return User-Agent Header
> >
> > ```python
> > from fastapi import FastAPI, Header
> >
> > app = FastAPI()
> >
> > @app.get("/agent")
> > def greet(user_agent: str = Header()):
> >     return user_agent
> > ```
>
> > [!check] HTTPie
> >
> > ```zsh
> > http -v localhost:8000/agent
> > ```
