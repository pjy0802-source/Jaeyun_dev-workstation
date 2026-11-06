# 코디세이 미션 1 기록

## 1. 실습 목표
개발 환경을 확인하고, 터미널에서 기본 파일/폴더 조작을 연습한 뒤, 리눅스에서 파일 권한을 변경하는 방법을 익힌다.

---

## 2. 환경 확인

아래 도구들이 설치되어 있는지 확인했다.

- Git: v2.56.0
- VS Code: v1.144.0
- Docker Desktop: v29.9.2
- WSL Ubuntu: v2
- PowerShell: 5.1

PowerShell 7은 설치되어 있지 않았지만, 이번 미션 진행에는 문제가 없었다.

---

## 3. PowerShell 파일/폴더 조작 실습

PowerShell에서 파일과 폴더를 직접 생성하고, 파일 내용을 확인하고, 내용을 추가하는 실습을 진행했다.

### 사용한 명령어
    New-Item sample-dir -ItemType Directory
    Get-Content sample.txt
    Set-Content sample.txt "첫 번째 줄"
    Add-Content sample.txt "두 번째 줄"

### 실습 결과
- `sample-dir` 폴더를 생성했다.
- `sample.txt` 파일의 내용을 확인했다.
- `Set-Content`로 첫 번째 줄을 작성했다.
- `Add-Content`로 두 번째 줄을 추가했다.
- `Get-Content`로 최종 내용을 확인했다.

---

## 4. Ubuntu 권한 실습

WSL Ubuntu 환경에서 파일과 디렉터리의 권한을 변경하고 확인하는 실습을 진행했다.

### 작업 위치
- `~/codyssey-practice/ubuntu-lab`

### 사용한 명령어
    chmod 644 sample.txt
    chmod 755 sample-dir
    ls -l

### 권한 변경 결과
- `sample.txt` 권한: `rw-r--r--` (644)
- `sample-dir` 권한: `rwxr-xr-x` (755)

### 실습 결과
- 파일과 디렉터리의 권한을 각각 원하는 값으로 변경할 수 있었다.
- `ls -l` 명령으로 권한이 반영되었는지 확인했다.

---

## 5. Docker 확인

Docker Desktop이 설치되어 있고 실행 가능한 상태임을 확인했다.

- Docker Desktop: v29.9.2

---

## 6. 실습을 통해 배운 점

- PowerShell에서는 `New-Item`, `Get-Content`, `Set-Content`, `Add-Content`를 사용해 파일과 폴더를 쉽게 다룰 수 있다.
- Ubuntu에서는 `chmod` 명령어로 파일과 디렉터리의 권한을 변경할 수 있다.
- `ls -l`을 사용하면 권한이 제대로 적용되었는지 확인할 수 있다.

---

## 7. 정리

이번 실습을 통해 기본적인 터미널 조작과 파일 권한 관리 방법을 익혔다.
앞으로도 명령어를 직접 실행해 보면서 리눅스와 터미널 사용에 더 익숙해질 수 있을 것 같다.
## 8. Docker 기본 실습
Docker의 기본 동작을 확인했다.

### 8-1. hello-world 컨테이너 실행
`hello-world` 이미지를 사용해 컨테이너 실행에 성공했다.

### 8-2. Ubuntu 컨테이너 실행
`ubuntu` 이미지를 사용해 컨테이너를 실행하고 내부에 진입했다.

예시 명령:
    docker run -it --name ubuntu-test ubuntu bash

컨테이너 내부에서 확인한 내용:
- `ls`로 기본 디렉터리 구조 확인
- `touch test2.txt`로 파일 생성
- 생성한 파일이 컨테이너 내부에 저장됨을 확인

## 9. Docker 컨테이너 생명주기 확인
컨테이너의 상태 변화를 직접 확인했다.

### 9-1. stop/start 후 파일 유지
컨테이너를 종료한 뒤 다시 시작해도 `test2.txt`가 유지되는 것을 확인했다.

명령:
    docker start ubuntu-test
    docker exec -it ubuntu-test bash

### 9-2. 컨테이너 삭제 후 파일 사라짐
컨테이너를 삭제한 뒤 새로 생성하면 `test2.txt`가 없어지는 것을 확인했다.

명령:
    docker rm -f ubuntu-test
    docker run -it --name ubuntu-test ubuntu bash

이 실습을 통해 다음을 확인했다.

- `stop/start`만 하면 컨테이너 내부 파일은 유지된다.
- `rm`으로 컨테이너를 삭제하면 기존 파일은 사라진다.

## 10. Docker exec와 attach 개념 정리
### `docker exec`
- 실행 중인 컨테이너 안에서 새 명령/새 프로세스를 실행한다.
- 보통 디버깅이나 점검할 때 많이 사용한다.
- `exit`하면 해당 exec 세션만 종료되고, 컨테이너 자체는 보통 계속 실행된다.

### `docker attach`
- 실행 중인 컨테이너의 기존 메인 프로세스에 연결한다.
- 컨테이너를 시작할 때 실행된 원래 프로세스와 직접 상호작용한다.
- `exit` 시 메인 프로세스가 종료되면 컨테이너도 종료될 수 있다.

### 차이점 요약
- `exec`는 새 프로세스 실행
- `attach`는 기존 프로세스 연결

## 11. 현재 상태
- Docker 기본 동작을 직접 실습했다.
- 컨테이너 생성, 시작, 종료, 삭제의 차이를 이해했다.
- `exec`와 `attach`의 개념 차이를 정리했다.

## Docker 운영 명령 실습

| 명령어 | 설명 | 결과 |
|--------|------|------|
| `docker ps` | 실행 중인 컨테이너 확인 | my-web 확인 |
| `docker ps -a` | 전체 컨테이너 확인 | 동일 |
| `docker images` | 이미지 목록 확인 | my-nginx:1.0 확인 |
| `docker logs my-web` | 컨테이너 로그 확인 | nginx 접속 기록 확인 |
| `docker stop my-web` | 컨테이너 중지 | 정상 중지 |
| `docker start my-web` | 컨테이너 재시작 | 정상 재시작 |
## 포트 매핑 확인
![포트 매핑 확인](images/port-mapping-8080.png)

## 📚 실습 진행 현황

### ✅ 완료
- [x] 환경 구성 (Git, Docker 설치 확인)
- [x] GitHub 저장소 연결
- [x] Dockerfile 작성 및 nginx 이미지 빌드
- [x] Docker 컨테이너 실행 및 운영 명령어
- [x] 바인드 마운트 실습 (실시간 파일 반영 확인)

### 🔄 진행 예정
- [x] Docker 볼륨(Volume) 실습
- [x] Docker Compose 실습
---

## 미션 2 - Docker Compose 실습

### 실습 날짜
2025-07-xx

### 구성 환경
- web : my-nginx:1.0 (포트 8080)
- redis : redis:alpine (포트 6379)

### 실습한 명령어

| 명령어 | 설명 |
|--------|------|
| docker compose up -d | 백그라운드 멀티 컨테이너 실행 |
| docker compose ps | 실행 중인 컨테이너 목록 확인 |
| docker compose pause | 프로세스 일시 동결 |
| docker compose unpause | 동결 해제 |
| docker compose stop | 컨테이너 중지 (삭제 안됨) |
| docker compose start | 중지된 컨테이너 재시작 |
| docker compose down | 컨테이너 + 네트워크 완전 삭제 |

