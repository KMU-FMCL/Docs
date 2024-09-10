---
title: HTTP Request
tag: Language/Python/FastAPI
---

## HTTP Request

### Example

> [!example] 예시 3-10 HTTP 요청
>
> ```zsh
> GET /hi HTTP/1.1
> Accept: /
> Accept-Encoding: gzip, deflate
> Connection: keep-alive
> Host: localhost:8000
> User-Agent: HTTPie/3.2.1
> ```

### HTTP Request 의 Structure

- [[REST#HTTP 동사와 CRUD Task 의 대응|동사(GET, POST, etc.)]] & Path(`/hi`, etc.)
- [[REST#RESTful Communication|All Query Parameter]](URL 의 ? 뒤에 오는 부분, 현재 Request 에는 X)
- [[REST#RESTful Communication|기타 HTTP Header]]
- [[REST#RESTful Communication|Request Body Content]] X

### FastAPI 의 HTTP Request 해석

- **Header**: [[REST#RESTful Communication|HTTP Header]]
- **Path**: [[HTTP#HTTP|URL]]
- **Query**: [[REST#RESTful Communication|Query Parameter]](URL 끝의 ? 뒤)
- **Body**: [[REST#RESTful Communication|HTTP Body]]

### FastAPI 의 장점

- HTTP Request Data 에 직접 접근 가능
- Path Function 내에서 필요한 Argument 를 직접 선언 가능
- **Dependency Injection** 기법 사용

### Example Application 확장

- `who` Parameter Add 예정
- Parameter 전달 방법
  - URL Path
  - Query Parameter
  - HTTP Body
  - HTTP Header
