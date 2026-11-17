# 개발 작업 환경 구축 (Development Workstation Setup)

## 1. 프로젝트 소개

이번 프로젝트에서는 macOS 환경에서 개발에 필요한 기본 도구를 설치하고 사용하는 방법을 실습하였다.

터미널을 이용한 파일 및 폴더 관리부터 Docker를 활용한 컨테이너 실행, 웹 서버 구축, 데이터 저장 방식까지 경험하였다.

마지막으로 Git과 GitHub를 연동하여 프로젝트 파일과 작업 기록을 관리하였다.

**주요 실습 내용**
- 터미널 기본 명령어 및 파일 관리
- 파일과 폴더 권한 변경
- Docker 이미지와 컨테이너 관리
- NGINX 웹 서버 실행 및 포트 연결
- Bind Mount와 Docker Volume 실습
- Git 및 GitHub를 이용한 버전 관리

## 2. 개발 환경

| 구분 | 사용 환경 |
|---|---|
| 운영체제 | macOS |
| 컴퓨터 | MacBook Air (Apple Silicon) |
| 터미널 | zsh |
| 컨테이너 실행 환경 | OrbStack |
| 컨테이너 관리 도구 | Docker |
| 버전 관리 도구 | Git |
| 원격 저장소 | GitHub |

## 3. 프로젝트 폴더 구성

```text
dev-workstation/
├── app/                  # 웹 서버 관련 파일
├── screenshots/          # 실습 과정 및 결과 캡처
├── Dockerfile            # Docker 이미지 빌드 설정
├── compose.yaml          # Docker Compose 설정
└── README.md             # 프로젝트 설명 및 실습 기록
```

각 폴더와 파일을 목적에 맞게 구분하여 관리하였다.

## 4. 터미널 기본 명령어 실습

터미널에서 파일과 폴더를 직접 생성하고 관리하는 방법을 실습하였다.

| 명령어 | 기능 |
|---|---|
| `pwd` | 현재 작업 위치 확인 |
| `ls` | 파일 및 폴더 목록 확인 |
| `mkdir` | 새 폴더 생성 |
| `touch` | 새 파일 생성 |
| `cp` | 파일 복사 |
| `mv` | 파일 이동 및 이름 변경 |
| `rm` | 파일 삭제 |
| `cat` | 파일 내용 확인 |
| `chmod` | 파일 및 폴더 권한 변경 |

### 권한 변경 실습

`chmod` 명령어를 이용하여 파일과 폴더의 접근 권한을 변경하였다.

```bash
chmod 600 practice/memo.txt
chmod 644 practice/memo.txt
chmod 700 practice
chmod 755 practice
```

권한 변경 후 `ls -l` 명령어를 이용하여 실제 변경 여부를 확인하였다.

**실습 결과:** 파일과 폴더의 권한을 직접 변경하고, 소유자 및 다른 사용자의 접근 권한이 달라지는 것을 확인하였다.

## 5. Docker 설치 및 기본 실습

OrbStack을 실행한 후 Docker 명령어를 이용하여 컨테이너 환경을 확인하였다.

### Docker 실행 상태 확인

```bash
docker --version
docker info
```

- `docker --version`: 설치된 Docker 버전 확인
- `docker info`: Docker 엔진의 실행 상태와 환경 정보 확인

### Hello World 컨테이너 실행

```bash
docker run hello-world
```

Docker의 기본 동작을 확인하기 위해 Hello World 이미지를 실행하였다.

**실습 결과:** `Hello from Docker!` 메시지가 출력되어 Docker 컨테이너가 정상적으로 실행되는 것을 확인하였다.

### Ubuntu 컨테이너 실행

```bash
docker run -it ubuntu bash
```

Ubuntu 이미지를 이용하여 별도의 Linux 실행 환경에 접속하고 기본 명령어를 실습하였다.

## 6. Docker 이미지 및 컨테이너 관리

Docker 이미지와 컨테이너의 목록을 확인하고, 사용이 끝난 컨테이너를 정리하는 방법을 실습하였다.

### 이미지와 컨테이너 확인

```bash
docker images
docker ps
docker ps -a
```

- `docker images`: 저장된 이미지 목록 확인
- `docker ps`: 실행 중인 컨테이너 확인
- `docker ps -a`: 종료된 컨테이너까지 전체 확인

