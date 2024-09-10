---
title: URL Path
tag: Language/Python/FastAPI
---

## URL Path

> [!example] Return Path
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

편집기에서 이 변경 사항을 저장하면 Uvicorn 이 다시 시작된다. 다시 시작하지 않을 경우 hello2.py 등을 생성하고 매번 Uvicorn 을 다시 실행하길 권한다. Uvicorn 에서 오류가 발생한다면 Uvicorn 자체 문제라기보다 오타가 있을 확률이 크다.

URL 에 `{who}` 를 추가하면(`@app.get` 뒤에) URL 의 해당 위치에 <var>who</var> 라는 이름의 변수를 예상하도록 FastAPI 에 지시한다. 그런 다음 FastAPI 는 이 변수를 다음 `greet()` 함수의 <var>who</var> 인수에 할당한다. 이는 경로 데코레이터와 경로 함수 간의 조율을 보여준다.

> [!Caution]
> 수정된 URL 문자열(`"/hi/{who}"`)에 파이썬 f-스트링을 사용하면 안 된다. 중괄호는 URL 을 경로 매개변수로 일치시키기 위해 FastAPI 가 사용하는 표현법이다.

> [!Tip] Test
>
> > [!example] HTTPie 로 **/hi/Mom** Test
> >
> > `zsh`
