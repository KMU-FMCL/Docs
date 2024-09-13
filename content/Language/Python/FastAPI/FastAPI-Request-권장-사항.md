---
title: Request 권장 사항
tag: Python/FastAPI
---

## Request 권장 사항

- URL Argument 전달 시 [[REST|RESTful]] 가이드라인을 따르는 것이 좋음 <p style='margin-top: 0.4em; margin-bottom: 0.4em'></p>

- Query String 은 주로 선택적 Argument[^1] 에 사용
- Request Body 는 더 큰 Input[^2] 에 사용 <p style='margin-top: 0.4em; margin-bottom: 0.4em'></p>
- Data 정의에 [[Type-Hint|Type Hint]] 를 제공하면 Pydantic 이 자동으로 Argument 의 Type 과 존재 여부를 검사할 수 있음

<br>**이러한 권장 사항을 따르면 [[Service-&-API#Web Service & API|API Design]] 이 더 명확하고 일관성 있게 되며, Data 유효성 Test 도 향상됨**

[^1]: [[Pagination]]

[^2]: **Ex)** &nbsp;**전체** &nbsp;or&nbsp; **부분 Model**
