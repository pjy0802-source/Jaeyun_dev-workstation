<<<<<<< HEAD
<<<<<<< HEAD
# Jaeyun Dev Workstation
=======
﻿## Jaeyun Dev Workstation
>>>>>>> 66bfec1 (feat: initial commit with README.md)
=======
﻿# 코디세이 미션 1 기록

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
>>>>>>> 4f14fdd (1차 진행 내용 기록)