### 컨테이너 삭제

```bash
docker rm 컨테이너이름
```

실습이 종료된 컨테이너를 삭제하여 불필요한 자원을 정리하였다.

### 이미지 삭제

```bash
docker image rm 이미지이름
```

사용하지 않는 이미지의 삭제 방법을 확인하였다.

### 최종 정리 결과

실습 과정에서 종료된 컨테이너 6개를 삭제하였다.

최종적으로 다음 상태를 확인하였다.

- 실행 중인 컨테이너: 2개
- 보존한 이미지: 3개
- 유지한 볼륨: `my-web-data`

직접 빌드한 `my-web-image`와 실행 중인 컨테이너에서 사용하는 이미지는 보존하였다.

**실습 결과:** 컨테이너와 이미지의 목록을 확인하고, 종료된 컨테이너를 정리하는 방법을 익혔다.

## 7. Dockerfile 및 NGINX 웹 서버 구축

Dockerfile을 작성하여 NGINX 기반의 사용자 정의 이미지를 생성하고 웹 서버를 실행하였다.

### Dockerfile

```dockerfile
FROM nginx:alpine
COPY app/ /usr/share/nginx/html/
EXPOSE 80
```

- `FROM`: 사용할 기본 이미지 지정
- `COPY`: 웹 페이지 파일을 컨테이너 내부로 복사
- `EXPOSE`: 컨테이너가 사용할 포트 표시

### 이미지 빌드

```bash
docker build -t my-web-image .
```

작성한 Dockerfile을 기반으로 사용자 정의 이미지를 생성하였다.

### 웹 서버 실행

```bash
docker run -d --name my-web -p 8080:80 my-web-image
```

호스트 컴퓨터의 8080번 포트를 컨테이너의 80번 포트에 연결하여 웹 서버에 접근하도록 설정하였다.

**실습 결과:** 브라우저에서 로컬 주소를 통해 NGINX 웹 페이지가 출력되는 것을 확인하였다.

※ 실제 최종 실행 포트와 컨테이너 이름은 현재 Docker 설정에 맞춰 확인 후 수정한다.

## 8. Bind Mount 및 Docker Volume

컨테이너와 외부 저장 공간을 연결하는 두 가지 방법을 실습하였다.

### 8-1. Bind Mount

Bind Mount는 호스트 컴퓨터의 특정 폴더와 컨테이너 내부 폴더를 연결하는 방식이다.

**실습 목적:** 로컬 HTML 파일을 수정했을 때 컨테이너 내부 웹 페이지에도 변경 사항이 반영되는지 확인한다.

**실습 결과:** 로컬 파일을 수정한 뒤 브라우저에서 변경된 내용이 반영되는 것을 확인하였다.

### 8-2. Docker Volume

Docker Volume은 컨테이너와 별도로 데이터를 저장할 수 있는 공간이다.

**실습 목적:** 컨테이너가 삭제되어도 별도로 연결된 데이터 저장 공간이 유지되는지 확인한다.

```bash
docker volume ls
```

위 명령어로 생성된 볼륨 목록을 확인하였다.

**실습 결과:** `my-web-data` 볼륨이 존재하는 것을 확인하였다. 볼륨은 컨테이너와 별도로 관리되므로 컨테이너 삭제와 구분하여 관리하였다.

## 9. Docker Compose를 이용한 컨테이너 통합 관리(보너스 과제)

Docker Compose는 여러 개의 Docker 컨테이너를 하나의 YAML 설정 파일로 정의하고 관리할 수 있는 도구이다.

본 프로젝트에서는 `compose.yaml` 파일을 작성하여 NGINX 웹 서버와 Ubuntu 컨테이너를 함께 관리하도록 설정하였다.

### 주요 설정

- `services`: 실행할 서비스 정의
- `image`: 사용할 Docker 이미지 지정
- `ports`: 호스트와 컨테이너의 포트 연결
- `environment`: 컨테이너에 전달할 환경변수 설정
- `command`: 컨테이너 실행 시 수행할 명령어 지정

### 주요 명령어