### 핵심 개념
- pause : 메모리 유지, 프로세스만 동결
- stop  : 컨테이너 유지, 프로세스 종료
- down  : 컨테이너 + 네트워크 완전 삭제

### 결과
- localhost:8080 nginx 정상 확인
- redis + web 동시 운영 성공
## 3-2. PowerShell 터미널 기본 조작 실습

`mkdir`, `echo`, `cat`, `cp`, `mv`, `rm` 명령어를 사용해 파일과 폴더를 직접 조작하는 실습을 진행했다.

### 사용한 명령어

| 명령어 | 설명 | 결과 |
|--------|------|------|
| `pwd` | 현재 경로 확인 | `C:\Jaeyun_dev-workstation` |
| `ls -Force` | 숨김 파일 포함 목록 확인 | `.git` 포함 전체 구조 확인 |
| `mkdir test-dir` | 폴더 생성 | `test-dir` 생성 완료 |
| `echo "hello world" > test-dir/test.txt` | 파일 생성 및 내용 작성 | `test.txt` 생성 |
| `cat test-dir/test.txt` | 파일 내용 확인 | `hello world` 출력 |
| `cp test-dir/test.txt test-dir/test-copy.txt` | 파일 복사 | `test-copy.txt` 생성 |
| `mv test-dir/test-copy.txt test-dir/test-renamed.txt` | 파일 이름 변경 | `test-renamed.txt` 로 변경 |
| `rm test-dir/test-renamed.txt` | 파일 삭제 | `test-renamed.txt` 삭제 완료 |

### 실습 결과
- `test-dir` 폴더를 생성하고 파일을 만들어 내용을 확인했다.
- `cp`로 파일을 복사하고, `mv`로 이름을 변경했다.
- `rm`으로 파일을 삭제한 뒤 `ls`로 결과를 확인했다.
- 최종적으로 `test-dir` 안에 `test.txt` 만 남은 것을 확인했다.
## 미션 3 - Docker 커스텀 이미지 빌드

### 실습 날짜
2025-07-xx

### 실습 목표
Dockerfile을 직접 작성하여 커스텀 nginx 이미지를 빌드하고, 컨테이너로 실행해 브라우저에서 확인한다.

---

### 3-1. Dockerfile 작성

`my-nginx:1.0` 이미지를 만들기 위해 아래 Dockerfile을 작성했다.

