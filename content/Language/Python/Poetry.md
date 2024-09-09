---
title: Poetry
tag: Python
---

## Poetry<sup><a href="https://python-poetry.org/docs"></a></sup>

### Introdution

- **Python Virtual Environment** 와 **Package Management** 를 위한 Tool
- `pip` 와 `venv` 의 기능을 결합하여 사용 편의성 향상

### Installation & Usage

- `pip install poetry`
- `poetry add`<sup id="add-ref"><a href="#footnote-add">1</a></sup> & `poetry install`<sup id="install-ref"><a href="footnote-install">2</a></sup>

### Poetry VS pip

- 둘 다 **Package Download** & **Management** 기능 제공
- **Configuration File**
  - <code>pyproject.toml</code> / <code>requirements.txt</code>
- **Package Dependency Management** 기능 제공

### Version Management

- Package Version 을 최소, 최대, 범위 또는 정확한 값<sup id="pinning-ref"><a href="footnote-pinning">3</a></sup>으로 지정 가능
- Project Growth 에 따른 **Managing Dependency Package CHanges** 에 중요

---

<span style="display: block; font-size: 1.5em; margin-top: 0.83em; margin-bottom: 0.83em; margin-left: 0; margin-right: 0; font-weight: 900; text-shadow: 0px 0px 0.5px #000">Footnotes</span>

<ol>
  <li id="footnote-add">New Dependency(Package) 을 Project 에 Add
    <ul>
      <li> File 을 자동으로 Update 하여 New Dependency 를 기록</li>
      <li>Added Package 와 The dependencies 즉시 Install</li>
      <li>Ex) <code>poetry add requests</code>
        <a href="#add-ref" title="Return">↩</a>
      </li>
    </ul>
  </li>
  <p style='margin-top: 0.5em; margin-bottom: 0.5em'></p>
  <li id="footnote-install"><code>pyproject.toml</code> 에 명시된 All dependencies 를 Install
    <ul>
      <li>이미 Install 된 Packages 는 건너뛰고, Missing Package 만 Install </li>
      <li>Project 의 Virtual Environment 을 Create or Update</li>
      <li>New Environment 에서 Project 를 Configure or Another Developer 와 Same Environment 을 구성할 때 사용
        <a href="#install-ref" title="Return">↩</a>
      </li>
    </ul>
  </li>
</ol>