\```bash
docker compose up -d
docker compose ps
docker compose logs
docker compose stop
docker compose down
\```

- `up -d`: 정의된 서비스 실행
- `ps`: 서비스 실행 상태 확인
- `logs`: 서비스 실행 로그 확인
- `stop`: 실행 중인 서비스 중지
- `down`: 컨테이너 및 기본 네트워크 정리

### 실습 결과

하나의 `compose.yaml` 파일에서 NGINX와 Ubuntu 서비스를 정의하고 Docker Compose 명령어를 통해 여러 컨테이너를 통합 관리하는 방법을 익혔다.

## 10. Git 및 GitHub 연동

Git을 이용하여 프로젝트의 변경 이력을 관리하고 GitHub 원격 저장소에 업로드하였다.

### 주요 명령어

```bash
git init
git add .
git commit -m "Initial commit"
git remote add origin 저장소주소
git push -u origin main
```

- `git init`: 로컬 Git 저장소 생성
- `git add`: 변경된 파일을 커밋 대상으로 지정
- `git commit`: 현재 작업 내용 저장
- `git remote add origin`: GitHub 원격 저장소 연결
- `git push`: 로컬 프로젝트를 GitHub에 업로드

**GitHub 저장소:**  
https://github.com/juju1105/dev_workstation

**실습 결과:** Git을 이용해 작업 이력을 관리하고 GitHub에 프로젝트 파일을 업로드하였다.

## 11. 오류 해결 과정

### 문제 1. GitHub 저장소 연결 오류

**문제:**  
`git push -u origin main` 실행 시 Repository not found 오류 발생

**원인:**  
원격 저장소 주소가 올바르게 설정되지 않았다.

**해결 방법:**

```bash
git remote set-url origin https://github.com/juju1105/dev_workstation.git
git remote -v
git push -u origin main
```

**결과:**  
올바른 저장소 주소로 수정한 후 GitHub에 정상적으로 업로드하였다.

### 문제 2. Docker 이미지 빌드 오류

**문제:**  
`docker build` 명령어 실행 중 이미지 빌드 오류 발생

**원인:**  
Dockerfile의 명령어, 파일 경로 또는 빌드 대상 폴더 설정에 문제가 있을 가능성이 있었다.

**해결 방법:**

1. Dockerfile의 명령어 확인
2. HTML 파일의 실제 위치 확인
3. Dockerfile이 있는 프로젝트 폴더로 이동
4. 빌드 명령어 재실행

```bash
docker build -t my-web-image .
```

**결과:**  
이미지 빌드에 성공하고 NGINX 웹 서버를 실행하였다.

### 문제 3. Docker 엔진 연결 오류

**문제:**  
Docker 명령어 실행 시 Docker API 연결 실패 오류 발생

**원인:**  
OrbStack이 실행되지 않아 Docker 엔진에 연결할 수 없었다.

**해결 방법:**

1. OrbStack 실행
2. Docker 엔진 실행 상태 확인
3. `docker --version` 실행
4. `docker ps -a`로 연결 상태 확인

**결과:**  
OrbStack을 실행한 후 Docker 명령어가 정상적으로 작동하였다.

## 12. 최종 실습 결과 및 느낀 점

이번 프로젝트를 통해 개발 환경을 구성하는 데 필요한 기본적인 명령어와 도구의 사용 방법을 익힐 수 있었다.

특히 Docker를 이용해 이미지를 생성하고 컨테이너를 실행하는 과정에서 이미지와 컨테이너의 차이를 이해할 수 있었다.

또한 Bind Mount와 Volume을 직접 실습하면서 호스트 컴퓨터와 컨테이너 간의 파일 공유 방식, 컨테이너와 별도로 데이터를 보존하는 방식의 차이를 확인하였다.

마지막으로 Git과 GitHub를 연동하여 작업 내용을 기록하고 원격 저장소에 관리하는 방법을 익혔다.

단순히 명령어를 실행하는 것에서 그치지 않고, 실행 결과를 확인하고 발생한 오류를 해결하는 과정을 통해 개발 환경 관리의 기본적인 흐름을 경험할 수 있었다.

## 13. 실습 스크린샷

각 실습 과정에서 실행한 명령어와 결과를 `screenshots` 폴더에 저장하였다.

- 터미널 기본 명령어 및 권한 변경
- Docker 설치 및 기본 실행
- Ubuntu 컨테이너 실행
- Docker 이미지 및 컨테이너 관리
- NGINX 웹 서버 실행 및 접속
- Bind Mount 및 Volume 실습
- Git 및 GitHub 연동
- 오류 해결 과정