```dockerfile
FROM nginx:latest
COPY index.html /usr/share/nginx/html/index.html
3-3. 이미지 빌드 및 컨테이너 실행
명령어	설명	결과
docker build -t my-nginx:1.0 .	커스텀 이미지 빌드	my-nginx:1.0 생성 완료
docker images	이미지 목록 확인	my-nginx:1.0 확인
docker run -d -p 8080:80 --name my-web-container my-nginx:1.0	컨테이너 실행	정상 실행
docker ps	실행 중인 컨테이너 확인	my-web-container Up 상태 확인
결과
localhost:8080 접속 시 "Docker 커스텀 이미지 빌드 성공!" 문구 확인 ✅
커스텀 HTML 파일이 nginx를 통해 정상 서빙됨을 확인했다.
핵심 개념 정리
FROM : 베이스 이미지 지정
COPY : 로컬 파일을 이미지 안으로 복사
docker build : Dockerfile을 읽어 이미지를 생성
-t : 이미지에 이름(태그) 부여
-d : 백그라운드 실행
-p 8080:80 : 호스트 8080 → 컨테이너 80 포트 매핑

## 보완설명(로그 및 스크린샷, 이론적 근거)

### 1. Docker 버전 및 상태 확인
PS C:\Jaeyun_dev-workstation> docker --version
Docker version 29.9.2, build a82e528
PS C:\Jaeyun_dev-workstation> docker info
Docker 환경 정보 (docker info 요약)
- Server Version: 29.9.2
- Operating System: Docker Desktop (WSL2)
- Kernel Version: 6.18.54.1-microsoft-standard-WSL2
- Architecture: x86_64
- CPUs: 6
- Total Memory: 7.443GiB

### 2. Git 연결 상태 확인
PS C:\Jaeyun_dev-workstation> git remote -v
origin  https://github.com/pjy0802-source/Jaeyun_dev-workstation.git (fetch)
origin  https://github.com/pjy0802-source/Jaeyun_dev-workstation.git (push)

PS C:\Jaeyun_dev-workstation> git log -n 3 --oneline
3d4a626 (HEAD -> main, origin/main) docs: 미션 3 Docker 커스텀 이미지 빌드 실습 내용 추가
920a418 docs: 미션1 진행현황 체크리스트 업데이트
13d6702 docs: 미션2 Docker Compose 실습 기록 추가

### 3. 프로젝트 구조 확인 (현재 폴더 기준)
PS C:\Jaeyun_dev-workstation> tree /f
폴더 PATH의 목록입니다.
볼륨 일련 번호는 E46B-4CFE입니다.
C:.
│  .gitignore
│  Dockerfile
│  index.html
│  log.md
│  README.md
│
├─.git
│  │  COMMIT_EDITMSG
│  │  config
│  │  description
│  │  FETCH_HEAD
│  │  HEAD
│  │  index
│  │  ORIG_HEAD
│  │  REBASE_HEAD
│  │
│  ├─hooks
│  │      applypatch-msg.sample
│  │      commit-msg.sample
│  │      fsmonitor-watchman.sample
│  │      post-update.sample
│  │      pre-applypatch.sample
│  │      pre-commit.sample
│  │      pre-merge-commit.sample
│  │      pre-push.sample
│  │      pre-rebase.sample
│  │      pre-receive.sample
│  │      prepare-commit-msg.sample
│  │      push-to-checkout.sample
│  │      sendemail-validate.sample
│  │      update.sample
│  │
│  ├─info
│  │      exclude
│  │
│  ├─logs
│  │  │  HEAD
│  │  │
│  │  └─refs
│  │      ├─heads
│  │      │      main
│  │      │
│  │      └─remotes
│  │          └─origin
│  │                  main
│  │
│  ├─objects
│  │  ├─0c
│  │  │      19e0c5f7f24a863a69589abae0de130a77fe6b
│  │  │
│  │  ├─13
│  │  │      d6702377aedaa8d04127ce52573d8468a55083
│  │  │
│  │  ├─1d
│  │  │      04c807ada535dd2f381fdf27e2669b8e4dcc22
│  │  │
│  │  ├─20
│  │  │      8d618ca1c6ae2ef4ec3039b03f4f94e04dfaf1
│  │  │
│  │  ├─24
│  │  │      e09e9cf913b9a3a9cecb57e2de8d0caacf9e36
│  │  │
│  │  ├─28
│  │  │      91cd1cc320f7ac0e81cdd265a1c940f2412f82
│  │  │
│  │  ├─2d
│  │  │      955e5ed136e0778511082504008029d9792bad
│  │  │
│  │  ├─32
│  │  │      3e5265d06969d45cc4596021487ea8ba10b0d6
│  │  │
│  │  ├─3b
│  │  │      1748e50ecd7732c4a203ab1e4a5b6b1e6ec3bf
│  │  │
│  │  ├─3d
│  │  │      4a6264918dca1aa80f936f19997be6285c8fd1
│  │  │
│  │  ├─41
│  │  │      d06f5937c41bf521833c9a40fd363f36732369
│  │  │
│  │  ├─42
│  │  │      353eee6407846fc986921117ff28dbb400d2e6
│  │  │      7deae25fd2793f6bf8610e3621a97643b83953
│  │  │
│  │  ├─4f
│  │  │      14fdd873ab526d67f7c261eeabef3e877fe7d4
│  │  │
│  │  ├─55
│  │  │      15f4119fe41f603b797160e2a612705b6b203f
│  │  │
│  │  ├─56
│  │  │      0c3a949eab7a307078765e745abde4e152adaf
│  │  │
│  │  ├─59
│  │  │      feabed4c978cbc45beae7e487d03f760d3da9d
│  │  │
│  │  ├─5b
│  │  │      07f7e4b74f4cd1b4e4289cb7d26575f1cfaf49
│  │  │      e1ac205a62970c775be6afe2091273e9a063bb
│  │  │
│  │  ├─5c
│  │  │      7e9ab125c1d4ad04257e05bd48529c2ec2be22
│  │  │
│  │  ├─65
│  │  │      d13faed30e3ce72f0efe9f4f52f78c87aee3e0
│  │  │
│  │  ├─66
│  │  │      bfec1bf1e90bef0801d6ee77acb2d0af156e6d
│  │  │
│  │  ├─6d
│  │  │      6fe4a0020d507e384273c892ec4d8097d3209f
│  │  │      99893a2a7beea119a164daee496a33c034a8c8
│  │  │
│  │  ├─6e
│  │  │      114a1653258012a635183f5d7737b548cf79e0
│  │  │
│  │  ├─6f
│  │  │      f0a55abda9d7e0099c092ef7cdb80591680336
│  │  │
│  │  ├─78
│  │  │      6b6d486c6a20eeac7b57ec8ebc142d763cbf85
│  │  │      cb830c47c1a00f6e3e3c948cfea13531d90fe8
│  │  │
│  │  ├─82
│  │  │      a0016c25d8bd8879f6b6181353d27dd3152aba
│  │  │
│  │  ├─83
│  │  │      2954d8af78ae55b22307592c75bc6a2f637001
│  │  │
│  │  ├─84
│  │  │      6d1862876b4dc66358f5f3b0cb60c658655b77
│  │  │
│  │  ├─85
│  │  │      2d84803a7e1e05eae8c7e7e3c0f70a961b06ed
│  │  │      8a186c20a29a7e56b2786fb252edf057f95ad5
│  │  │
│  │  ├─89
│  │  │      eef4de4f762cdd77b62c460db01857ac1a7c04
│  │  │
│  │  ├─8c
│  │  │      a6f03b00f97a90a09279b59b2e0050032c7b54
│  │  │
│  │  ├─92
│  │  │      0a418a92e8a17eac292a7e199bcd845a3258df
│  │  │
│  │  ├─9e
│  │  │      70c9b5b5d426c98678e994a665668bc4556803
│  │  │
│  │  ├─9f
│  │  │      b893b77065c10617bb1d01622760ccb71f3f09
│  │  │
│  │  ├─a0
│  │  │      c085d7467d49e9e61a19e421fcb2f22adf5abe
│  │  │
│  │  ├─a3
│  │  │      f7c72a7b4b22c4d9e779b4f33e84b99072b969
│  │  │
│  │  ├─a5
│  │  │      7ae1628bfb75b5ec9064c0a03465766d5f7499
│  │  │
│  │  ├─ad
│  │  │      8f00de4d72f5e614d51c35d34776952e7d20ff
│  │  │
│  │  ├─b1
│  │  │      409f54775061af68dbcc1f53f92e522c0da688
│  │  │
│  │  ├─b9
│  │  │      f817f6b2955831bb73f270f0f8a10a7e4b44ed
│  │  │
│  │  ├─c0
│  │  │      bc6b2dbd07ca31911e0e9e44c869d8dcd4e115
│  │  │
│  │  ├─cf
│  │  │      31dc66100172aced987fcf733fb077f3a17bdc
│  │  │
│  │  ├─d8
│  │  │      1fa446dc11c710c72fe393c1b069763eba224e
│  │  │
│  │  ├─da
│  │  │      0391ea0db395e90d3f9e3e2bc6c22dabd7a473
│  │  │
│  │  ├─db
│  │  │      2716bfa2e3c28a3dc5bbbb25828cd527d27fa2
│  │  │
│  │  ├─dd
│  │  │      fd76b5bfc52aeb892ca6c2b335147154a86524
│  │  │
│  │  ├─de
│  │  │      42779107564505909b5fd1b26caebee534d217
│  │  │
│  │  ├─e5
│  │  │      1f5cd2ce67523d0e4bb4c25a7820d7a997c6b6
│  │  │
│  │  ├─e6
│  │  │      9de29bb2d1d6434b8b29ae775ad8c2e48c5391
│  │  │
│  │  ├─e8
│  │  │      78726a40784312c956ecb91a2c29222f881fe2
│  │  │
│  │  ├─ed
│  │  │      890710a4fc019a6a1766191a67e42bf574b040
│  │  │
│  │  ├─f1
│  │  │      b8c8e4abd903b21ac785db5959d469ad53319b
│  │  │
│  │  ├─f4
│  │  │      6bf3ac7573d9a59ba898d9cd56941e8ab8b033
│  │  │      c6d3a4268f4dcf10164da2028ab0a232cc82ed
│  │  │
│  │  ├─f5
│  │  │      631593d59eeab8820b432240196df7d5c42973
│  │  │
│  │  ├─fd
│  │  │      e5f36ba6c7a01d87277a593e2abed7bea8c337
│  │  │
│  │  ├─fe
│  │  │      a4f2dceed4be37671277688b191f40eb74e8c3
│  │  │
│  │  ├─info
│  │  └─pack
│  └─refs
│      ├─heads
│      │      main
│      │
│      ├─remotes
│      │  └─origin
│      │          main
│      │
│      └─tags
├─images
│      port-mapping-8080.png  .png
│
├─my-web
│  └─site
│          index.html
│
├─practice
│  ├─bind-mount
│  │      index.html
│  │
│  └─docker-compose-lab
│          docker-compose.yml
│
└─test-dir
        test.txt
### 4. Hello-World 실행 로그
PS C:\Jaeyun_dev-workstation> docker run hello-world

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/

### 5. 이미지 및 컨테이너 목록 확인
PS C:\Jaeyun_dev-workstation> docker images
                                                                     i Info →   U  In Use
IMAGE                ID             DISK USAGE   CONTENT SIZE   EXTRA
hello-world:latest   c567b231f656       25.9kB         9.49kB    U
my-nginx:1.0         6239396760e7       93.7MB         26.4MB    U
redis:alpine         71885d8cc6e4        162MB           40MB
ubuntu:latest        6a06111c3b0a        163MB         45.9MB

PS C:\Jaeyun_dev-workstation> docker ps -a
CONTAINER ID   IMAGE          COMMAND                   CREATED              STATUS                          PORTS                                     NAMES
f2e5b290dda9   hello-world    "/hello"                  About a minute ago   Exited (0) About a minute ago                                             peaceful_bouman
0bc0c0214603   my-nginx:1.0   "/docker-entrypoint.…"   47 minutes ago       Up 47 minutes                   0.0.0.0:8080->80/tcp, [::]:8080->80/tcp   my-web-container
13362ca31bcb   hello-world    "/hello"                  2 hours ago          Exited (0) 2 hours ago                                                    admiring_rosalind

### 6. 권한 변경 전후 확인
PS C:\Jaeyun_dev-workstation> echo "permission test" > sample.txt
PS C:\Jaeyun_dev-workstation> wsl ls -l sample.txt
-rwxrwxrwx    1 root     root            36 Nov  6 14:48 sample.txt
PS C:\Jaeyun_dev-workstation> wsl chmod 644 sample.txt
PS C:\Jaeyun_dev-workstation> wsl ls -l sample.txt
-rw-r--r--    1 root     root            36 Nov  6 14:48 sample.txt

#### 7. 권한 구성 이론 설명
리눅스 권한은 `r(읽기)`, `w(쓰기)`, `x(실행)`의 조합을 8진수 숫자로 표기합니다.
- **r (Read):** 4
- **w (Write):** 2
- **x (Execute):** 1

**계산 예시 (644):**
1. **소유자 (6):** 4(r) + 2(w) = 읽기 및 쓰기 가능
2. **그룹 (4):** 4(r) = 읽기만 가능
3. **기타 (4):** 4(r) = 읽기만 가능
결과적으로 `rw-r--r--`와 같은 형태로 나타납니다.

### 8. Docker 빌드 로그 (성공 메시지 포함)
PS C:\Jaeyun_dev-workstation> docker build -t my-nginx:1.0 .
[+] Building 2.4s (7/7) FINISHED                                     docker:desktop-linux
 => [internal] load build definition from Dockerfile                                 0.0s
 => => transferring dockerfile: 109B                                                 0.0s
 => [internal] load metadata for docker.io/library/nginx:alpine                      1.7s
 => [internal] load .dockerignore                                                    0.0s
 => => transferring context: 2B                                                      0.0s
 => [internal] load build context                                                    0.0s
 => => transferring context: 32B                                                     0.0s
 => [1/2] FROM docker.io/library/nginx:alpine@sha256:713fc2ebfd92e8217db451477182ee  0.1s
 => => resolve docker.io/library/nginx:alpine@sha256:713fc2ebfd92e8217db451477182ee  0.0s
 => [2/2] COPY index.html /usr/share/nginx/html/index.html                           0.1s
 => exporting to image                                                               0.4s
 => => exporting layers                                                              0.1s
 => => exporting manifest sha256:041a4012eb57d276293be2f8bbaecb52c0b981faa64f61f785  0.0s
 => => exporting config sha256:c13ca572063125862b012b2012f71db42129d4f0da65e5725fae  0.0s
 => => exporting attestation manifest sha256:8b8852b5e71046016a56cfa6c95a1b0c52c936  0.0s
 => => exporting manifest list sha256:6a47280fe9b191f90357e18b87166dbb4c492a0f78ac2  0.0s
 => => naming to docker.io/library/my-nginx:1.0                                      0.0s
 => => unpacking to docker.io/library/my-nginx:1.0

### 9. 컨테이너 실행 및 접속 확인 (curl 사용)
PS C:\Jaeyun_dev-workstation> docker run -d -p 8081:80 --name my-web-container2 my-nginx:1.0
40fc69a6bcad60b82c685241c1cf0dc4b0036506784db220db64aa1cb75efdc8
PS C:\Jaeyun_dev-workstation> curl http://localhost:8081

보안 경고: 스크립트 실행 위험
Invoke-WebRequest는 웹 페이지의 내용을 구문 분석합니다. 페이지를 구문 분석할 때 웹 페이지
 내 스크립트 코드가 실행될 수 있습니다.
      권장 조치:
      -UseBasicParsing 스위치를 사용하여 스크립트 코드 실행을 방지합니다.

      계속하시겠습니까?

[Y] 예(Y)  [A] 모두 예(A)  [N] 아니요(N)  [L] 모두 아니요(L)  [S] 일시 중단(S)
[?] 도움말(기본값은 "N"): y


StatusCode        : 200
StatusDescription : OK
Content           : ï»¿<!DOCTYPE html>
                    <html lang="ko">
                    <head>
                      <meta charset="UTF-8">
                      <title>Docker Test</title>
                    </head>
                    <body>
                      <h1>Docker ì»¤ì¤í
 ì ë¹ë ì
        ±ê³µ!</h1>
                    </body>
                    </html>

RawContent        : HTTP/1.1 200 OK
                    Connection: keep-alive
                    Accept-Ranges: bytes
                    Content-Length: 191
                    Content-Type: text/html
                    Date: Fri, 06 Nov 2026 15:12:23 GMT
                    ETag: "6aed929b-bf"
                    Last-Modified: Fri, 06 Nov 2026 0...
Forms             : {}
Headers           : {[Connection, keep-alive], [Accept-Ranges, bytes], [Content-Length, 1
                    91], [Content-Type, text/html]...}
Images            : {}
InputFields       : {}
Links             : {}
ParsedHtml        : mshtml.HTMLDocumentClass
RawContentLength  : 191

github images폴더에 이미지 저장완료

### 10. 바인드 마운트 및 삭제 후 복구 검증
PS C:\Jaeyun_dev-workstation> echo "Persistence Test" > ./test.txt
PS C:\Jaeyun_dev-workstation> docker run -d --name test-v -v ${PWD}/test.txt:/usr/share/nginx/html/test.txt nginx
Unable to find image 'nginx:latest' locally
latest: Pulling from library/nginx
512ac5e7ce8e: Pull complete
6d2e43921e9e: Pull complete
1724c05f72c6: Pull complete
bbb080c71d50: Pull complete
1962e1ff75b4: Pull complete
7cb4701ce7cd: Pull complete
37fb86c2a767: Pull complete
d2c7e31f04a3: Download complete
4582dace95e2: Download complete
Digest: sha256:165ddde8751e75a1c907d24ef10d9f6deb08b57e0fe56caf67512486aff76d82
Status: Downloaded newer image for nginx:latest
d3cc8eacaf2a82adef7dba88fe191dff64d7a5d95ecae62c135636ecf35aa8cd
PS C:\Jaeyun_dev-workstation> docker rm -f test-v
test-v
PS C:\Jaeyun_dev-workstation> ls ./test.txt


    디렉터리: C:\Jaeyun_dev-workstation


Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
-a----      2026-11-07  오전 12:18             38 test.txt

### 11. 이미지 vs 컨테이너
- 이미지는 실행 파일과 설정이 담긴 '읽기 전용 설계도'이며,
컨테이너는 이 설계도를 기반으로 메모리 위에서 실제 '살아 움직이는 프로세스'임



## 미션 1 추가 검증 실습

### 1. 작업 위치 및 로그 기록

PowerShell에서 프로젝트 루트 경로를 확인하고, 실습 명령과 출력을 기록하기 시작했다.

실행 명령:

```powershell
Get-Location
New-Item -ItemType Directory -Path ./logs -Force
Start-Transcript -Path "./logs/mission1-$(Get-Date -Format 'yyyyMMdd-HHmmss').txt"
```

실제 출력:

```PS C:\Jaeyun_dev-workstation> Get-Location
Path
----
C:\Jaeyun_dev-workstation

