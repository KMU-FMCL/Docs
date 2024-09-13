---
title: HTTP Response
tag: Python/FastAPI
---

## HTTP Response

기본적으로 FastAPI 는 엔드포인트 함수에서 반환하는 모든 것을 JSON 으로 변환한다. HTTP 응답<sup>response</sup>의 헤더 행은 `Content-type: application/json` 이다. 따라서 `greet()` 함수가 처음에 **"Hello World?"** 라는 문자열을 반환하지만, FastAPI 는 이를 JSON 으로 변환한다. 이는 API 개발을 간소화하기 위해 FastAPI 에서 선택한 기본 사항 중 하나다.

이 경우 파이썬 문자열 **"Hello? World?"** 는 이에 상응하는 JSON 문자열 **"Hello? World?"** 라는 동일한 문자열로 변환된다. 그러나 파이썬 내장 타입이든 Pydantic 모델이든 반환하는 모든 것은 JSON 으로 변환된다.
