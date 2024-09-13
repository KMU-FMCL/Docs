---
title: Multiple Request Data
tag: Python/FastAPI
---

## Multiple Request Data

1. 하나의 FastAPI Path Function 에서 여러 **Data Source** 를 동시에 사용 가능 <p style='margin-top: 0.5em; maring-bottom: 0.5em'></p>

2. Example of Data Source <p style='margin-top: 0.25em; maring-bottom: 0.25em'></p>

   - [[FastAPI-URL-Path|URL]] <p style='margin-top: 0.4em; maring-bottom: 0.4em'></p>
   - [[./FastAPI-Query-Parameter|Query Parameter]] <p style='margin-top: 0.4em; maring-bottom: 0.4em'></p>
   - [[FastAPI-Body|HTTP Body]] <p style='margin-top: 0.4em; maring-bottom: 0.4em'></p>
   - [[FastAPI-Header|HTTP Header]]
   - Cookie[^1] <p style='margin-top: 0.5em; maring-bottom: 0.5em'></p>

3. Developer 는 이러한 Data 를 처리하기 위한 **Custom Dependency Function** 을 작성할 수 있음 <p style='margin-top: 0.5em; maring-bottom: 0.5em'></p>

4. 이 Feature 을 활용하여 [[Pagination]] &nbsp;or&nbsp; Authentication 같은 Advance Feature 을 구현할 수 있음 <p style='margin-top: 0.5em; maring-bottom: 0.5em'></p>

5. 이러한 접근 방식은 다양한 Source 에서 Data 를 유연하게 조합하고 Processing 할 수 있게 해줌 <p style='margin-top: 0.5em; maring-bottom: 0.5em'></p>

[^1]: Server 가 User 의 Web browser 에 전송하는 Small Data Fragment