PS C:\Jaeyun_dev-workstation> Set-Location C:\Jaeyun_dev-workstation
PS C:\Jaeyun_dev-workstation> New-Item -ItemType Directory -Path ./logs -Force


    디렉터리: C:\Jaeyun_dev-workstation


Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
d-----      2026-11-07  오전 12:38                logs


PS C:\Jaeyun_dev-workstation> Start-Transcript -Path "./logs/mission1-$(Get-Date -Format 'yyyyMMdd-HHmmss').txt"
기록이 시작되었습니다. 출력 파일은 ./logs/mission1-20261107-003857.txt입니다.
```

### 2. Docker 버전 및 엔진 상태 확인

실행 명령:

```powershell
docker --version
docker info
```

실제 출력:

```PS C:\Jaeyun_dev-workstation> docker --version
Docker version 29.9.2, build a82e528
PS C:\Jaeyun_dev-workstation> docker info
Client:
 Version:    29.9.2
 Context:    desktop-linux
 Debug Mode: false
 Plugins:
  agent: Docker AI Agent Runner (Docker Inc.)
    Version:  v1.152.0
    Path:     C:\Users\HP\.docker\cli-plugins\docker-agent.exe
  ai: Docker AI Agent - Ask Gordon (Docker Inc.)
    Version:  v1.33.0
    Path:     C:\Users\HP\.docker\cli-plugins\docker-ai.exe
  buildx: Docker Buildx (Docker Inc.)
    Version:  v0.38.1
    Path:     C:\Users\HP\.docker\cli-plugins\docker-buildx.exe
  compose: Docker Compose (Docker Inc.)
    Version:  v5.6.1
    Path:     C:\Users\HP\.docker\cli-plugins\docker-compose.exe
  debug: Get a shell into any image or container (Docker Inc.)
    Version:  0.49.0
    Path:     C:\Users\HP\.docker\cli-plugins\docker-debug.exe
  desktop: Docker Desktop commands (Docker Inc.)
    Version:  4.98.0
    Path:     C:\Users\HP\.docker\cli-plugins\docker-desktop.exe
  dhi: CLI for managing Docker Hardened Images (Docker Inc.)
    Version:  v0.0.9
    Path:     C:\Users\HP\.docker\cli-plugins\docker-dhi.exe
  extension: Manages Docker extensions (Docker Inc.)
    Version:  v0.2.32
    Path:     C:\Users\HP\.docker\cli-plugins\docker-extension.exe
  init: Creates Docker-related starter files for your project (Docker Inc.)
    Version:  v1.4.1
    Path:     C:\Users\HP\.docker\cli-plugins\docker-init.exe
  mcp: Docker MCP Plugin (Docker Inc.)
    Version:  v0.44.2
    Path:     C:\Users\HP\.docker\cli-plugins\docker-mcp.exe
  model: Docker Model Runner (Docker Inc.)
    Version:  v1.2.9
    Path:     C:\Users\HP\.docker\cli-plugins\docker-model.exe
  offload: Docker Offload (Docker Inc.)
    Version:  v0.7.35
    Path:     C:\Users\HP\.docker\cli-plugins\docker-offload.exe
  pass: Docker Pass Secrets Manager Plugin (beta) (Docker Inc.)
    Version:  v0.3.2
    Path:     C:\Users\HP\.docker\cli-plugins\docker-pass.exe
  sandbox: "docker sandbox" is deprecated, use Docker Sandboxes instead (Docker Inc.)
    Version:  v0.13.0
    Path:     C:\Users\HP\.docker\cli-plugins\docker-sandbox.exe
  scout: Docker Scout (Docker Inc.)
    Version:  v1.27.0
    Path:     C:\Users\HP\.docker\cli-plugins\docker-scout.exe

