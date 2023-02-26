# 코드스테이츠 10일차 정리(Linux, Git)

생성일: 2023년 2월 24일 오전 9:30
태그: 코드스테이츠 일일 정리

# Linux

## CLI

Command Line Interface의 약자로 터미널을 통해 사용자와 컴퓨터가 키보드 입력 및 모니터의 출력으로 상호작용하는 방식

## 프롬프트

키보드의 입력을 확인, 편집할 수 있는 한 줄의 공간
![](https://velog.velcdn.com/images/player1552/post/77697a4b-9d8d-4c53-ae80-8c13ccc845c8/image.PNG)

# **Linux 명령어 정리**

## **pwd**

- 현재 경로를 확인

## **mkdir**

- 폴더를 생성

## **ls**

- 폴더 안의 파일 및 폴더 리스트를 출력
- **`l`** : 파일의 포맷까지 전부 표현
- **`a`** : 숨김 파일까지 모두 출력.
- **`al`** : **`a`**와 **`l`**의 기능 모두 사용

## **nautilus**

- Ubuntu를 GUI로 실행

## **cd**

- 경로를 이동하여 폴더로 들어감

## **touch**

- 빈 텍스트 파일을 생성

## **cat**

- 파일 내용을 출력

### rm

- 파일 및 폴더를 삭제
- **`r` :** 폴더 삭제
- `f` : 강제로 삭제

### mv

- 파일 및 폴더 위치 이동
- 이름 변경 가능 : `mv 파일명 바꿀이름`

### cp

- 파일 및 폴더 복사
- rm과 옵션 동일

### whoami

- 현재 로그인된 사용자를 확인

### sudo

- 관리자 권한(root 권한을 가져와서 사용)

## nano

기본적인 리눅스기반 텍스트 에디터

**vim(vi), emacs** 등 유명한 텍스트 에디터들은 기능이 많아 **초보자에게 부적절**

### 실행 방법

nano 파일 이름

**파일 저장** : Ctrl + O

**파일 편집 종료** : Ctrl + X

**패키지** : 압축파일, 파일의 여러 정보들부터 내부 파일들을 담고 있다.

**패키지 매니저** : 패키지들은 한 저장공간에 모여있고, 그 저장공간에서 패키지를 가져와 설치할 수 있게 한다.

( 패키지에 선설치가 필요한 파일들이 담겨있고, 패키지 매니저는 자동으로 선설치 패키지를 먼저 설치한다 )

### Node.js

Javascript 런타임 ( 브라우저 )

### 런타임

어떤 프로그램이 실행되는 환경

### nvm

Node Version Manager의 약자로, Node.js의 설치를 담당하는 패키지 매니저와 같은 기능을 하는 프로그램이다.

**nvm ls-remote** : Node.js의 사용가능한 모든 버전들을 목록으로 보여준다.

**nvm use 버전** : nvm으로 여러 버전을 설치한 경우, 원하는 버전을 입력해서 변경할 수 있다.

### npm

- Node Package Manager의 약자로, npm 서비스를 통해 Node.js로 개발된 프로그램들을 npm 패키지라고 부르며, 그 패키지들을 관리해주는 프로그램
- npm install 이름@버전

### package.json

- 코드(모듈)의 전반적인 정보를 담고 있는 파일
- 실제 실행시키는 모듈은 node_modules라는 폴더에 저장되어 있고, package.json은 카탈로그라고 생각하면 편하다.
- package.json에는 필요한 모듈을 작성해두는 공간이 존재하며, 그 모듈을 npm으로 다운로드 받으면 node_modules 라는 폴더가 생성되며, 내용이 담긴다.
- **npm install 이름 —save-dev 를 입력하면, 이름의 모듈이 devDependencies에 기록됨.**

### github에 Linux git과 보안 ssh 키로 연동하는법

1. ssh-keygen을 통해 /.ssh./ 에 id_rsa와 id_rsa.pub이 생성됨
2. id_rsa.pub은 공개키
3. id_rsa는 개인키, 비밀키

**(공개키를 복사 → github → Settings → SSH and GPG Keys → new SSH Key → title(장치 이름) / Key(공개키) → Add SSH Key)**

## [**Github CLI 사용법**](https://meaownworld.tistory.com/entry/Github-cli-설치-사용법)

## 처음 듣거나 어려웠던 부분(암기할 부분)

스냅샷 : 특정 시점에 생성된 백업 복사본

commit : 특정 시점에 스냅샷을 만드는 것

⭐ package.json 내부 코드