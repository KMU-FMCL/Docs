---
title: Directory structure
tag: OS/Linux
---

- Linux 는 Unix 와 마찬가지로 **모든 대상들을 파일로 관리**
- Directory file 들을 관리하기 위해 계층적으로 구성하며 이를 Tree structure
- 모든 Directory 의 **최상의 Directory 를 Root directory(`/`)**

<table>
  <tr>
    <th style='text-align: center'>Directory Location</th>
    <th style='text-align: center'>Directory Name</th>
    <th style='text-align: center'>Features</th>
  </tr>
  <tr>
    <td style='text-align: center'><b>/</b></td>
    <td style='text-align: center'><b>/</b></td>
    <td><ul><li>모든 Directory 의 최상의 Directory</li></ul></td>
  <tr>
  <tr>
    <td style='text-align: center'><b>/bin</b></td>
    <td style='text-align: center'><b>bin</b></td>
    <td><ul><li><b>Default command 가 저장</b>된 Directory</li><li><b>자주 사용되는 Command</b> 들이 해당 Directory 에 저장</li></ul></td>
  </tr>
  <tr>
    <td style='text-align: center'><b>/boot</b></td>
    <td style='text-align: center'><b>boot</b></td>
    <td><ul><li>리눅스의 부팅에 필요한 Information 을 가진 File 들이 저장된 Directory</li></ul></td>
  </tr>
  <tr>
    <td style='text-align: center'><b>/dev</b></td>
    <td style='text-align: center'><b>dev</b></td>
    <td><ul><li><b>시스템 장치 File 을 저장</b>하고 있는 Directory</li><li><b>물리적 장치들이 File 형식으로 저장되어 있음</b></li></ul></td>
  </tr>
  <tr>
    <td style='text-align: center'><b>/etc</b></td>
    <td style='text-align: center'><b>etc</b></td>
    <td><ul><li>Linux 의 Preferences file 이 저장된 Directory</li></ul></td>
  </tr>
  <tr>
    <td style='text-align: center'><b>/home</b></td>
    <td style='text-align: center'><b>home</b></td>
    <td><ul><li><b>User 의 Home directory 가 존재</b>하는 곳</li><li>User를 추가할 때 마다 User ID 명과 동일한 Directory 가 생성된</li></lu></td>
  </tr>
  <tr>
    <td style='text-align: center'><b>/lib</b></td>
    <td style='text-align: center'><b>lib</b></td>
    <td><ul><li>Kernel 이 필요로 하는 Libaray, Kernel Module file 이 존재하는 Directory</li></ul></td>
  </tr>
  <tr>
    <td style='text-align: center'><b>/media</b></td>
    <td style='text-align: center'><b>media</b></td>
    <td><ul><li>외부 기억장치들의 Mount 연결 시 사용되는 Directory</li></ul></td>
  </tr>
  <tr>
    <td style='text-align: center'><b>/mnt</b></td>
    <td style='text-align: center'><b>mnt<b></td>
    <td><ul><li>사용자가 직접 외부 장치들을 Mount 할 때 사용되는 Directory</li></ul></td>
  </tr>
  <tr>
    <td style='text-align: center'><b>/opt</b></td>
    <td style='text-align: center'><b>opt</b></td>
    <td><ul><li>추가 응용 프로그램 Package 가 설치되는 Directory</li></ul></td>
  </tr>
  <tr>
    <td style='text-align: center'><b>/proc</b></td>
    <td style='text-align: center'><b>proc</b></td>
    <td><ul><li>최상위 Root directory 와 전혀 다른 directory</li><li><b>관리자 계정 root 의 Home directory</b></li></td>
  </tr>
  <tr>
    <td style='text-align: center'><b>/sbin</b></td>
    <td style='text-align: center'><b>sbin</b></td>
    <td><ul><li>System Binary file, ifconfig, ethtool 와 같은 System commands 을 저장하고 있는 Directory</li></ul></td>
  </tr>
  <tr>
    <td style='text-align: center'><b>/usr</b></td>
    <td style='text-align: center'><b>usr</b></td>
    <td><ul><li>Nomal User 들이 사용하는 Directory</li></ul></td>
  </tr>
  <tr>
    <td style='text-align: center'><b>/var</b></td>
    <td style='text-align: center'><b>var</b></td>
    <td><ul><li><b>Log file 수집</b>, Database Caching file, Web Server image 등 다양한 File 이 존재하는 Directory</li></ul></td>
  </tr>
  <tr>
    <td style='text-align: center'><b>/sys</b></td>
    <td style='text-align: center'><b>sys</b></td>
    <td><ul><li>Device 를 관리하기 위한 Virtual File System Directory</li></ul></td>
  </tr>
  <tr>
    <td style='text-align: center'><b>/run</b></td>
    <td style='text-align: center'><b>run</b></td>
    <td><ul><li>실행 환경 변수(Run-time variable)를 관리하는 Directory</li><li>부팅한 후의 System Information 을 관리하는 Directory</li></ul></td>
  </tr>
  <tr>
    <td style='text-align: center'><b>/tmp</b></td>
    <td style='text-align: center'><b>tmp</b></td>
    <td><ul><li>임시 File 을 저장하기 위한 Directory</li></ul></td>
  </tr>
  <tr>
    <td style='text-align: center'><b>/lost + found</b></td>
    <td style='text-align: center'><b>lost + found</b></td>
    <td><ul><li>Trash 와 같은 개념으로, 삭제된 File 이 저장된 Directory</li></ul></td>
  </tr>
</talbe>