Server:
 Containers: 4
  Running: 2
  Paused: 0
  Stopped: 2
 Images: 5
 Server Version: 29.9.2
 Storage Driver: overlayfs
  driver-type: io.containerd.snapshotter.v1
 Logging Driver: local
 Cgroup Driver: cgroupfs
 Cgroup Version: 2
 Plugins:
  Volume: local
  Network: bridge host ipvlan macvlan null overlay
  Log: awslogs fluentd gcplogs gelf journald json-file local splunk syslog
 CDI spec directories:
  /etc/cdi
  /var/run/cdi
 Discovered Devices:
  cdi: docker.com/gpu=webgpu
 Swarm: inactive
 Runtimes: io.containerd.runc.v2 nvidia runc
 Default Runtime: runc
 Init Binary: docker-init
 containerd version: b7a25261e029d68978bbf290df0a62fc819b3c51
 runc version: v1.5.2-0-g29dd3dc2
 init version: de40ad0
 Security Options:
  seccomp
   Profile: builtin
  cgroupns
 Kernel Version: 6.18.54.1-microsoft-standard-WSL2
 Operating System: Docker Desktop
 OSType: linux
 Architecture: x86_64
 CPUs: 6
 Total Memory: 7.443GiB
 Name: docker-desktop
 ID: e3198a08-ce75-4e4e-b3ce-09151e04450d
 Docker Root Dir: /var/lib/docker
 Debug Mode: false
 HTTP Proxy: http.docker.internal:3128
 HTTPS Proxy: http.docker.internal:3128
 No Proxy: hubproxy.docker.internal
 Labels:
  com.docker.desktop.address=npipe://\\.\pipe\docker_cli
 Experimental: false
 Insecure Registries:
  hubproxy.docker.internal:5555
  127.0.0.0/8
  ::1/128
 Live Restore Enabled: false
 Firewall Backend: iptables
```

확인 기준:
- docker --version으로 Docker CLI 버전을 확인한다.
- docker info의 Server 영역에서 엔진 응답과 서버 환경을 확인한다.
- Docker Desktop 앱 버전은 CLI 및 서버 버전과 별도로 구분한다.

### 3. hello-world 컨테이너 실행 확인

실행 명령:

```powershell
docker run hello-world
```

실제 출력:

```PS C:\Jaeyun_dev-workstation> docker run hello-world

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/
```

결과 해석:
- Hello from Docker! 메시지로 테스트 프로그램의 정상 실행을 확인했다.
- Docker CLI가 엔진에 요청하고, 엔진이 이미지로 컨테이너를 생성해 실행했다.
- hello-world는 메시지를 출력한 뒤 종료되는 프로그램이므로 실행 후 종료되는 것이 정상이다.

### 4. 이미지 및 컨테이너 목록 확인

실행 명령:

```powershell
docker images
docker ps -a
```

이미지 목록 실제 출력:

```PS C:\Jaeyun_dev-workstation> docker images
                                                                     i Info →   U  In Use
