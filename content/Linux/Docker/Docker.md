---
title: Docker
tag: Linux
---

## Docker

### Image

- 타 개발자 및 기업들이 배포하는 Docker Image 는 기본적으로 Root 권한
- Ubuntu Desktop 사용 시 사용하는 건 User 권한, &nbsp;고로 Container 에서 Host Computer 로 건네받을 시 여러 권한문제가 발생하게 됨

  - 이를 해결하기 위해선 user 권한으로 작동하도록 dockerfile 작성 후 빌드 후 사용 & `apt install sudo` 와 `adduser` 를 통해 User 권한으로 사용 <br><br>

- 현재 연구실의 Dockerfile 을 사용하고 싶다면 아래의 이미지를 활용할 것<br>(단 Pytorch & Tensorflow 같은 딥러닝 라이브러리를이 설치되지 않았으므로 주의 요망)
  ```zsh
  docker pull taehun3446/setup:user
  ```

### Container

- Oh My Zsh 의 docker plugin 적용 X

  ```zsh
  docker run -it --rm --gpus all -v /tmp/.X11-unix:/tmp/.X11-unix -e DISPLAY=unix$DISPLAY {docker image}
  ```

<br>

- Oh My Zsh 의 docker plugin 적용 O
  ```zsh
  drit --rm --gpus all -v /tmp/.X11-unix:/tmp/.X11-unix -e DISPLAY=unix$DISPLAY {docker image}
  ```
