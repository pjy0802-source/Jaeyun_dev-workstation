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











