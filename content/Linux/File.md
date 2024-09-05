---
titel: File
---

### 2. File
  - `cat` : File 의 내용 출력
    - `cat -n` : Row number 붙여 출력
  - `more` : File 의 내용을 화면 단위로 출력
    - `more +number` : 출력을 시작할 Row number 를 지정
  - `less` : File 의 내용을 화면 단위로 출력[^4]
  - `head` : File 의 1 ~ n Row 까지 출력
    - `head -Line` : 출력할 Row 수를 지정
  - `cp` : File 이나 Directory 복사
    - `cp -r` : SubDirectory & Subfile 까지 모두 복사
    - `cp -v` : 복사 진행 상태 출력
    - `cp -p` : File or Directory 를 복사할 때 복사 대상의 User, Group, Permissions
    - `cp -i` : 복사 대상 File 이 이미 해당 위치에 있다면 User 한테 Overdrive 여부 묻고 복사
    - `cp -f` : 복사 대상 File 이 이미 해당 위치에 있다면 File 을 지우고 강제로 복사
  - `rm` : File 이나 Directory delete
    - `rm -i` : User 한테 여부 묻고 delete
  - `ln` : File link 생성
    - `ln -s` : Symbolic link file 생성
  - `touch` : Empty file 생성
  - `greb` : (File 내 search) 지정한 Pattern 포함된 Line 찾기 &nbsp; Ex) `grep [option][pattern][file]`
    - `grep -c` : 일치하는 Row 의 수 출력
    - `grep -i` : 대소문자 구별 X
    - `grep -v` : 일치ㅏ하지 않는 Row 만 출력
    - `grep -n` : 포함된 Row number 함께 출력
    - `grep -l` : Pattern 이 포함된 File name 출력
    - `grep -w` : Word 와 일치하는 Row 만 출력
    - `grep -x` : Line 과 일치하는 Row 만 출력
    - `grep -r` : SubDirectory 를 포함한 모든 File 에서 search
    - `grep -m number` 최대로 표시될 수 있는 결과를 제한
    - `grep -E` : 찾을 pattern 을 정규 포현식으로 찾기
    - `grep -F` : 찾을 pattern 을 String 으로 찾기
  - `find` : 지정한 Path 에서 Search 조건에 맞는 File 찾기 &nbsp; Ex) `find [option][path][expressions]`[^expressions]
    - `find -P` : Symbolic link 를 따라가지 않고, Symbolic link 자체 정보 사용
    - `find -L` : Symbolic link 에 연결된 File 정보 사용
    - `find -D` : Debug message 출력
  - `whereis` : 지정된 Path 에서 Command 의 Binary file 이나 Maual file 의 위치를 찾음
    - `whereis -b` : Binary file 만 Search
    - `whereis -m` : Maual file 만 Search
    - `whereis -s` : Source file 만 Search

[^4]: `j` : Down key <br> `k` : Up key <br> `space bar, Ctrl + f` : 다음 Page 이동<br> `\string` : 해당 String 찾기 <br> `q` : 종료
[^expressions]: `name` : 해당 이름의 File을 찾음(Regex 사용 O) <br> `type` : 지정된 File type 에 해당하는 Search for file <br> `user` : 해당 User 에게 속한 Search for file <br> `empty` : Empty directory 혹은 크기가 0인 Search for file <br> `delete` : Search된 File 혹은 Directory delete <br> `exec` : Search된 File 에 대해 지정된 Command 실행 <br> `path` : 지정된 String pattern 에 해당하는 Path 에서 Search <br> `print` : Search 결과를 출력, Search 항목을 `newline` 으로 구분(Default) <br> `print0` : Search 결과를 출력, Search 항목을 `null` 로 구분 <br> `size` : File size 를 사용 하여 Search for file <br> `mindepth` : Search 을 시작할 SubDirectory 최소 Depth 지정 <br> `maxdepth` : Search 할 SubDirectory 의 최대 Depth 지정 <br> `atime` : n 일 이내에 Acess 된 File 찾음 <br> `ctime` : n 일 이내에 만들어진 File 찾음 <br> `mtime` : n 일 이내에 수정된 File 을 찾음 <br> `cnewer file` : 해당 File 보다 최근에 수정된 File 을 찾음

