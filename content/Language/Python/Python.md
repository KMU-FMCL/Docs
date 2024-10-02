---
title: Modern Python
tag: Language, Python
---

## Python

```mermaid
gantt
    title Python Release Cycle
    dateFormat  YYYY
    axisFormat %Y

    section Python 2.6
    End-of-Life : crit, 2008, 2013

    section Python 2.7
    End-of-Life : crit, 2010, 2020

    section Python 3.0
    End-of-Life : crit, 2008, 2009

    section Python 3.1
    End-of-Life : crit, 2009, 2012

    section Python 3.2
    End-of-Life : crit, 2011, 2016

    section Python 3.3
    End-of-Life : crit, 2012, 2017

    section Python 3.4
    End-of-Life : crit, 2014, 2019

    section Python 3.5
    End-of-Life : crit, 2015, 2020

    section Python 3.6
    End-of-Life : crit, 2016, 2021

    section Python 3.7
    End-of-Life : crit, 2018, 2023

    section Python 3.8
    Security : done, 2019, 2024

    section Python 3.9
    Security : done, 2020, 2025

    section Python 3.10
    Security : done, 2021, 2026

    section Python 3.11
    Security : done, 2022, 2027

    section Python 3.12
    Bugfix  : active, 2023, 2028

    section Python 3.13
    Pre-release : active, 2024, 2029

    section Python 3.14
    Feature : active, 2025, 2030
```

### Tool

- [[Python-Version#Version]]
- Package Management<sup id="management-ref"><a href="#footnote-management">1</a></sup>
- Code Formatting<sup id="formatting-ref"><a href="#footnote-formatting">2</a></sup>
- [[Testing]]<sup id="testing-ref"><a href="#footnote-testing">3</a></sup>
- Source control<sup id="source-ref"><a href="#footnote-source">4</a></sup> & Continuous Integration(CI)<sup id="ci-ref"><a href="#footnote-ci">5</a></sup>
- <span><a href="FastAPI-Application.md#Default Python Package">Web Tool</a></span>

### Subtitle

- [[./Python-API-&-Service|API & Service]] <p style='margin-top: 0.5em; margin-bottom: 0.5em;'></p>
- [[./Python-Variable|Variable]] <p style='margin-top: 0.5em; margin-bottom: 0.5em;'></p>
- [[./Type-Hint|Type-Hint]] <p style='margin-top: 0.5em; margin-bottom: 0.5em;'></p>
- [[Py Data Structure|Data Structure]] <p style='margin-top: 0.5em; margin-bottom: 0.5em;'></p>
- [[./Python-Web-Framework|Web Framework]]

---

<span style="display: block; font-size: 1.5em; margin-top: 0.83em; margin-bottom: 0.83em; margin-left: 0; margin-right: 0; font-weight: 900; text-shadow: 0px 0px 0.5px #000">Footnotes</span>

<ol>
  <li id="footnote-management">전통적으로는 pip 를 사용, &nbsp;<a href="Virtual.md">Virtual Environment</a> 를 사용하거나 <a href="Poetry.md">Poetry</a> 같은 대체제 고려 가능
    <a href="#management-ref" title="Return">↩</a>
  </li>
  <li id="footnote-formatting">중요하지만 다른 것들에 비해 중요도 떨어짐, &nbsp;불필요한 논쟁을 피하기 위해선 자동화된 &nbsp;Formatting Tool 을 사용
    <ul>
      <li style='margin-bottom: 0.35em'>Ex) &nbsp;<a href="https://black.readthedocs.io">black</a>, &nbsp;<code>pip install black</code>
        <a href="#formatting-ref" title="Return">↩</a>
      </li>
    </ul>
  </li>
  <p style='margin-top: 0.5em; margin-bottom: 0.5em'></p>
  <li id="footnote-testing"><code>unittest</code> 가 Standard Python Test Package
    <ul>
      <li style='margin-bottom: 0.35em'>하지만, &nbsp;대부분의 Python Developer 는 <a href="https://docs.pytest.org">pytest</a> 사용</li>
      <li style='margin-bottom: 0.35em'>Ex) <code>pip install pytest</code>
        <a href="#testing-ref" title="Return">↩</a>
      </li>
    </ul>
  </li>
  <p style='margin-top: 0.5em; margin-bottom: 0.5em'></p>
  <li id="footnote-source"><a href="https://git-scm.com/docs">Git</a> 이 현재 가장 보편적인 시스템
    <ul>
      <li><a href="https://docs.github.com/ko">Github</a> & <a href="https://gitlab-docs.infograb.net/">GitLab</a> 등의 Platform 에서 Git Storage Hosting</li>
      <li>All Programming Languages 에 &nbsp;사용 가능
        <a href="#source-ref" title="Return">↩</a>
      </li>
    </ul>
  </li>
  <p style='margin-top: 0.5em; margin-bottom: 0.5em'></p>
  <li id="footnote-ci"><b>pre-commit</b>
    <ul>
      <li>Local 에서 Commit 전 Test 실행 가능</li>
      <li>Ex) &nbsp;<a href="https://black.readthedocs.io">black</a>, &nbsp;<a href="https://docs.pytest.org">pytest</a>
      <li>Remote Repository 에 Push 후 추가 <b>CI</b> Test 가능
        <a href="#ci-ref" title="Return">↩</a>
      </li>
    </ul>
  </li>
</ol>
