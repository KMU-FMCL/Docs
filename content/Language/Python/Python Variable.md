---
title: Variable
tag: Language/Python
---

## Variable

### Object

- Every Individual Piece of Data 을 감싸는 Structure
  - 고유 **ID**
  - Hardware 와 일치하는 저수준의 **Type**
  - Specific **Value**(Physical Bit)
  - Object<sup id="object-ref"><a href="#footnote-object">1</a></sup> 를 Reference 하는 Variable 의 수를 나타내는 **Reference Count**
- Object 수준에서 강 Type<sup id="strongtype-ref"><a href="#footnote-strongtype">2</a></sup>을 가짐

### Variable

- Object 를 가리키는 **Name** 일 뿐
- Memory 의 Value 을 직접 가리키지는 않음
- Object 와 일시적으로 Connect

### Another Language 와의 차이점

- 많은 Language 에서 Variable 는 Memory 의 Value 를 직접 가리킴<sup id="memory-ref"><a href="#footnote-memory">3</a></sup>
- Python 은 Object 를 Reference 하는 방식으로 작동

### Variable 할당

- Immutable Object 에 New Value 할당 시 New Object 생성
- 이전 Object 는 Reference Count 가 0 이 되면 Memory 에서 Delete

### Scope

- Name 이 동일한 Object 를 가리키는 Code Area
- Another Scope 에서 Same Name 사용 가능

### Caution

- Variable 가 Program 전체에서 Another Object 를 Reference 할 수 있음
- 의미 있는 Variable Name 사용 권장

<br><b>이러한 특성들로 인해 Python 의 Variable 와 Object Control 방식은 독특하며, &nbsp;이를 이해하는 것이 효과적인 Python Programming 에 중요</b>

---

<span style="display: block; font-size: 1.5em; margin-top: 0.83em; margin-bottom: 0.83em; margin-left: 0; margin-right: 0; font-weight: 900; text-shadow: 0px 0px 0.5px #000">Footnotes</span>

<ol>
  <li id="footnote-object">Software 세계에서 <b>Object</b> 라는 용어는 무수히 많은 의미로 통용
    <a href="#object-ref" title="Return">↩</a>
  </li>
  <p style='margin-top: 0.5em; margin-bottom: 0.5em'></p>
  <li id="footnote-strongtype">Type 은 변경되지 않지만 Value 은 바뀔 수 있음
    <ul>
      <li>값을 변경할 수 있으면 Mutable</li>
      <li>값을 변경할 수 없으면 Immutable
        <a href="#strongtype-ref" title="Return">↩</a>
      </li>
    </ul>
  </li>
  <p style='margin-top: 0.5em; margin-bottom: 0.5em'></p>
  <li id="footnote-memory">대표적으로 C Language, &nbsp;C 가 Python 보다 빠르다는 얘기를 들어본 적이 있다면 이에서 비롯된 것
    <a href="#memory-ref" title="Return">↩</a>
  </li>
</ol>
