---
title: HTTP Response
tag: Python/FastAPI
---

## HTTP Response

- [[./FastAPI]] 는 기본적으로 All Return Value 를 [[JSON-&-API-Data-Type#JSON(JavaScript Object Notation)|JSON]] 으로 Conversion
  - **Ex)** &nbsp;String, Python Built-in Type, Pydantic Model, etc.
- **HTTP Response Header** 는 `'Content-type': application` 이 포함
- 이는 API Development 를 Simplification 하기 위한 [[./FastAPI]] 의 Default Setting

### Subheadding

- [[FastAPI Status Code|Status Code]]
- [[FastAPI-Header|Header]]
- [[FastAPI-Response-Type|Response Type]]
- [[FastAPI-Type-Conversion|Type Conversion]]
- [[FastAPI-Model-Type-&-Response-Model|Model Type & Response Model]]

<br>**이러한 Feature 는 [[./FastAPI]] 를 사용할 때 일관된 JSON Response 를 쉽게 생성할 게 있게 해준다.**
