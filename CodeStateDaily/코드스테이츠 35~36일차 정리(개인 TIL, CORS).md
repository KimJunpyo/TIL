# 코드스테이츠 35~36일차 정리(개인 TIL, CORS)

생성일: 2023년 4월 4일 오전 9:47
태그: 코드스테이츠 일일 정리

# CORS 에러

![](https://velog.velcdn.com/images/player1552/post/81cd9b71-3695-4dc5-8da4-0f06785e8cb2/image.PNG)


## CORS

> Cross-Origin Resource Sharing의 약어로 교차 출처 리소스 공유를 의미한다.
> > 추가 HTTP 헤더를 사용하여, 한 출처에서 실행 중인 웹 애플리케이션이 다른 출처의 선택한 자원에 접근할 수 있는 권한을 부여하도록 브라우저에 알려주는 체제
> 
- SOP로 인해 차단되는 다른 출처의 자원에 대한 접근을 허용하는 정책이다.
- 따라서, CORS가 에러를 발생시키는 것이 아니라, SOP로 인해 에러가 발생한 것이며, 이를 도와주기 위해 브라우저에서 에러를 발생시키는 것이다.




## 출처

> Origin을 의미하며 URL을 기준으로 scheme(protocol), hosts, port 부분을 뜻하는 말이다.
> 

![](https://velog.velcdn.com/images/player1552/post/c49f673e-7c29-48d5-8d67-9dd374c47b41/image.png)



## SOP

> Same-Origin Policy의 약어로 동일 출처 정책을 의미한다.
> > “다른 출처의 리소스에 대한 접근을 차단한다”는 브라우저 정책이다.
같은 출처의 서버에 존재하는 리소스는 자유롭게 사용할 수 있지만, 다른 출처의 리소스는 브라우저에서 사용되는 SOP로 인하여 접근이 차단된다.
> 



### SOP를 쓰는 이유

> 브라우저가 기본적으로 다른 출처들과의 연결을 차단함으로써 외부 출처들이 사이트에 대한 공격을 시도하지 못하도록 한다.
> 
- 만약 A 사이트에서 로그인을 한 뒤, 공격 스크립트가 설치된 B 사이트에 접속하게 되면 A 사이트의 로그인 정보 등을 탈취 당할 수 있다.
- SOP를 사용한다고 하여 모든 공격을 방지할 수는 없으나, 그 경로를 줄일 수 있기 때문에 모든 브라우저에서 기본적으로 시행되는 정책으로써 사용되고 있다.

### CORS Error 해결 방법

- 서버의 응답 헤더에 “Access-Control-Allow-Origin”을 작성하여 접근 권한을 얻을 수 있다.
- 즉, 백엔드의 기반에서 해결해줘야 하는 부분이다.
- 서버로 요청하는 데이터의 출처가 “Access-Control_Allow-Origin”의 출처와 동일한지 확인하는 과정이 진행되며, 동일하지 않은 요청은 CORS Error를 발생시킨다.

## CORS 동작 방식

### 1. Preflight Request

- 실제 요청을 보내기 전, OPTIONS 메소드로 출처 리소스에 접근할 수 있는 권한이 있는지 확인하는 것을 말한다.
- 실제 요청을 보낸 뒤, CORS Error를 발생시킨다면 리소스가 직접 서버에 오가는 상황이 발생하는데, 통신 상황에 따라 상당히 비효율적일 수 있기 때문에 사용한다.
- CORS에 대비가 되어 있지 않은 서버를 보호할 수 있다. 이전에 만들어진 서버들은 SOP만을 상정하여 개발되었기 때문에 다른 출처에서 들어오는 요청의 대비가 되어있지 않다.
    - 위 문제는 DELETE, PUT과 같은 데이터를 삭제 및 변경하는 메소드에서 가장 문제가 심각한데, CORS 에러가 나타나기 전에 이미 서버에서 요청을 받아 수행한 뒤, SOP로 인해 CORS 에러가 발생한다. 즉, 데이터는 이미 변경되어버릴 수 있는 심각한 문제가 있다.

### 2. 단순 요청(Simple Request)

- 특정 조건이 만족됬을 때, Prefilght Request를 생략하고 요청을 보내는 방법
- GET, HEAD, POST 요청 중 하나여야만 가능하다.
- 헤더가 Accept, Accept-Language, Content-Language, Content-Type, DPR, Downlink, Save-Data, Viewport-Width, Width일 때만 가능하다.
- Content-Type 헤더는 application/x-www-form-urlencoded, multipart/form-data, text/plain 의 값일때만 가능하다.

### 3. 인증정보를 포함한 요청(Credentialed Request)

- 요청 헤더에 인증 정보(로그인 등)를 함께 전달하는 요청 방법
- 프론트와 백엔드에서 모두 CORS 설정을 해줘야 한다.
- 프론트: 요청 헤더에 withCredentials: true를 넣어서 요청해야 한다.
- 백엔드: Access-Control-Allow-Credentials: true를 넣어서 응답해야 한다.
    - Access-Control-Allow-Origin: “*”를 설정하게 되면 CORS 정책으로 응답이 거부된다. 인증 정보를 다루는 것이기 때문에 출처를 정확하게 설정해줘야 한다.

## 처음 듣거나 어려웠던 부분(암기할 부분)

CSRF