IMAGE                ID             DISK USAGE   CONTENT SIZE   EXTRA
hello-world:latest   c567b231f656       25.9kB         9.49kB    U
my-nginx:1.0         6a47280fe9b1       93.7MB         26.4MB    U
nginx:latest         165ddde8751e        243MB         66.8MB
redis:alpine         71885d8cc6e4        162MB           40MB
ubuntu:latest        6a06111c3b0a        163MB         45.9MB
```

컨테이너 목록 실제 출력:

```PS C:\Jaeyun_dev-workstation> docker ps -a
CONTAINER ID   IMAGE          COMMAND                   CREATED             STATUS                         PORTS                                     NAMES
6b9e2b10ff63   hello-world    "/hello"                  2 minutes ago       Exited (0) 2 minutes ago                                                 focused_vaughan
40fc69a6bcad   my-nginx:1.0   "/docker-entrypoint.…"   39 minutes ago      Up 39 minutes                  0.0.0.0:8081->80/tcp, [::]:8081->80/tcp   my-web-container2
f2e5b290dda9   hello-world    "/hello"                  About an hour ago   Exited (0) About an hour ago                                             peaceful_bouman
0bc0c0214603   6239396760e7   "/docker-entrypoint.…"   2 hours ago         Up 2 hours                     0.0.0.0:8080->80/tcp, [::]:8080->80/tcp   my-web-container
13362ca31bcb   hello-world    "/hello"                  3 hours ago         Exited (0) 3 hours ago                                                   admiring_rosalind
```

결과 해석:
- docker images는 로컬에 저장된 이미지 목록을 보여준다.
- docker ps -a는 실행 중인 컨테이너와 종료된 컨테이너를 모두 보여준다.
- 이미지 이름·태그와 컨테이너 이름·상태·포트 매핑을 구분해 확인했다.

### 5. 프로젝트 구조 및 구성 기준

실행 명령:

```powershell
git ls-files
```

실제 출력:

```PS C:\Jaeyun_dev-workstation> git ls-files
.gitignore
Dockerfile
README.md
images/port-mapping-8080.png  .png
index.html
log.md
my-web/site/index.html
practice/bind-mount/index.html
practice/docker-compose-lab/docker-compose.yml
sample.txt
test-dir/test.txt
test.txt
```

주요 파일과 폴더의 역할:

| 경로 | 역할 |
|---|---|
| README.md | 실습 절차, 명령어, 결과와 배운 내용 기록 |
| Dockerfile | 커스텀 Nginx 이미지 빌드 방법 정의 |
| index.html | 커스텀 이미지에 포함할 웹페이지 |
| log.md | 실습 과정과 작업 기록 |
| images/ | README에서 참조할 스크린샷 저장 |
| practice/bind-mount/ | 바인드 마운트 실습 파일 |
| practice/docker-compose-lab/ | Docker Compose 실습 설정 |
| my-web/site/ | 웹 실습용 HTML 파일 |
| test-dir/ | 기본 파일 조작 실습 파일 |
| logs/ | 추가 검증 실습의 터미널 기록 |

구성 기준:
- 프로젝트 루트에는 대표 문서와 이미지 빌드에 필요한 파일을 둔다.
- practice 폴더에서는 실습 주제별로 하위 폴더를 구분한다.
- 스크린샷은 images, 터미널 실행 기록은 logs에 구분해 저장한다.
- git ls-files에는 Git이 추적하는 파일만 표시되며, 아직 추가하지 않은 파일과 빈 폴더는 표시되지 않는다.

### 6. 이미지와 컨테이너의 차이 및 변경 반영

Dockerfile 확인 명령:

```powershell
Get-Content .\Dockerfile
```

실제 출력:

```PS C:\Jaeyun_dev-workstation> Get-Content .\Dockerfile
FROM nginx:alpine
COPY index.html /usr/share/nginx/html/index.html
```

이미지와 컨테이너 비교:

| 구분 | 이미지 | 컨테이너 |
|---|---|---|
| 역할 | 프로그램과 설정을 담은 실행 템플릿 | 이미지로부터 생성한 실행 환경 |
| 생성 명령 | docker build | docker run |
| 상태 | 실행 상태를 갖지 않음 | 실행·중지 등의 상태를 가짐 |
| 파일 변경 | 빌드로 새 이미지 생성 | 자체 쓰기 계층에 변경 저장 |
| 삭제 영향 | 해당 이미지 삭제 | 마운트 외의 자체 쓰기 계층 데이터 삭제 |

변경 반영 과정:
1. Dockerfile 또는 COPY 대상인 index.html을 수정한다.
2. docker build로 이미지를 다시 빌드한다.
3. 기존 컨테이너에는 새 이미지의 변경이 자동 반영되지 않는다.
4. 새 이미지로 컨테이너를 다시 생성한다.

기존 컨테이너를 stop/start하는 것만으로는 새 이미지가 적용되지 않는다.
바인드 마운트로 연결한 파일은 호스트의 변경을 컨테이너에서 확인할 수 있다.

### 7. 포트 매핑 및 웹 응답 확인

실행 명령:

```powershell
docker port my-web-container2
curl.exe -i http://localhost:8081
```

포트 매핑 실제 출력:

```
PS C:\Jaeyun_dev-workstation> docker port my-web-container2
80/tcp -> 0.0.0.0:8081
80/tcp -> [::]:8081
```

웹 응답 실제 출력:

```HTTP/1.1 200 OK
Server: nginx/1.31.8
Date: Fri, 06 Nov 2026 15:53:54 GMT
Content-Type: text/html
Content-Length: 191
Last-Modified: Fri, 06 Nov 2026 08:40:59 GMT
Connection: keep-alive
ETag: "6aed929b-bf"
Accept-Ranges: bytes

<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <title>Docker Test</title>
</head>
<body>
  <h1>Docker 커스텀 이미지 빌드 성공!</h1>
</body>
</html>
```

네트워크 원리:
- 일반적인 브리지 네트워크에서 컨테이너는 네트워크 네임스페이스로 분리된 네트워크 환경을 가진다.
- 각 컨테이너가 내부 80번 포트를 사용해도 서로 충돌하지 않는다.
- -p 8081:80은 호스트의 8081번 포트로 들어오는 요청을 컨테이너의 80번 포트로 전달한다.
- 같은 호스트 IP와 포트를 여러 컨테이너가 동시에 사용하려 하면 충돌한다.

확인 결과:
- 실제 포트 매핑 출력에서 호스트와 컨테이너의 연결을 확인했다.
- HTTP 응답 상태와 HTML 본문으로 웹서버의 응답을 확인했다.

### 8. 호스트와 컨테이너의 경로 구분

실행 명령:

```powershell
Get-Location
Resolve-Path .\index.html
docker exec my-web-container2 ls -l /usr/share/nginx/html/index.html
```

실제 출력:

```PS C:\Jaeyun_dev-workstation> Get-Location

Path
----
C:\Jaeyun_dev-workstation

PS C:\Jaeyun_dev-workstation> Resolve-Path .\index.html

Path
----
C:\Jaeyun_dev-workstation\index.html

PS C:\Jaeyun_dev-workstation> docker exec my-web-container2 ls -l /usr/share/nginx/html/index.html
-rwxr-xr-x    1 root     root           191 Nov  6 08:40 /usr/share/nginx/html/index.html

