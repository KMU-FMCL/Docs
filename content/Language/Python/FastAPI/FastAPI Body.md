---
title: Body
tag: Language/Python/FastAPI
---

## Body

### GET

- **멱등성(idempotent)** 을 가져야 하며, &nbsp;Result 만 Return 해야 함.

<h4 style='padding-left: 20px'>Request</h4>

<ul style='padding-left: 60px'>
  <li><a href="FastAPI URL Path.md#URL Path">Path</a> & <a href="FastAPI Query Parameter.md#Query Parameter">Query Parameter</a> 는  사용 가능</li>
  <li><b>Request Body</b> 는 사용 불가능</li>
</ul>

### Request Body

- 주로 [[REST#HTTP 동사와 CRUD Task 의 대응|POST]], &nbsp; [[REST#HTTP 동사와 CRUD Task 의 대응|PUT & PATCH]] Request 에서 Server 로 Info 를 전달할 때 사용

### Example

> [!example] Return String Body
>
> Endpoint 를 [[REST#HTTP 동사와 CRUD Task 의 대응|GET]] 에서 [[REST#HTTP 동사와 CRUD Task 의 대응|POST]] 로 Change
>
> ```python
> from fastapi import FastAPI
>
> app = FastAPI()
>
> @app.post("/hi")
> def greet(who: str = Body(embed=True)):
>     return f"Hello? {who}?"
> ```
>
> > [!Caution]
> >
> > - [[./FastAPI]] 에서 [[REST#HTTP 동사와 CRUD Task 의 대응|POST]] Request 로 **Body** 를 받으려면 Function Parameter 에 `Body(embed=True)` 사용
> > - Client 에서 **Request Body** 를 보낼 때는 [[JSON & API Data Type#JSON & API Data Type|JSON Type]] 으로 Data 전송
> >   - Embed 부분은 단순히 **"String"** 이 아니라 `{"key": "Value"}` 처럼 보여야 함

> [!check]
>
> - Argument `json` 을 사용해 **Request Body** 에 JSON Encoding 한 Data 전달([[REST#HTTP 동사와 CRUD Task 의 대응|POST]] Request)
>
> > [!example] HTTPie
> >
> > ```zsh
> > http -v localhost:8000/hi who=Mom
> > ```
>
> > [!example] Requests
> >
> > ```python
> > >>> import requests
> > >>> r = requests.post("http://localhost:8000/hi", json={"who", "Mom"})
> > >>> r.json()
> > ```
