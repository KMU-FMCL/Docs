---
title: Directory
---

### 1. Directory
  - `pwd` : 현재 위치 확인
  - `cd`  : 이동
  - `ls`  : Directory 안 내용 출력
    - `ls -a` : 숨긴 파일 모두 출력
    - `ls -d` : Directory 자체의 정보 출력
    - `ls -i` : incode[^incode] 번호 출력
    - `ls -A` : `.`, `..`를 제외한 모든 목록 출력[^2]
    - `ls -F` : File 종류 표시[^3]
    - `ls -L` : Symbolic link 의 경우 원본 File 의 정보 출력
    - `ls -R` : 하위 Directory 의 목록 출력
  - `mkdir` : Directory 생성
    - `mkdir -p` : SubDirectory 를 계층적으로 생성할 때 중간 단계의 Directory 를 자동 생성
  - `rmdir` : Directory delete

[^incode]: File, Directory 에 관한 정보를 가지는 숫자
[^2]: File, Directory 의 이름 앞에 붙으면 Hidden File, Directory <br> - `.` : Current Directory <br> - `..` : Parent Directory
[^3]: `/` : Directory <br> `*` : 실행 가능한 File(executable) <br> `@` : 바로가기(Symbolic link) <br> `|` : AND(Pipe)

