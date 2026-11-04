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
- [ ] Docker 볼륨(Volume) 실습
- [ ] Docker Compose 실습