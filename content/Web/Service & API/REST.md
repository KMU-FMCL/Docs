---
title: REST(ful)
---

## 1 . 1 . 3 REST(ful)

### REST(Representational State Transfer)의 주요 특징

<ol>
  <li>HTTP Protocol Usage</li>
  <li>상태 비저장(Stateless)<sup id="less-ref"><a href="#foonote-less">1</a></sup></li>
  <li>Cacheable<sup id="cache-ref"><a href="#foonote-cache">2</a></sup></li>
  <li>Resource-based<sup id="base-ref"><a href="#foonote-base">3</a></sup></li>
</ol>

### RESTful Web Service 의 핵심 개념

- `Resource` : 작업을 수행할 수 있는 Data
- `Endpoint` : 고유한 URL 과 HTTP 동사(동작)로 구성된 기능 접근

<h3>HTTP 동사와 CRUD<sup id="crud-ref"><a href="#foonote-crud">4</a></sup> Task 의 대응</h3>

- `POST` : 생성(Create)
- `GET` : 읽기(Read)
- `PUT/PATCH` : 수정(Update)
- `DELETE` : 삭제(Delete)

### RESTful Communication

- `Request` : Client 가 Data 를 Header , URL, Quary parameter, 본문에 담아 전송
- `Response` : Server 가 State Code, Header, 본문으로 응답

### HTTP State Code

- `1xx` : Information
- `2xx` : Success
- `3xx` : Redirection
- `4xx` : Client Error
- `5xx` : Server Error

<br>PS) `418` State Code(I'm a teapot)는 Web 의 유머러스한 Easter Egg

![GoogleStatus418](../Media/GoogleStatus418.png)

---

<span style="display: block; font-size: 1.5em; margin-top: 0.83em; margin-bottom: 0.83em; margin-left: 0; margin-right: 0; font-weight: 900; text-shadow: 0px 0px 0.5px #000">Footnotes</span>

<ol>
  <li id="foonote-less">Server 가 Client 의 이전 Request 를 저장하지 않는 Architecture
    <a href="#less-ref" title="Return">↩</a>
  </li>
  <li id="foonote-cache">Data 를 <code>Cache</code> 에 저장할 수 있는 지 여부<br>(Server 로 부터 Re-request 하지 않고 Client Cache 에서 가져올 수 있는 Data)
    <a href="#cache-ref" title="Return">↩</a>
  </li>
  <li id="foonote-base"><code>Resource</code> : User 가 식별하고 Task 를 수행할 수 있는 Data<br>특정 System 이나 설계가 <code>Resource</code> 를 중심으로 작동하거나 조작되는 방식
    <a href="#base-ref" title="Return">↩</a>
  </li>
  <li id="foonote-crud">Database 의 기본 동작
    <ul>
      <li><b>쓰기(Create)</b></li>
      <li><b>읽기(Read)</b></li>
      <li><b>수정(Update)</b></li>
      <li><b>삭제(Delete)</b></li>
    </ul>
  </li>
</ol>
