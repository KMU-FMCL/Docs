---
title: API Type
---

## 1 . 1 . 1 API Type

### 각 **API** 는 다음을 정의

- **Protocol** : Control structure
- **Format** : Content structure

### **API** 종류

<ol>
  <li style='font-weight: 900'>
  <span style='font-weight: normal'>초기 <b>API</b></span>
    <ul>
      <li style='font-weight: normal'>주로 Local Libaray Function 호출 형태</li>
    </ul>
  </li>
  <br>
  <li style='font-weight: 900'>
  <span style='font-weight: normal'><b>원격 프로시저 호출</b>(RPC)</span>
    <ul>
      <li style='font-weight: normal'>다른 Process 나 Computer 의 Function 를 Local Function 처럼 호출</li>
      <li style='font-weight: normal'>Ex) gRPC<sup id="grpc-ref"><a href="#footnote-grpc">1</a></sup></li>
    </ul>
  </li>
  <br>
  <li style='font-weight: 900'>
  <span style='font-weight: normal'><b>Messaging</b>(RPC)</span>
    <ul>
      <li style='font-weight: normal'>Process 간 Small data Chunk<sup id="chunk-ref"><a href="#footnote-chunk">2</a></sup></li>
      <li style='font-weight: normal'>Command 나 Event 가능</li>
      <li style='font-weight: normal'>Ex) Apache Kafka<sup id="apache-ref"><a href="#footnote-apache">3</a></sup>, RabbitMQ<sup id="rabbitmq-ref"><a href="#footnote-rabbitmq">4</a></sup>, NATS<sup id="nats-ref"><a href="#footnote-nats">5</a></sup>, ZeroMQ<sup id="zeromq-ref"><a href="#footnote-zeromq">6</a></sup></li>
    </ul>
  </li>
  <br>
  <li style='font-weight: 900'>
  <span style='font-weight: normal'><b>Communication Pattern</b>(RPC)</span>
    <ul>
      <li style='font-weight: normal'><b>Request - Response</b> : Web Browser - Web Server</li>
      <li style='font-weight: normal'><b>Publish - Subscribe</b>(Pub - Sub) : Publisher 가 Message publish, Subscriber 가 선별적으로 Receive</li>
      <li style='font-weight: normal'><b>Queue</b> : Pub - Sub 와 유사하나 Single Subscriber 만 Message 처리</li>
    </ul>
  </li>
</ol>

<b><br>이 모든 기술들은 Web Service 에서도 Back-end 작업 수행 등에 활용 가능</b>

---

<span style="display: block; font-size: 1.5em; margin-top: 0.83em; margin-bottom: 0.83em; margin-left: 0; margin-right: 0; font-weight: 900; text-shadow: 0px 0px 0.5px #000">Footnotes</span>

<ol>
  <li id="footnote-grpc">
    <a href="https://grpc.io">https://grpc.io</a>
    <a href="#grpc-ref" title="Return">↩</a>
  </li>
  <li id="footnote-chunk">Piece, Data 를 더 작은 단위로 나눈 것
    <a href="#chunk-ref" title="Return">↩</a>
  </li>
  <li id="footnote-apache">
    <a href="https://kafka.apache.org">https://kafka.apache.org</a>
    <a href="#apache-ref" title="Return">↩</a>
  </li>
  <li id="footnote-rabbitmq">
    <a href="https://www.rabbitmq.com">https://www.rabbitmq.com</a>
    <a href="#rabbitmq-ref" title="Return">↩</a>
  </li>
  <li id="footnote-nats">
    <a href="https://nats.io">https://nats.io</a>
    <a href="#nats-ref" title="Return">↩</a>
  </li>
  <li id="footnote-zeromq">
    <a href="https://zeromq.org">https://zeromq.org</a>
    <a href="#zeromq-ref" title="Return">↩</a>
  </li>
</ol>
