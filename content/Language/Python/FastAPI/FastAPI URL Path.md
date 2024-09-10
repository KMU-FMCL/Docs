---
title: URL Path
tag: Language/Python/FastAPI
---

## URL Path

### Example

> [!example] Return String Path
>
> ```python
> from fastapi import FastAPI
>
> app = FastAPI()
>
> @app.get("/hi/{who}")
> def greet(who):
>     return f"Hello? {who}?"
> ```
>
> - 동적 URL Path 를 만들기 위해 `@app.get("/hi/{String}")` 형식 사용 <p style='margin-top: 0.25em; margin-bottom: 0.25em'></p>
> - Path Function(Ex: `def greet(String):`) 에서 이 [[Python Variable|Variable]] 를 사용 가능
>
> > [!caution] Caution
> >
> > - 수정된 URL String(**"/hi/{String}"**) 에 Python f-string 사용 X <p style='margin-top: 0.25em; margin-bottom: 0.25em'></p>
> > - 중괄호는 FastAPI 의 Path Parameter 문법 <p style='margin-top: 0.25em; margin-bottom: 0.25em'></p>
> > - Code 변경 후 Uvicorn 이 Restart 됨 <p style='margin-top: 0.125em; margin-bottom: 0.125em'></p>
> >   - Restart 하지 않을 경우 New File 생성 후 다시 실행하길 권함
> >   - Uvicorn 에서 Error 가 발생한다면 Uvicorn 자체 Problem 라기보다 오타가 있을 확률 큼

> [!Tip] Test
>
> > [!example] Browser
> >
> > > http://localhost:8000/hi/Mom
>
> > [!example] HTTPie
> >
> > ```zsh
> > http localhost:8000/hi/Mom
> > ```
>
> > [!example] Requests
> >
> > ```python
> > >>> import requests
> > >>> r = requests.get("http://localhost:8000/hi/Mom")
> > >>> r.json()
> > ```
>
> - 이 방식으로 URL 의 일부를 동적으로 처리 가능 <p style='margin-top: 0.25em; margin-bottom: 0.25em'></p>
> - Response 는 JSON Type 으로 Return
