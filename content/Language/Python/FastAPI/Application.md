---
title: Application
tag: Python, FastAPI
---

## Application

### Default Python Package

- [[./FastAPI]] Framework

  ```zsh
  pip install fastapi
  ```

<p style='margin-top: 1.5em; margin-bottom: 1.5em'></p>

- **Uvicorn** Web Server

  ```zsh
  pip install uvicorn
  ```

<p style='margin-top: 1.5em; margin-bottom: 1.5em'></p>

- **HTTPie**<sup id="httpie-ref"><a href="#footnote-httpie">1</a></sup> Text Web Client

  ```zsh
  pip install httpie
  ```

<p style='margin-top: 1.5em; margin-bottom: 1.5em'></p>

- **Requests** [[Concurrency|Synchronous]] Web Client Package

  ```zsh
  pip install requests
  ```

<p style='margin-top: 1.5em; margin-bottom: 1.5em'></p>

- **HTTPX** [[Concurrency|Synchronous & Asynchronous]] Web Client Package
  ```zsh
  pip install httpx
  ```

### Example

> [!example] 1. [[REST#RESTful Web Service 의 핵심 개념|Endpoint]]:**hello.py**
>
> ```python
> from fastapi import FastAPI
>
> app = FastAPI()
> @app.get("/hi")
> def greet():
>     return "Hello? World?"
> ```

> [!example] 2. Command Line 으로 **uvicorn** Start
>
> ```zsh
> uvicorn hello:app --reload
> ```

> [!example] 3. Internally **uvicorn** Start
>
> ```python
> from fastapi import FastAPI
>
> app = FastAPI()
> @app.get("/hi")
> def greet():
>     return "Hello? World?"
>
> if __name__ == "__name__":
>     import uvicorn
>     uvicorn.run("hello:app", reload=True)
> ```

> [!example] 4. Browser 에서 **/hi** Test
>
> ```zsh
> http://localhost:8000/hi
> ```

> [!example] <span id="requests-ref"><a href="#footnote-requests">5</a></span>. **Requests** 로 **/hi** Test
>
> ```python
> >>> import requests
> >>> r = requests.get("http://localhost:8000/hi")
> >>> r.json()
> ```

### Caution

- `app` 은 All Web Application 을 나타내는 최상위 [[./FastAPI]] [[Variable|Object]]

<p style='margin-top: 0.5em; margin-bottom: 0.5em'></p>

- `app.get("/hi")` 는 **Path Decorator**. 이는 [[./FastAPI]] 에 다음 사항을 알려줌.
  - URL **"/hi"** 에 대한 [[REST#RESTful Communication|Request]] 는 Next Function 으로 전달돼야 함.
  - Decorator 는 [[REST#HTTP 동사와 CRUD Task 의 대응|HTTP GET 동사]]에만 적용.
    - 또한 다른 [[REST#HTTP 동사와 CRUD Task 의 대응|HTTP 동사(PUT, POST, etc.)]]와 함께 전송된 **"/hi"** [[HTTP|URL]] 에 응답할 수 있는데, 각 동사에는 [[REST#HTTP 동사와 CRUD Task 의 대응|개별 기능]]이 있음.

<p style='margin-top: 0.5em; margin-bottom: 0.5em'></p>

- `def greet()`<sup id="greet-ref"><a href="#footnote-greet">2</a></sup> 은 Path Function 으로, &nbsp;[[REST#RESTful Web Service 의 핵심 개념|HTTP Request & Response]] 의 주요 접점.

<p style='margin-top: 0.5em; margin-bottom: 0.5em'></p>

- [[./FastAPI]] 를 Test 하는데 `Requests` & `HTTPX` 중 어느 것이 좋다고 단언할 수 없음.
  - 앞으로의 Example 에서는 `Requests` 를 사용하나 [[Concurrency|Asynchronous]] Request 를 할 때는 `HTTPX` 를 사용

---

<span style="display: block; font-size: 1.5em; margin-top: 0.83em; margin-bottom: 0.83em; margin-left: 0; margin-right: 0; font-weight: 900; text-shadow: 0px 0px 0.5px #000">Footnotes</span>

<ol>
  <li id="footnote-httpie">가장 잘 알려진 Text Web Client 는 <code>curl</code>
    <ul>
      <li>하지만 <code>HTTPie</code> 가 더 사용하기 쉽고 기본적으로 <a href="JSON & API Data Type.md#JSON(JavaScript Object Notation)">JSON</a> Incoding & Decoding 을 사용하므로 FastAPI 와 더 잘 어울림.
        <a href="#httpie-ref" title="Return">↩</a>
      </li>
    </ul>
  </li>
  <p style='margin-top: 0.5em; margin-bottom: 0.5em'></p>
  <li id="footnote-greet">현재 에시엔 Argument 가 없지만, &nbsp;FastAPI 내부에 훨씬 더 많은 기능이 존재함.
    <a href="#greet-ref" title="Return">↩</a>
  </li>
  <p style='margin-top: 0.5em; margin-bottom: 0.5em'></p>
  <li id="footnote-requests">Python Interpreter 라는 점을 명심하라.
    <ul>
      <li>Command Line 에 냅다 Copy & Paste 하지 말라는 뜻
        <a href="#requests-ref" title="Return">↩</a>
      </li>
    </ul>
  </li>
</ol>
