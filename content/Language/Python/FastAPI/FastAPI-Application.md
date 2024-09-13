---
title: Application
tag: Python/FastAPI
---

## Application

### Default Python Package

> [!tldr] Package
>
> > [!info] FastAPI
> >
> > - Web Framework
> >
> > ```zsh
> > pip install fastapi
> > ```
>
> > [!info] **Uvicorn**
> >
> > - Asynchronous Web Server
> >
> > ```zsh
> > pip install uvicorn
> > ```
>
> > [!info] <span id="httpie-ref"><a href="#footnote-httpie">HTTPie</a></span>
> >
> > - Text Web Client
> > - 가장 잘 알려진 Text Web CLient 는 `curl`
> >   - But, `HTTPie` 가 더 사용하기 쉽고 기본적으로 [[JSON-&-API-Data-Type#JSON(JavaScript Object Notation)|JSON]] Encoding/Decoding 을 사용하므로 [[./FastAPI]] 와 더 잘 어울림
> >
> > ```zsh
> > pip install httpie
> > ```
>
> > [!info] **Requests** [[Concurrency|Synchronous]]
> >
> > - Synchronous Web Client Package
> >
> > ```zsh
> > pip install requests
> > ```
>
> > [!info] **HTTPX** [[Concurrency|Synchronous & Asynchronous]]
> >
> > - Asynchronous/Synchronous Web Client Package
> >
> > ```zsh
> > pip install httpx
> > ```

### Example

> [!example] [[REST#RESTful Web Service 의 핵심 개념|Endpoint]]:**hello.py**
>
> ```python
> from fastapi import FastAPI
>
> app = FastAPI()
>
> @app.get("/hi")
> def greet():
>     return "Hello? World?"
> ```

> [!Tip] <span id="uvicorn">Uvicorn</span>
>
> > [!example] Command Line
> >
> > ```zsh
> > uvicorn hello:app --reload
> > ```
>
> > [!example] Internally
> >
> > ```python
> > from fastapi import FastAPI
> >
> > app = FastAPI()
> >
> > @app.get("/hi")
> > def greet():
> >     return "Hello? World?"
> >
> > if __name__ == "__main__":
> >     import uvicorn
> >     uvicorn.run("hello:app", reload=True)
> > ```
>
> 어느 경우든, &nbsp;`reload` Argument 는 `hello.py` 가 변경되면 Web Server 를 다시 시작하도록 <a href="Python.md#footnote-tool">Uvicorn</a> 에 지시
>
> - 두 경우 기본적으로 **localhost** 의 `8000` 번 Port 를 사용
>   - 외부 & 내부, &nbsp;어디에서 시작하든 두 경우 모두 원하는 **host** & **port** Argument 사용 가능

> [!tldr] Test
> 이제 Server 에 단일 Endpoint(`/hi`)가 있고 Request 를 받을 준비 완료
>
> - Browser: 상단 주소창에 URL 입력
> - `HTTPie`: 표시된 Command 입력
> - `Request` & `HTTPX`: Python Interpreter 사용해서 입력
>
> > [!check] Browser
> >
> > > http://localhost:8000/hi
>
> > [!check] **Requests**
> >
> > ```python
> > >>> import requests
> > >>> r = requests.get("http://localhost:8000/hi")
> > >>> r.json()
> > ```
>
> > [!check] **HTTPX**
> >
> > ```python
> > >>> import httpx
> > >>> r = httpx.get("http://localhost:8000/hi")
> > >>> r.json()
> > ```
>
> > [!check] **HTTPie**
> >
> > > [!note] Basic
> > >
> > > ```zsh
> > > http localhost:8000/hi
> > > ```
> >
> > > [!note] Response Body
> > >
> > > ```zsh
> > > http -b localhost:8000/hi
> > > ```
> >
> > - `-b` 를 사용해 Response Header 를 건너뛰고 Body 만 Print
> >
> > > [!note] Display All Information
> > >
> > > ```zsh
> > > http -v localhost:8000/hi
> > > ```
> >
> > - `-v` 를 사용해 Full Request Header & Response 를 가져옴.

### Caution

- `app` 은 All Web Application 을 나타내는 최상위 [[./FastAPI]] [[Python-Variable|Object]]

<p style='margin-top: 0.5em; margin-bottom: 0.5em'></p>

- `app.get("/hi")` 는 **Path Decorator**. 이는 [[./FastAPI]] 에 다음 사항을 알려줌.
  - URL **"/hi"** 에 대한 [[REST#RESTful Communication|Request]] 는 Next Function 으로 전달돼야 함.
  - Decorator 는 [[REST#HTTP 동사와 CRUD Task 의 대응|HTTP GET 동사]]에만 적용.
    - 또한 다른 [[REST#HTTP 동사와 CRUD Task 의 대응|HTTP 동사(PUT, POST, etc.)]]와 함께 전송된 **"/hi"** [[HTTP|URL]] 에 응답할 수 있는데, 각 동사에는 [[REST#HTTP 동사와 CRUD Task 의 대응|개별 기능]]이 있음.

<p style='margin-top: 0.5em; margin-bottom: 0.5em'></p>

- `def greet()`<sup id="greet-ref"><a href="#footnote-greet">1</a></sup> 은 Path Function 으로, &nbsp;[[REST#RESTful Web Service 의 핵심 개념|HTTP Request & Response]] 의 주요 접점.

<p style='margin-top: 0.5em; margin-bottom: 0.5em'></p>

- [[./FastAPI]] 를 Test 하는데 `Requests` & `HTTPX` 중 어느 것이 좋다고 단언할 수 없음.
  - 앞으로의 Example 에서는 `Requests` 를 사용하나 [[Concurrency|Asynchronous]] Request 를 할 때는 `HTTPX` 를 사용

---

<span style="display: block; font-size: 1.5em; margin-top: 0.83em; margin-bottom: 0.83em; margin-left: 0; margin-right: 0; font-weight: 900; text-shadow: 0px 0px 0.5px #000">Footnotes</span>

<ol>
  <li id="footnote-greet">현재 에시엔 Argument 가 없지만, &nbsp;FastAPI 내부에 훨씬 더 많은 기능이 존재함.
    <a href="#greet-ref" title="Return">↩</a>
  </li>
</ol>
