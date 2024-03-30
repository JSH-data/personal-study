### 이미지를 빌드하기
- 이미지를 빌드하기 위해서는 일련의 과정이 반드시 필요합니다. 
- 도커는 이러한 일련의 과정을 손쉽게 기록하고 수행할 수 있는 빌드 명령어를 제공합니다.
- 완성된 이미지를 생성하기 위해 컨테이너에 설치애햐하는 패키지 추가해야하는 소스코드 실행해야하는 명령어와 스크립트를 등을 하나의 파일에 기록해두면 도커는 이파일을 읽어 컨테이너에서 작업을 수행한 뒤 이미지로 만들어 냅니다.
- 이러한 작업을 기록한 파일의 이름을 Dockerfile이라 하며, 빌드 명령어는 Dockerfile을 읽어 이미지를 생성합니다
- 이미지를 자체 배포하는 대신 Dockerfile을 배포할 수 있기 때문에 애플리케이션에 필요한 패키지 설치등을 명확히 할 수 있고 이미지 생성을 자동화할 수 있으며 쉽게 배포할 수 있습니다.

##### Dockerfile 에시
```docker
FROM ubuntu:14.04
LABEL "perpose"="practice"
RUN apt-get update
RUN apt-get install apache2 -y
ADD test.html /var/www/html
WORKDIR /var/www/html
RUN ["/bin/bash", "-c", "echo hello >> test.html"]
EXPOSE 80
CMD apachect1 -DFOREGROUND
```

##### Dockerfile 명령어
- **FROM**: 이미지의 베이스가 될 이미지를 뜻합니다. 반드시 한번 이상 입력해야합니다.
- **LABEL**: 이미지에 메타 데이터를 추가합니다.
- **RUN**: 이미지를 만들기ㅣ위해 컨테이너 내부에서 명령어를 실행합니다. (Dockerfile의 일부 명령어는 JSON 배열의 형태로 사용할 수 있습니다)
- **ADD**: 파일을 이미지에 추가합니다. 추가하는 파일은 Dockerfile이 위치한 디렉터리인 컨텍스트에서 가져옵니다.

WORKDIR: 명령어를 실행할 디렉터리를 나타냅니다. cd와 같습니다.

EXPOSE: Dockerfile의 빌드로 생성된 이미지에서 노출할 포트를 설정합니다. 하지만 반드시 이 포트가 바인딩되는 것은 아니며 단지 컨테이너의 80번 포트를 사용할 것 임을 타나내는 것뿐입니다.

CMD: 컨테이너가 시작될 때마다 실행할 명령어를 설정하며 Dockerfile에서 한 번만 사용할 수 있습니다. docker run 시 CMD를 사용하는경우 덮어씌우게 됩니다.

도커 빌드

```docker
docker build -t mybuild:0.0 ./
```

-t: 생성될 이미지의 이름을 설정합니다.

빌드 결과물 실행

```docker
docker run -d -P --name myserver mybuild:0.0
```

-P: EXPOSE의 모든 포트를 호스트에 연결

—filter 옵션을 통해 해당 라벨을 가지는 이미지를 출력할 수 있습니다.

```docker
docker images --filter "label=perpose=practice"
```

이미지 빌드를 시작하면 도커는 가장 먼저 빌드 컨텍스트를 읽어 들입니다. (Dockerfile이 위치한 디렉터리가 빌드 컨텍스트가 됩니다.)

빌드 컨텍스트는 Dockerfile에서 빌드될 이미지에 파일을 추가할 때 사용됩니다. ADD, COPY를 통해 빌드 컨텍스트의 파일을 이미지에 추가합니다.

.dockerignore 파일은 dockerfiler이 위한 경롸 같은 곳에 위치해야합니다. 

각 STEP은 Dockerfile에 기록된 명령어에 해당합니다. ADD, RUN등의 명령어가 실행될 때마다 새로운 컨테이너가 하나씩 생성되며 이를 이미지로 커밋합니다. 즉, 명령어 한 줄이 실행될 떄마다 이전 Step에서 생성된 이미지에 의해 새로운 컨테이너가 생성되ㅕ, Dockerfile에 적힌 명령어를 수행하고 다시 새로운 이미지 레이어로 저장됩니다. 

이미지 빌드가 완료되면 Dockerfiel의 명령어 줄 수만큼의 레이어가 존재하게 되며 중간에 컨테이너도 같은 수만큼 생성되고 삭제됩니다. 

한번 이미지를 빌드를 마치고 난 뒤 다시 같은 빌드를 진행하면 이전의 이미지 빌드에서 사용했던 캐시를 사용합니다. 

이미지 빌드 중 오류가 발생하는 경우 build 명령어가 중지되며 임시 컨테이너가 삭제되지 않은 채로 남게 됩니다. <none>:<none>으로 이미지가 생성됩니다. rmi 명령어에 docker images의 출력 결과에서 확인할 수 있는 이미지의 ID를 입력합니다. 

git을 pull 받는 경우 캐시로 인하여 업데이트 사항이 받아지지 않을 수 있기 때문에 --no-cache 옵션을 추가합니다. 

