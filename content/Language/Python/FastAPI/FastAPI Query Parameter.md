---
title: Query Parameter
tag: Language/Python/FastAPI
---

## Query Parameter

[[./FastAPI HTTP Request#FastAPI 의 HTTP Request 해석|URL]] 에서 **?** 뒤에 오는 `Name=Value` 형태의 문자열로, &nbsp;**&** 로 구분된다.

### Example

> [!example] Return String Query Parameter
>
> ```python
> from fastapi import FastAPI
>
> app = FastAPI()
>
> @app.get("/hi")
> def greet(who):
>     return f"Hello? {who}?"
> ```
>
> - Endpoint Function 는 `greet(String)` 로 정의 <p style='margin-top: 0.25em; margin-bottom: 0.25em'></p>
> - `@app.get("/hi/{String}")` 이 존재 X <p style='margin-top: 0.125em; margin-bottom: 0.125em'></p>
>   - <var>who</var> 가 Query Parameter 라고 가정

> [!check] Test
>
> > [!example] Browser
> >
> > > http://localhost:8000/hi?who=Mom
>
> > [!example] **HTTPie**
> >
> > > [!note] bash
> > >
> > > ```bash
> > > http -b localhost:8000/hi?who=Mom
> > > ```
> >
> > > [!note] zsh
> > >
> > > ```zsh
> > > http -b localhost:8000/hi\?who=Mom
> > > ```
> >
> > - bash & zsh 는 String Parsing 에서 약간의 차이가 존재
> >   - bash : `?`
> >   - zsh : `\?`
> >
> > > [!note] Argument
> > >
> > > ```zsh
> > > http -b localhost:8000/hi who==Mom
> > > ```
> >
> > - 이러한 Argument 를 두 개 이상 사용 가능 <p style='margin-top: 0.25em; margin-bottom: 0.25em'></p>
> > - 공백으로 구분된 Argument 를 입력하는 더 쉬움
>
> > [!example] Requests
> >
> > > ```python
> > > >>> import requests
> > > >>> r = requests.get("http://localhost:8000/hi?who=Mom")
> > > >>> r.json()
> > > ```
> >
> > > [!note] Argument
> > >
> > > ```python
> > > >>> import requests
> > > >>> params = {"who": "Mom"}
> > > >>> r = requests.get("http://localhost:8000/hi", params=params)
> > > >>> r.json()
> > > ```
>
> - 다른 방식으로 String 을 제공하고, &nbsp;이를 [[./FastAPI HTTP Request#FastAPI 의 HTTP Request 해석|Path]] 로 전달해 Final Response 로 보낸다.
