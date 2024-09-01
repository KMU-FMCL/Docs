---
title: Concurrency
---

## 1 . 2 Concurrency

<ul>
  <li>Service 가 성장 시 효율성과 확장성이 중요, <b>Latency</b><sup id="delay-ref"><a href="#Footnote-delay">1</a></sup> & <b>Throughput</b><sup id="usage-ref"><a href="#footnote-usage">2</a></sup> 개선 필요</li>
  <li>완전한 병렬 처리가 아니라 <b>Busy Waiting</b><sup id="wait-ref"><a href="#footnote-wait">3</a></sup> 을 피하는 걸 의미</li>
</ul>

### Asynchronous Processing

<ol>
  <li style='margin-bottom: 0.25em'>Python 은 기본적으론 <b>Synchronous</b><sup id="single-ref"><a href="#footnote-single">5</a></sup> 이지만, &nbsp; <b>Asynchronous<sup id="dual-ref"><a href="#footnote-dual">4</a></sup> Processing</b> 도 가능</li>
  <li style='margin-bottom: 0.55em'><b>I/O-bound</b><sup id="io-ref"><a href="#footnote-io">6</a></sup> Task 에 특히 유용</li>
  <li style='margin-bottom: 0.25em'>FastAPI 에 <b>Synchronous Processing</b> 을 적용하면 <b>Performance</b> 가 크게 향상</li>
  <li>CPU 집약적 Task 를 과도하게 수행하지 않도록 주의<sup id="cpu-ref"><a href="#footnote-cpu">7</a></sup></li>
</ol>

**Concurrency** 은 [[HTTP.md|Modern Web Service]] 에서 중요한 개념이며, 적절히 활용하면 **Performance** 를 크게 개선 가능

---

<span style="display: block; font-size: 1.5em; margin-top: 0.83em; margin-bottom: 0.83em; margin-left: 0; margin-right: 0; font-weight: 900; text-shadow: 0px 0px 0.5px #000">Footnotes</span>

<ol>
  <li id="delay-ref">사전 대기 시간
    <a href="#delay-ref" title="Return">↩</a>
  </li>
  <li id="usage-ref">Service 와 Caller 간의 초당 <b>Byte</b> 수
    <a href="#usage-ref" title="Return">↩</a>
  </li>
  <li id="wait-ref"><b>Process</b> 나 <b>Thread</b> 가 특정 조건이 충족될 때까지 <b>Idle State</b> 로 대기하는 대신, <br> &emsp; 계속해서 해당 조건을 확인하는 Task 를 반복하는 것<br> &emsp; CPU 자원을 소모하면서 대기하기에 비효율적일 순 있으나, <b>Fast Response</b> 가 필요한 상황에서 사용되기도 함
    <a href="#wait-ref" title="Return">↩</a>
  </li>
  <li id="dual-ref"><code>비동기식</code> : Task 가 시작된 후 완료될 때 까지 기다리지 않고, Other Task 를 병행하여 수행할 수 있는 방식
    <a href="#dual-ref" title="Return">↩</a>
  </li>
  <li id="single-ref"><code>동기식</code> : Task 가 순차적으로 진행되며, 하나의 Task 가 완료될 때까지 Next Task 가 수행되지 않는 방식
    <a href="#single-ref" title="Return">↩</a>
  </li>
  <li id="io-ref">Program 이나 Task 가 주로 I/O 에 의해 제한 되는 상태
    <ul>
      <li>Disk Read/Write, Network Communication, File I/O, etc 에 많은 시간 소요</li>
      <li>CPU 보다 I/O Task의 속도가 전체 성능을 좌우</li>
    </ul>
  </li>
</ol>
