
# Docker에서 MySQL 설정하기

## Docker 설치

Docker는 각 운영 체제에 따라 설치 방법이 다릅니다. [Docker 공식 웹사이트](https://docs.docker.com/get-docker/)에서 관련 지침을 찾을 수 있습니다.

## MySQL Docker 이미지 다운로드

Docker Hub에서 MySQL 이미지를 다운로드하려면 다음 명령을 실행합니다:

```bash
docker pull mysql
```

이 명령은 MySQL의 최신 버전 이미지를 다운로드합니다. 특정 버전을 원할 경우 `mysql:<tag>` 형식으로 태그를 지정할 수 있습니다.

## MySQL 컨테이너 실행

MySQL 컨테이너를 실행하는 기본 명령은 다음과 같습니다:

```bash
docker run --name some-mysql -e MYSQL_ROOT_PASSWORD=my-secret-pw -d mysql
```

- `--name some-mysql`: 컨테이너의 이름을 설정합니다.
- `-e MYSQL_ROOT_PASSWORD=my-secret-pw`: `root` 사용자의 비밀번호를 설정합니다.
- `-d`: 컨테이너를 백그라운드에서 실행합니다.

## 데이터 저장을 위한 볼륨 사용

데이터를 영구적으로 보관하려면 Docker 볼륨을 사용하는 것이 좋습니다:

```bash
docker run --name some-mysql -e MYSQL_ROOT_PASSWORD=my-secret-pw -v my-db:/var/lib/mysql -d mysql
```

- `-v my-db:/var/lib/mysql`: `my-db` 볼륨을 컨테이너의 `/var/lib/mysql` 디렉터리에 연결합니다.

## 네트워크 포트 설정

외부에서 MySQL 서버에 접근하려면 포트를 매핑해야 합니다:

```bash
docker run --name some-mysql -e MYSQL_ROOT_PASSWORD=my-secret-pw -p 3306:3306 -d mysql
```

- `-p 3306:3306`: 호스트의 3306 포트와 컨테이너의 3306 포트를 연결합니다.

## MySQL 서버 접속

컨테이너에 접속하여 MySQL을 사용하려면 다음 명령을 사용합니다:

```bash
docker exec -it some-mysql mysql -u root -p
```

이 명령은 MySQL 프롬프트에 접근하게 하며, 로그인 시 설정한 비밀번호를 입력해야 합니다.

## Docker 컨테이너 관리

컨테이너를 중지, 시작, 재시작하는 명령은 다음과 같습니다:

- 컨테이너 중지: `docker stop some-mysql`
- 컨테이너 시작: `docker start some-mysql`
- 컨테이너 재시작: `docker restart some-mysql`

