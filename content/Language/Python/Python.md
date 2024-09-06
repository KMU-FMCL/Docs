---
title: Modern Python
tag: Program Language
---

## Python

### Tool

- [[./Version.md|Python Version]]
- Package Management<sup id="management-ref"><a href="#footnote-management">1</a></sup>
- Code Formatting<sup id="formatting-ref"><a href="#footnote-formatting">2</a></sup>
- [[Testing.md|Testing]]<sup id="testing-ref"><a href="#footnote-testing">3</a></sup>
- Source control<sup id="source-ref"><a href="#footnote-source">4</a></sup> & Continuous Integration(CI)<sup id="ci-ref"><a href="#footnote-ci">5</a></sup>
- Web Tool <sup id="tool-ref"><a href="#footnote-tool">6</a></sup>

### [[./API & Service.md|API & Service]]

### [[./Variable.md|Variable]]

### [[Py Type Hint|Type Hint]]

### [[Py Data Structure|Data Structure]]

### [[Py Web Framwork|Web Framework]]

---

<span style="display: block; font-size: 1.5em; margin-top: 0.83em; margin-bottom: 0.83em; margin-left: 0; margin-right: 0; font-weight: 900; text-shadow: 0px 0px 0.5px #000">Footnotes</span>

<ol>
  <li id="footnote-management">전통적으로는 pip 를 사용, &nbsp;<a href="Virtual.md">Virtual Environment</a> 를 사용하거나 &nbsp;<a href="Poetry.md">Poetry</a> &nbsp;같은 대체제 고려 가능
    <a href="#management-ref" title="Return">↩</a>
  </li>
  <br>
  <li id="footnote-formatting">중요하지만 이전의 내용보단 덜 중요, &nbsp;불필요한 논쟁을 피하기 위해선 자동화된 &nbsp;Formatting Tool 을 사용
    <ul>
      <li style='margin-bottom: 0.35em'>Ex) <code>black</code><sup><a href="https://black.readthedocs.io"></a></sup>, &nbsp;<code>pip install black</code>
        <a href="#formatting-ref" title="Return">↩</a>
      </li>
    </ul>
  </li>
  <br>
  <li id="footnote-testing"><code>unittest</code> 가 &nbsp;Standard Python Test Package
    <ul>
      <li style='margin-bottom: 0.35em'>하지만, 대부분의 &nbsp;Python Developer 는 &nbsp;<code>pytest</code><sup><a href="https://docs.pytest.org"></a></sup> 사용</li>
      <li style='margin-bottom: 0.35em'>Ex) <code>pip install pytest</code>
        <a href="#testing-ref" title="Return">↩</a>
      </li>
    </ul>
  </li>
  <br>
  <li id="footnote-source"><code>Git</code> 이 현재 가장 보편적인 시스템
    <ul>
      <li>Github & GitLab &nbsp;등의 &nbsp;Platform 에서 Git Storage Hosting</li>
      <li>All Programming Languages 에 &nbsp;사용 가능
        <a href="#source-ref" title="Return">↩</a>
      </li>
    </ul>
  </li>
  <br>
  <li id="footnote-ci"><b>pre-commit</b>
    <ul>
      <li>Local 에서 &nbsp;Commit &nbsp;전 &nbsp;Test &nbsp;실행 가능</li>
      <li>Ex) <code>black</code>, &nbsp;<code>pytest</code></li>
      <li>Remote Repository 에 &nbsp;Push 후 추가 &nbsp;<b>CI</b> Test &nbsp;가능
        <a href="#ci-ref" title="Return">↩</a>
      </li>
    </ul>
  </li>
  <br>
  <li id="footnote-tool">앞으로 &nbsp;사용하게 &nbsp;될 &nbsp;주요 Tool
    <ul>
      <li><b>FastAPI</b> : Web Framework</li>
      <li><b>Uvicorn</b> : Asynchronous Web Server</li>
      <li><b>HTTPie</b> : <code>curl</code> 과 &nbsp;유사한 Text &nbsp;기반 &nbsp;Web Client</li>
      <li><b>Requqsts</b> : Synchronous Web Client Package</li>
      <li><b>HTTPX</b> : Asynchronous/Synchronous Web Client Package
        <a href="#tool-ref" title="Return">↩</a>
      </li>
    </ul>
  </li>
</ol>
