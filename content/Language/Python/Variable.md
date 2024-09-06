---
title: Variable
tag: Python
---

## Variable

### Object

- Every Individual Piece of Data 을 &nbsp;감싸는 Structure
  - 고유 **ID**
  - Hardware 와 &nbsp;일치하는 &nbsp;저수준의 &nbsp;**Type**
  - Specific **Value**(Physical Bit)
  - Object<sup id="object-ref"><a href="#footnote-object">1</a></sup> 를 &nbsp;참조하는 &nbsp;Variable 의 &nbsp;수를 &nbsp;나타내는 &nbsp;**Reference Count**
- Object 수준에서 &nbsp;강 Type<sup id="strongtype-ref"><a href="#footnote-strongtype">2</a></sup>을 &nbsp;가짐

### Variable

- Object 를 가리키는 **Name** 일 뿐
- Memory 의 &nbsp;Value 을 &nbsp;직접 &nbsp;가리키지는 않음
- Object 와 &nbsp;일시적으로 &nbsp;Connect

### Another Language 와의 차이점

- 많은 Language 에서 &nbsp;Variable 는 &nbsp;Memory 의 &nbsp;Value 를 &nbsp;직접 &nbsp;가리킴<sup id="memory-ref"><a href="#footnote-memory">3</a></sup>
- Python 은 &nbsp;Object 를 &nbsp;Reference 하는 방식으로 &nbsp;작동

### Variable 할당

- Immutable Object 에 &nbsp;New Value &nbsp;할당 시 &nbsp;New Object 생성
- 이전 Object 는 &nbsp;Reference Count 가 &nbsp;0 이 되면 &nbsp;Memory 에서 &nbsp;Delete

### Scope

- Name 이 &nbsp;동일한 Object 를 &nbsp;가리키는 &nbsp;Code Area
- Another Scope 에서 &nbsp;Same Name &nbsp;사용 가능

### Caution

- Variable 가 &nbsp;Program 전체에서 &nbsp;Another Object 를 &nbsp;Reference 할 &nbsp;수 &nbsp;있음
- 의미 있는 &nbsp;Variable Name &nbsp;사용 권장

<br><b>이러한 특성들로 인해 &nbsp;Python 의 &nbsp;Variable 와 &nbsp;Object Control 방식은 &nbsp;독특하며, &nbsp;이를 이해하는 것이 &nbsp;효과적인 &nbsp;Python Programming 에 &nbsp;중요</b>

---

<span style="display: block; font-size: 1.5em; margin-top: 0.83em; margin-bottom: 0.83em; margin-left: 0; margin-right: 0; font-weight: 900; text-shadow: 0px 0px 0.5px #000">Footnotes</span>

<ol>
  <li id="footnote-object">Software 세계에서 &nbsp;<b>Object</b> 라는 &nbsp;용어는 &nbsp;무수히 많은 의미로 &nbsp;통용
    <a href="#object-ref" title="Return">↩</a>
  </li>
  <br>
  <li id="footnote-strongtype">Type 은 &nbsp;변경되지 않지만 &nbsp;Value 은 &nbsp;바뀔 수 있음
    <ul>
      <li>값을 &nbsp;변경할 수 &nbsp;있으면 &nbsp;Mutable</li>
      <li>값을 &nbsp;변경할 수 &nbsp;없으면 &nbsp;Immutable
        <a href="#strongtype-ref" title="Return">↩</a>
      </li>
    </ul>
  </li>
  <br>
  <li id="footnote-memory">대표적으로 &nbsp;C Language, &nbsp; C 가 &nbsp;Python 보다 &nbsp;빠르다는 얘기를 &nbsp;들어본 적이 &nbsp;있다면 &nbsp;이에서 &nbsp;비롯된 것
    <a href="#memory-ref" title="Return">↩</a>
  </li>
</ol>
