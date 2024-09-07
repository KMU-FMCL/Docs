---
title: Docker
tag: Linux
---

## Docker

### Image

- 타 개발자 및 기업들이 배포하는 Docker Image 는 기본적으로 Root 권한
- Ubuntu Desktop 사용 시 사용하는 건 User 권한, &nbsp;고로 Container 에서 Host Computer 로 건네받을 시 여러 권한문제가 발생하게 됨

  - 이를 해결하기 위해선
    1. user 권한으로 작동하도록 dockerfile 작성 후 빌드 후 사용
    2. `apt install sudo`[^1], &nbsp;`adduser`[^2], &nbsp;`usermod -aG sudo {USER}`[^3], &nbsp;`su`[^4] Command 를 통해 User 권한으로 사용 <br><br>

- 현재 연구실의 Dockerfile 을 사용하고 싶다면 아래의 이미지를 활용할 것<br>(단 Pytorch & Tensorflow 같은 딥러닝 라이브러리를이 설치되지 않았으므로 주의 요망)
  ```zsh
  docker pull taehun3446/setup:user
  ```

### Container

- Oh My Zsh 의 **docker plugin**<sup><a href="https://github.com/ohmyzsh/ohmyzsh/blob/master/plugins/docker/README.md"></a></sup> 적용 X

  ```zsh
  docker run -it --rm --gpus all -v /tmp/.X11-unix:/tmp/.X11-unix -e DISPLAY=unix$DISPLAY {docker image}
  ```

<br>

- Oh My Zsh 의 **docker plugin**<sup><a href="https://github.com/ohmyzsh/ohmyzsh/blob/master/plugins/docker/README.md"></a></sup> 적용 O

  ```zsh
  drit --rm --gpus all -v /tmp/.X11-unix:/tmp/.X11-unix -e DISPLAY=unix$DISPLAY {docker image}
  ```

  [^1]: Docker Container 안에서 apt 를 통하여 설치하고자 한다면 항상 우선적으로 `apt update` 실시하는 걸 잊지 말 것<br>Docker Image 는 용량 절감을 위해 항상 `rm -rf /var/lib/apt/lists/*` 로 APT 패키지 관리자의 캐시된 패키지 목록을 삭제한 상태이기 때문

  [^2]: User Add

  [^3]: `sudo` Command 를 사용할 수 있도록 Group 에 Add

  [^4]: User Change