```

경로 선택 기준:

| 구분 | 예시 | 기준 |
|---|---|---|
| 호스트 상대 경로 | .\index.html | PowerShell의 현재 작업 폴더 기준 |
| 호스트 절대 경로 | C:\Jaeyun_dev-workstation\index.html | 현재 작업 폴더와 관계없이 위치 지정 |
| 컨테이너 절대 경로 | /usr/share/nginx/html/index.html | 컨테이너 내부 루트 기준 |
| 컨테이너 상대 경로 | index.html | 컨테이너에서 명령을 실행하는 작업 디렉터리 기준 |

재현성을 위한 기준:
- 실습 명령을 실행할 프로젝트 루트 위치를 먼저 명시한다.
- 프로젝트 내부 파일은 상대 경로를 사용하면 다른 컴퓨터로 옮겨도 활용하기 쉽다.
- 바인드 마운트의 호스트 경로는 현재 위치를 확인한 뒤 절대 경로로 지정한다.
- 바인드 마운트의 컨테이너 대상 경로는 절대 경로로 지정해야 한다.
- Dockerfile의 COPY 원본은 빌드 컨텍스트 기준이며, 위 컨테이너 파일은 COPY로 이미지에 포함된 파일이다.

### 9. 바인드 마운트 데이터 유지 및 재연결 검증

실습 방법:
1. 호스트에 persistence-check.txt를 생성했다.
2. mission1-persist-a에 바인드 마운트하고 내용을 확인했다.
3. 컨테이너를 삭제한 뒤 호스트에서 파일 내용을 확인했다.
4. 새 컨테이너 mission1-persist-b에 같은 파일을 연결하고 내용을 확인했다.
5. 실습용 컨테이너를 삭제했다.

실행 명령 및 실제 출력:

```PS C:\Jaeyun_dev-workstation> Set-Content -Path .\persistence-check.txt -Value "Persistence Test" -Encoding ASCII
PS C:\Jaeyun_dev-workstation> docker run -d --name mission1-persist-a --mount "type=bind,source=${PWD}/persistence-check.txt,target=/usr/share/nginx/html/test.txt" nginx:alpine
Unable to find image 'nginx:alpine' locally
alpine: Pulling from library/nginx
Digest: sha256:713fc2ebfd92e8217db451477182ee91944b123d2b1ee9fd5a8c6e91ca6c3a11
Status: Downloaded newer image for nginx:alpine
64ddc51975d262d3cf1d409d38c221603bc590b907d6ad083ccda3406ebf9953
PS C:\Jaeyun_dev-workstation> docker exec mission1-persist-a cat /usr/share/nginx/html/test.txt
Persistence Test
PS C:\Jaeyun_dev-workstation> docker rm -f mission1-persist-a                             mission1-persist-a
PS C:\Jaeyun_dev-workstation> Get-Content .\persistence-check.txt
Persistence Test
PS C:\Jaeyun_dev-workstation> docker run -d --name mission1-persist-b --mount "type=bind,source=${PWD}/persistence-check.txt,target=/usr/share/nginx/html/test.txt" nginx:alpine
cdfadbdeb33a7f1226d599da72b354aea14a113722a1a287cacc219402778385
PS C:\Jaeyun_dev-workstation> docker exec mission1-persist-b cat /usr/share/nginx/html/test.txt
Persistence Test
PS C:\Jaeyun_dev-workstation> docker rm -f mission1-persist-b
mission1-persist-b
```

결과 해석:
- 삭제 전 컨테이너, 삭제 후 호스트, 새 컨테이너에서 같은 내용을 확인했다.
- 바인드 마운트 원본은 호스트에 있으므로 컨테이너 삭제 후에도 유지됐다.
- 이번 실습은 남아 있는 원본을 재연결한 것이며, 백업 파일에서 복원한 것은 아니다.
- 바인드 마운트는 백업이 아니므로 원본 파일의 삭제나 변경에 대비한 별도 백업이 필요하다.

### 10. 포트 충돌 진단 및 해결

문제:
- 두 컨테이너에 같은 호스트 18080번 포트를 할당하려고 했다.
- 두 번째 컨테이너 실행 시 포트 할당 오류가 발생했다.

가설:
- 첫 번째 컨테이너가 호스트 18080번 포트를 사용하고 있어 충돌한 것으로 추정했다.

확인:
- docker ps의 publish 필터로 포트를 사용하는 컨테이너를 확인했다.
- Get-NetTCPConnection으로 리스닝 포트와 PID를 확인했다.
- Get-Process로 해당 PID의 프로세스 이름을 확인했다.

조치:
- 18080번 포트를 사용하던 mission1-port-a를 중지했다.
- mission1-port-b를 docker start로 시작했지만, docker port 출력이 없고 HTTP 접속도 실패했다.
- mission1-port-b를 삭제하고 -p 18080:80 옵션으로 다시 생성했다.

검증:
- 재생성 후 docker port와 curl.exe로 포트 매핑 및 HTTP 응답을 확인했다.
- 실제 확인 결과는 아래 실행 로그에 기록했다.

추가 문제 확인:
- mission1-port-a를 중지한 후 mission1-port-b를 시작했다.
- 시작 명령은 컨테이너 이름을 반환했지만, docker port에는 출력이 없었다.
- curl.exe 요청도 연결에 실패했다.
- 따라서 시작 명령의 반환만으로 정상 작동을 판단할 수 없으며, 포트 매핑과 실제 HTTP 응답을 함께 확인해야 한다.

다음 조치:
- mission1-port-b를 삭제하고 포트 매핑을 지정해 다시 생성한 뒤 재검증한다.

PS C:\Jaeyun_dev-workstation> docker run -d -p 18080:80 --name mission1-port-a nginx:alpine
7c8794773bbe8db859b2df6a289cb20eac030d91dc296934a4aaf00fe93d1e10
PS C:\Jaeyun_dev-workstation> docker run -d -p 18080:80 --name mission1-port-b nginx:alpine
cf1c239a21c0fee686337abd313d3182853ae1148f1654b47d9e74b42b6459a5
docker: Error response from daemon: failed to set up container networking: driver failed p8beade7b6433a3dca7f598ad71fe1bc4fb4c): Bind for 0.0.0.0:18080 failed: port is already allo


PS C:\Jaeyun_dev-workstation> docker ps --filter "publish=18080"
CONTAINER ID   IMAGE          COMMAND                   CREATED          STATUS          P
7c8794773bbe   nginx:alpine   "/docker-entrypoint.…"   34 seconds ago   Up 33 seconds   0.-Object LocalAddress, LocalPort, OwningProcess
LocalAddress LocalPort OwningProcess
------------ --------- -------------
::               18080          7624
127.0.0.1        18080          5164


PS C:\Jaeyun_dev-workstation> Get-NetTCPConnection -LocalPort 18080 -State Listen | ForEach-Object { Get-Process -Id $_.OwningProcess } | Select-Object Id, ProcessName -Unique

  Id ProcessName
  -- -----------
5164 wslrelay
7624 com.docker.backend


PS C:\Jaeyun_dev-workstation> docker stop mission1-port-a
mission1-port-a
PS C:\Jaeyun_dev-workstation> docker ps --filter "publish=18080"
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
PS C:\Jaeyun_dev-workstation> docker start mission1-port-b
mission1-port-b
PS C:\Jaeyun_dev-workstation> docker port mission1-port-b
PS C:\Jaeyun_dev-workstation> curl.exe -I http://localhost:18080
curl: (7) Failed to connect to localhost port 18080 after 2241 ms: Could not connect to server
PS C:\Jaeyun_dev-workstation> docker rm -f mission1-port-b
mission1-port-b
PS C:\Jaeyun_dev-workstation> docker run -d -p 18080:80 --name mission1-port-b nginx:alpine
c610f66e956c7a38d0449503687e729ac15bb6b268d557bb47807c50a2f06527
PS C:\Jaeyun_dev-workstation> docker port mission1-port-b
80/tcp -> 0.0.0.0:18080
80/tcp -> [::]:18080
PS C:\Jaeyun_dev-workstation> curl.exe -I http://localhost:18080
HTTP/1.1 200 OK
Server: nginx/1.31.8
Date: Fri, 06 Nov 2026 16:07:46 GMT
Content-Type: text/html
Content-Length: 896
Last-Modified: Wed, 21 Oct 2026 17:54:44 GMT
Connection: keep-alive
ETag: "6ad8fc64-380"
Accept-Ranges: bytes
결과 해석:
컨테이너 시작 명령은 이름을 반환했지만, 포트 매핑 출력이 없고 HTTP 연결도 실패했다. 정상 서비스 여부를 추가로 확인해야 한다.

#### 컨테이너 재생성 후 재검증

조치:
실패했던 mission1-port-b를 삭제하고, 호스트 18080번과 컨테이너 80번의 포트 매핑을 지정해 다시 생성했다.

실행 명령 및 실제 출력:

```PS C:\Jaeyun_dev-workstation> docker rm -f mission1-port-b
mission1-port-b
PS C:\Jaeyun_dev-workstation> docker run -d -p 18080:80 --name mission1-port-b nginx:alpine
b31966ccf5e0b1104f96535301f3de5b31e552ab04b9cce10af1f6aba462fb64
PS C:\Jaeyun_dev-workstation> docker port mission1-port-b
80/tcp -> 0.0.0.0:18080
80/tcp -> [::]:18080
PS C:\Jaeyun_dev-workstation> curl.exe -I http://localhost:18080
HTTP/1.1 200 OK
Server: nginx/1.31.8
Date: Fri, 06 Nov 2026 16:14:08 GMT
Content-Type: text/html
Content-Length: 896
Last-Modified: Wed, 21 Oct 2026 17:54:44 GMT
Connection: keep-alive
ETag: "6ad8fc64-380"
Accept-Ranges: bytes
```

검증 결과:
여기에 docker port의 매핑 결과와 curl.exe의 HTTP 응답 상태를 확인해 기록한다.



실행 명령 및 실제 출력:

```text
여기에 ①부터 ⑥까지 실행한 명령과 실제 출력을 순서대로 붙여 넣는다.
```

배운 점:
- 컨테이너 이름이 달라도 같은 호스트 IP와 포트를 동시에 사용하면 충돌한다.
- 실행에 실패해도 생성된 컨테이너가 남을 수 있다.
- 포트를 해제한 후 기존 컨테이너를 시작하거나, 다른 호스트 포트로 새 컨테이너를 만들 수 있다.
- Docker 관련 프로세스를 강제 종료하지 않고 해당 컨테이너를 중지해 문제를 해결했다.

### 11. 데이터 보호 및 백업·복원 검증

실습 방법:
1. 바인드 마운트 실습에서 만든 원본 파일을 확인했다.
2. backups 폴더에 원본 파일을 복사했다.
3. 백업 파일을 별도 파일로 복원했다.
4. 원본과 복원본의 내용 및 SHA256 해시를 비교했다.

실행 명령 및 실제 출력:

```PS C:\Jaeyun_dev-workstation> docker rm -f mission1-port-a mission1-port-b
mission1-port-a
mission1-port-b
PS C:\Jaeyun_dev-workstation> Get-Content .\persistence-check.txt
Persistence Test
PS C:\Jaeyun_dev-workstation> New-Item -ItemType Directory -Path .\backups -Force


    디렉터리: C:\Jaeyun_dev-workstation


Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
d-----      2026-11-07   오전 1:16                backups


