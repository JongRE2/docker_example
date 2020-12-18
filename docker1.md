### Container 실행하기

[ ]의미 :  써도 되고 안써도 된다는 의미임.

```terminal
docker run [option] IMAGE[:TAG|@DIGEST] [COMMAND] [ARG...]

옵션제거하고 간략하게 보면은
docker run IMAGE
```



docker run에서 자주사용하는 옵션.

| 옵션   | 설명                                               |
| ------ | -------------------------------------------------- |
| -d     | background mode                                    |
| -p     | host와 container의 port를 연결(포워딩)             |
| -v     | host와 container의 directiory를 연결(마운트)       |
| -e     | container내에서 사용할 환경변수를 설정             |
| --name | container의 이름 설정                              |
| --rm   | process종료 시 container자동 제거                  |
| --it   | -i과 -t를 동시에 사용한것. 터미널 입력을 위한 옵션 |





### Image로 Container를 생성하기!!

```
docker run 이미지이름
//run다음에 입력한 이미지이름이 있으면 이 이미지로 컨테이너를 생성하고,
만약에 이미지가 없다면 도커허브에서 해당 이미지이름의 자료가 있는지 자동으로 찾아본다.
```





### 중지되어있는 컨테이너 시작하기

```
docker start [options] CONTAINER [CONTAINER...]
```

| Name, shorthand      | Default | Description                                                  |
| -------------------- | ------- | ------------------------------------------------------------ |
| `--attach , -a`      |         | Attach STDOUT/STDERR and forward signals                     |
| `--checkpoint`       |         | [**experimental (daemon)**](https://docs.docker.com/engine/reference/commandline/dockerd/#daemon-configuration-file) Restore from this checkpoint |
| `--checkpoint-dir`   |         | [**experimental (daemon)**](https://docs.docker.com/engine/reference/commandline/dockerd/#daemon-configuration-file) Use a custom checkpoint storage directory |
| `--detach-keys`      |         | Override the key sequence for detaching a container          |
| `--interactive , -i` |         | Attach container’s STDIN                                     |





## Container 중지하기(stop)

```bash
docker stop [OPTIONS] CONTAINER [CONTAINER...]

docker ps # 컨테이너 ID 정보 확인
docker stop ${UBUNTU_CONTAINER_ID}
docker ps -a # 중지되었나 확인
```







## Container 제거하기(rm)

```bash
docker rm [OPTIONS] CONTAINER [CONTAINER...]

docker ps -a # 컨테이너 ID 정보 확인
docker rm ${UBUNTU_CONTAINER_ID} ${MARIA_CONTAINER_ID}
docker ps -a # 삭제되었나 확인

# 중지된 모든 컨테이너 삭제
docker rm -v $(docker ps -a)
```







## 이미지 목록 확인하기(images)

```bash
docker images [OPTIONS] [REPOSITORY[:TAG]]
# 이미지 확인하기
docker images
```





### Dockfile만들기

Dockfile만들때 알아야할 내용

코드 RUN 1개의 줄이 docker이미지상의 레이어 하나이다. 그래서 최대한 RUN을 여러개 합쳐서 하는게 좋다.

WORKDIR 은 내가 컨테이너를 켰을때(RUN했을때) 이제 내가 들어가있을 경로를 지정하는거다.

CMD ~~는 말그대로 커멘드로서 ~~컨테이너안에서 실행되게 한다는 의미다.

EXPOSE는 포트를 지정해주는 명령어다.

## (예시) Openjdk image 사용

```docker
# Dockerfile

FROM openjdk:8
COPY . /usr/src/myapp    //현재경로(.)를 복사해서 컨테이너안의 경로인 /usr/src/myapp 에다가 복사.
WORKDIR /usr/src/myapp
RUN javac Hello.java	 //자바에서 Hello.java를 컴파일하는 명령
CMD ["java", "Hello"]	 //빌드 하는 명령

// COPY A B 의미 : A의 경로를 복사해서 B(보통 컨테이너안의경로)의 경로
```

## (예시) Ubuntu base image 이용해 제작



