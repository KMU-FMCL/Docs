---
title: Web Framework
tag: Python, Web/Framework
---

## Web Framework

### 주요 역할

- [[HTTP.md]] 로 전달되는 Byte 와 Python Data Structure 간 변환
- Develop 노력 절감, 필요한 기능이 없으면 해결해야[^1] 할 수 있음

### WSGI(Web Server Gateway Interface)

- Python 표준 사양
- Application Code 를 Synchronous 으로 Web Server 에 Connect
- 기존 [[Python Web Framwork]] 의 기반<sup><a href="https://wsgi.readthedocs.io"></a></sup>

### [[../../Web/Concurrency.md#Concurrency|Concurrency]] 의 중요성

- **Synchronous Communication** 의 한계(CPU 보다 느린 **Task idle time**)
- 더 나은 [[../../Web/Concurrency.md#Concurrency|Concurrency]] 필요성 대두

### ASGI(Asynchronous Server Gateway Interface)

- [[../../Web/Concurrency.md#Concurrency|Concurrency]] 개선을 위해 최근 Develop 됨

### 활용 Tip

- 가능한 기존 Solution 활용[^2]
- 필요시 Open Source Framwork 수정 가능[^3]

### Subtitle

- Django <p style='margin-top: 0.5em; margin-bottom: 0.5em;'></p>
- Flask <p style='margin-top: 0.5em; margin-bottom: 0.5em;'></p>
- [[FastAPI]]

[^1]: Web Framwork 의 내부 Source 를 입맛에 맞게 고친다는 뜻

[^2]: 바퀴를 다시 발명하지 말라는 뜻

[^3]: 원하는 기능이나 Issue 가 있다면 이를 보고하고 직접 수정 사항을 제출해볼 것
