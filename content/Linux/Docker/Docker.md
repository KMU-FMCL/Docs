---
title: Docker
tag: OS/Linux
---

## Docker

### Image

- 타 개발자 및 기업들이 배포하는 Docker Image 는 기본적으로 Root 권한
- Ubuntu Desktop 사용 시 사용하는 건 User 권한, &nbsp;고로 Container 에서 Host Computer 로 여러 Data & GUI 를 건네받을 시 여러 권한문제가 발생하게 됨

  - 이를 해결하기 위해선
    1. user 권한으로 작동하도록 dockerfile 작성 후 빌드 후 사용
    2. `apt install sudo`[^1], &nbsp;`adduser`[^2], &nbsp;`usermod -aG sudo {User name}`[^3], &nbsp;`su`[^4] Command 를 통해 User 권한으로 사용 <br><br>

- 현재 연구실의 Dockerfile 을 사용하고 싶다면 아래의 이미지를 활용할 것<br>(단 Pytorch & Tensorflow 같은 딥러닝 라이브러리를이 설치되지 않았으므로 주의 요망)
  ```zsh
  docker pull taehun3446/setup:user
  ```

### Container

> [!Tip]
>
> > [!example] Oh My Zsh 의 <a href="https://github.com/ohmyzsh/ohmyzsh/blob/master/plugins/docker/README.md">docker plugin</a> 적용 X
> >
> > ```zsh
> > docker run -it --rm --gpus all -v /tmp/.X11-unix:/tmp/.X11-unix -e DISPLAY=unix$DISPLAY {docker image}
> > ```
>
> > [!example] Oh My Zsh 의 <a href="https://github.com/ohmyzsh/ohmyzsh/blob/master/plugins/docker/README.md">docker plugin</a> 적용 O
> >
> > ```zsh
> > drit --rm --gpus all -v /tmp/.X11-unix:/tmp/.X11-unix -e DISPLAY=unix$DISPLAY {docker image}
> > ```
>
> **Argument**
>
> - `-it`[^5]
>   - `-i` : 상호 Input/Output
>   - `-t` : **tty**[^6] 를 활성화하여 **Shell**[^7] 을 사용하도록 Container 에서 설정[^8] <p style='margin-top: 0.5em; margin-bottom: 0.5em'></p>
> - `--rm` : 접속 중인 **Shell** 종료 시 Container 바로 Delete <p style='margin-top: 0.5em; margin-bottom: 0.5em'></p>
> - `--gpus all` : Container 에서 Host 의 GPU 전체[^9]를 사용할 수 있게 함<sup><a href="https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/index.html"></a></sup>(`nvidia-smi`[^10] 로 확인 가능) <p style='margin-top: 0.5em; margin-bottom: 0.5em'></p>
> - `-v` : Host 의 Directory 를 Container 에 Mount 시킴 <p style='margin-top: 0.5em; margin-bottom: 0.5em'></p>
> - `-e` : Parameter 를 통해 Host 의 Environment Variable 를 Container 에 넘겨줌[^11]

[^1]: Docker Container 안에서 apt 를 통하여 설치하고자 한다면 항상 우선적으로 `apt update` 실시하는 걸 잊지 말 것<br>Docker Image 는 용량 절감을 위해 항상 `rm -rf /var/lib/apt/lists/*` 로 APT 패키지 관리자의 캐시된 패키지 목록을 삭제한 상태이기 때문

[^2]: User Add

[^3]: `sudo` Command 를 사용할 수 있도록 Group 에 Add

[^4]: User Conversion

[^5]: 이 Command 를 안써도 되지만 하나라도 쓰지 않을 경우 Shell 사용 불가

[^6]: User 와 Computer 가 상호작용하는 Text 기반의 Interface, &nbsp;Terminal

[^7]: User 가 Computer 가 상호작용할 수 있도록 Command 를 입력하고 그 결과를 출력하는 Program, &nbsp;Command Interpreter(Bash, Zsh, Fish)

[^8]: **tty**, &nbsp;**Shell** 서로 비슷해보이지만 다른 개념, &nbsp;이 점에 더 알고 싶다면 OS & Linux 를 공부해볼 것

[^9]: 단일 GPU 넘어서 다중 GPU 를 활용할 경우 Containers, &nbsp;Models 를 각 GPU 를 지정해서 실행 & 연산 가능

[^10]: Host 에 Nividia Driver & Nvidia Container Toolkit 을 설치하는 것을 잊지 말 것

[^11]: Docker 는 기본적으로 Terminal 기반으로 동작하기에 GUI 를 가지고 있지 않음, &nbsp;GUI 를 활용하기 위해선 필수
