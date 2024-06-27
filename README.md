Pintos UTSC edition [링크](https://thierrysans.me/CSCC69/projects/WWW/pintos.html#SEC_Top)

## 개발 환경 설정
1. VirtualBox 설치 [링크](https://www.virtualbox.org/wiki/Downloads)
2. Ubuntu Desktop 설치 [링크](https://ubuntu.com/download)
3. Docker Engine 설치 [링크](https://docs.docker.com/engine/install/ubuntu/)
    - 설치 방법 중에 "Install using the apt repository" 사용
4. Visual Studio Code 설치
    - Extensions
        - C/C++ Extension Pack
        - Docker
        - Remote Development
5. "pintos" directory 생성
    - mkdir pintos
5. pintos source clone
    - git clone https://github.com/ThierrySans/CSCC69-Pintos .
6. docker-compose.yaml 생성
    - pintos 폴더에 생성
    ```yaml
    services:
        dev:
            image: thierrysans/pintos
            container_name: pintos
            volumes:
                # same as '-v' option in docker
                - .:/pintos
            working_dir: /pintos
            hostname: pintos
            # same as '-it'
            tty: true
            # the container starts with bash
            entrypoint: bash
    ```
7. docker container 실행
    - docker-compose.yaml 파일이 있는 디렉토리에서 "docker compose up -d" 입력
8. attach visual studio
    - visual studio code에서 docker extension으로 가면 pintos container가 있다.
    해당 컨테이너를 마우스 오른쪽으로 클릭하면 attach visual studio 메뉴가 있고
    이것을 클릭하면 visual studio code가 하나 더 실행되면서 pintos container와 연결된다.
9. open folder (attached visual studio)
    - /pintos를 선택
10. visual studio code extensions 설치 (attached visual studio)
    - C/C++ Extension Pack
    - Native Debug 

## 디버깅 환경 설정
1. "실행 및 디버깅" 메뉴를 선택하고 "create a launch.json" 링크를 클릭한다. (디버거는 아무거나 선택한다.)
2. launch.json 파일을 다음과 같이 작성한다.
    ```json
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Attach to Pintos",
            "type": "gdb",
            "request": "attach",
            "executable": "${workspaceFolder}/src/threads/build/kernel.o",
            "target": ":1234",
            "remote": true,
            "cwd": "${workspaceRoot}",
            "gdbpath": "/pintos/src/utils/pintos-gdb"
        }
    ]
    ```