PS C:\Jaeyun_dev-workstation> Copy-Item .\persistence-check.txt .\backups\persistence-check-backup.txt
PS C:\Jaeyun_dev-workstation> Copy-Item .\backups\persistence-check-backup.txt .\persistence-restored.txt
PS C:\Jaeyun_dev-workstation> Get-Content .\persistence-restored.txt
Persistence Test
PS C:\Jaeyun_dev-workstation> Get-FileHash .\persistence-check.txt, .\persistence-restored.txt -Algorithm SHA256

Algorithm       Hash                                                                   Pa
                                                                                       th
---------       ----                                                                   --
SHA256          592FA851C79A6475A3E8A6AE3316579668254F3A2ACFBAE036E2026C5EF80673       C:
SHA256          592FA851C79A6475A3E8A6AE3316579668254F3A2ACFBAE036E2026C5EF80673
```

검증 결과:
여기에 복원 파일의 내용과 두 파일의 해시 일치 여부를 실제 결과에 따라 기록한다.

데이터 보호 기준:
- 데이터베이스처럼 컨테이너 교체 후에도 유지해야 하는 데이터는 이름 있는 볼륨에 저장한다.
- 바인드 마운트와 볼륨은 데이터 유지 수단이며, 별도 백업을 대신하지 않는다.
- 이번 실습은 호스트 파일의 복사 및 복원 검증이며, Docker 볼륨 백업 실습은 아니다.
- 같은 디스크의 backups 폴더는 디스크 고장에 대비할 수 없으므로, 중요한 백업은 별도 저장장치나 원격 저장소에도 보관한다.
- 운영 중인 데이터베이스는 단순 파일 복사보다 해당 DB의 백업 도구로 일관된 백업을 만든다.
- 볼륨 삭제 명령을 실행하기 전에는 필요한 데이터와 백업 여부를 확인한다.

### 12. Git 원격 연결 및 작업 상태 확인

실행 명령:

```powershell
git remote -v
git status --short
git log -n 3 --oneline
```

실제 출력:

```PS C:\Jaeyun_dev-workstation> git remote -v
origin  https://github.com/pjy0802-source/Jaeyun_dev-workstation.git (fetch)
origin  https://github.com/pjy0802-source/Jaeyun_dev-workstation.git (push)
PS C:\Jaeyun_dev-workstation> git status --short
 M README.md
?? backups/
?? logs/
?? persistence-check.txt
?? persistence-restored.txt
PS C:\Jaeyun_dev-workstation> git log -n 3 --oneline
00274f2 (HEAD -> main, origin/main) Fix: 보완 사항 반영
3d4a626 docs: 미션 3 Docker 커스텀 이미지 빌드 실습 내용 추가
920a418 docs: 미션1 진행현황 체크리스트 업데이트
```

결과 해석:
- git remote -v로 원격 저장소 주소를 확인했다.
- git status --short로 수정 파일과 미추적 파일을 확인했다.
- git log로 최근 커밋을 확인했다.
- 파일 저장, Git 커밋, GitHub push는 각각 별도 단계다.
- 이번 README 보완 내용의 원격 반영 여부는 최종 커밋과 push 후 별도로 확인한다.
