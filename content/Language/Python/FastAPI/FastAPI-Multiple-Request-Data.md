---
title: Multiple Request Data
tag: Python/FastAPI
---

## Multiple Request Data

1. 하나의 FastAPI Path Function 에서 여러 Data Source 를 동시에 사용 가능

   - [[FastAPI-URL-Path|URL]]
   - [[./Query Parameter]]
   - [[FastAPI-Body|HTTP Body]]
   - [[FastAPI-Header|HTTP Header]]
   - Cookie[^1]

동일한 경로 함수에서 이러한 메서드를 두 개 이상 사용할 수 없다. 즉 URL, 쿼리 매개변수, HTTP 본문, HTTP 헤더, 쿠키 등에서 데이터를 가져올 수 있다. 또한 이러한 데이터를 처리하는 의존성 함수를 직접 작성할 수 있다.

페이지네이션<sup>pagination</sup>이나 인증 같은 특별한 방법으로 결합할 수 있다.

[^1]: Server 가 User 의 Web browser 에 전송하는 Small Data Fragment
