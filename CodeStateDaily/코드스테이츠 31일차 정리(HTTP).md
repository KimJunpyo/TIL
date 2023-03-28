# 코드스테이츠 31일차 정리(HTTP)

생성일: 2023년 3월 28일 오후 12:24
태그: 코드스테이츠 일일 정리

# 클라이언트-서버 아키텍쳐(2티어 아키텍쳐)

> 리소스가 존재하는 곳(서버)과 리소스를 사용하는 앱(클라이언트)을 분리시킨 아키텍쳐
> 
- 클라이언트-서버 아키텍쳐를 사용하지 않으면 앱에 리소스가 함께 저장되어야 함
- 리소스가 업데이트가 될 때마다 앱 자체를 업데이트 해야하기 때문에 나타난 개념
- 클라이언트를 제작하는 개발자를 프론트엔드 개발자라고 부른다.

## 3티어 아키텍쳐

> 데이터베이스 - 서버 - 클라이언트의 3단계 구조를 가진 아키텍쳐
> 
- 서버에서 데이터를 보관하지 않고 데이터베이스에 리소스를 저장하며, 클라이언트에서 요청을 받으면 데이터베이스에서 데이터를 가져와 클라이언트에 전달한다
- 서버와 데이터베이스 시스템 설계를 제작하는 개발자를 백엔드 개발자라고 부른다.

# 프로토콜의 주요 종류

## OSI 7계층의 응용 계층 프로토콜

**HTTP**: 클라이언트-서버 프로토콜이라고도 불리며, 웹에서 HTML, JSON 등의 정보를 주고받는 프로토콜

**HTTPS**: HTTP에서 보안을 강화한 프로토콜

**FTP**: 파일 전송 프로토콜

**SMTP**: 메일 전송 프로토콜

**SSH**: CLI 환경 원격 컴퓨터 접속 프로토콜

**RDP**: Windows 계열 원격 컴퓨터 접속 프로토콜

**WebSocket**: 실시간 통신, Push등을 지원하는 프로토콜

## 전송 계층 프로토콜

**TCP**: HTTP, FTP 통신의 근간이 되는 인터넷 프로토콜

**UDP**: 단방향으로 작동하여 단순하고 빠르지만 신뢰성이 낮은 인터넷 프로토콜

## API(Application Programming Interface)

> 클라이언트와 서버가 의사소통을 하기 위해 제공하는 인터페이스
> 
- API에는 주소 자체에 데이터를 작성하여 요청하는 Parameter 방식과 새로운 하위 주소로 접근하는 Query 방식이 있다.
- CRUD 방식으로 목적에 맞게 API를 요청해야 하며, 프론트엔드에서 CRUD는 특정 메소드로 API 요청을 할 수 있다.
    - Create: POST
    - Read: GET
    - Update: PUT, PATCH
    - Delete: DELETE

## URL(Uniform Resource Locator)

> 네트워크 상에서 웹 페이지, 이미지, 동영상 등의 리소스 위치를 참조하는 문자열
> 
- 필수 요소인 scheme, hosts, url-path / 선택 요소인 port로 구성되어 있다.
- 일반적으로 웹 사이트의 주소를 의미한다.

## URI(Uniform Resource Identifier)

> 네트워크 상에서 리소스를 고유하게 식별할 수 있는 정보를 제공하는 개념
> 
- URL에 query, fragment를 포함하는 URL의 상위개념이다.
- scheme, hosts, url-path / 선택 요소인 port, query, fragment로 구성되어 있다.
- 백엔드와 데이터를 공유할 때는 데이터의 위치, 원하는 데이터, 개수 등 리소스를 식별할 수 있는 데이터를 알아야 하기 때문에 URI로 통신한다.

## URI의 구성종류 설명

| 명칭 | 구분 | 설명 |
| --- | --- | --- |
| scheme | file://, http://, https:// | 통신 프로토콜 |
| hosts | 127.0.0.1, www.google.com | 웹 페이지, 이미지 등 파일의 리소스 위치 도메인 또는 IP |
| url-path | /search, /users/content | 웹 서버의 루트부터 파일의 위치까지의 경로 |
| port | :80, :443, :3000 | 웹 서버에 접속하기 위한 통로 |
| query | ?id=asd1234 | 웹 서버에 전달하는 추가 질문 |
| fragment | #user, #section1 | 현재 파일 문서의 id 요소로 이동 |

### 크롬 브라우저 에러 메세지 확인 방법

> chrome://network-errors/ 검색
> 

# HTTP Messages

> Requests, Responses 유형이 있으며 클라이언트와 서버 사이에서 데이터가 교환되는 방식
> 

## HTTP Requests

> 클라이언트가 서버에 보내는 메세지
> 
- start line
    - 수행할 작업(GET, POST 등)이나 방식(HEAD, OPTIONS)을 설명하는 HTTP method
    - 요청 대상 또는 프로토콜, 포트, 도메인의 절대 경로( origin, absolute, authority, asterisk 표현 방식 )
    표현 방식은 HTTP Method마다 다르다.
    - HTTP 버전
- Headers
    - Request headers: fetch를 통해 가져올 리소스나 클라이언트 자체에 대한 자세한 정보를 포함하는 헤더를 의미
    - General headers: 메세지 전체에 적용되는 헤더
    - Representation headers: body에 담긴 리소스의 정보(콘텐츠 길이, 타입 등)
- Body
    - Body는 크게 두 가지의 종류로 나뉜다.
    - Single-resource bodies(단일-리소스 본문) : 헤더 두 개(Content-Type, Content-Length)로 정의된 단일 파일
    - Multiple-resource bodies(다중-리소스 본문): 본문이 여러 파트로 나뉘어져 있고, 각 파트마다 가지고 있는 정보가 다름[( HTML Form과 관련이 있음 )](https://developer.mozilla.org/en-US/docs/Learn/Forms)

## HTTP Responses

> 서버가 클라이언트에게 보내는 메세지
> 
- status line
    - HTTP 버전
    - 상태 코드(200, 302, 404 등)
    - 상태 텍스트(상태 코드에 대한 설명)
- Headers
    - Response headers: 서버 자체에 대한 정보(이름, 버전)와 같은 응답에 대한 부가적인 정보
    - General headers: 메시지 전체에 적용되는 헤더
    - Representation headers: body에 담긴 리소스의 정보(콘텐츠 길이, 타입 등)
- Body
    - Body는 크게 두 가지의 종류로 나뉜다.
    - Single-resource bodies(단일-리소스 본문) : 헤더 두 개(Content-Type, Content-Length)로 정의된 단일 파일
    길이를 모르는 파일의 경우, Transfer-Encoding: chunked로 설정되어 있고 파일이 chunk로 나뉘어 인코딩됨.
    - Multiple-resource bodies(다중-리소스 본문): 본문이 여러 파트로 나뉘어져 있고, 각 파트마다 가지고 있는 정보가 다름

## ajax 통신

> Asyncronous JavaScript And XML의 약자로, 자바스크립트를 통해 서버에 데이터를 요청하는 것
> 
- 브라우저가 가지고 있는 XMLHttpRequest 객체를 통해 Client와 서버 간의 XML 데이터를 주고받는 통신 기술이다.
- 하지만, ajax 통신은 여러가지 단점으로 인해 최근엔 사용이 잘 되지 않는다.
    1. 히스토리 관리가 되지 않는다.
    2. 통신 진행 상황을 확인 할 수 없다.
    3. 이전 브라우저, 시각 장애인용 브라우저에서는 AJAX 지원이 불가능하다.
    4. Cross Domain(다른 도메인과 통신하는 것) 지원을 하지 않는다.
    5. XML을 통신하는 것 보다 JSON 통신을 훨씬 더 많이 사용한다.
    6. fetch, axios와 같은 ajax 통신의 단점을 보완한 promise형 http 비동기 통신 방법이 생겨남

## SSR(Server Side Rendering)

> 웹 페이지를 브라우저에서 렌더링 하는 대신 서버에서 렌더링하여 페이지를 보여주는 방법
> 
- 서버의 URI에 GET 요청을 보내면, 서버는 렌더링된 웹 페이지를 브라우저로 전송한다.
- 장점
    1. 하나의 HTML 파일로써 완성된 문서가 서버에서 넘어오기 때문에 SEO에 유리하다.(검색엔진에서 더 잘 노출될 수 있다.)
    2. 웹 페이지의 첫 페이지를 빠르게 렌더링 해야 하거나, 페이지나 파일들의 크기가 작은 소규모 페이지에서 속도가 빠르다.
- 단점
    1. 다른 페이지를 들어갈 때마다 동일한 작업을 반복하기 때문에 서버 과부하가 심하다.
    2. 상호작용이 많은 페이지는 상호작용을 할 때마다 새로운 웹 페이지를 서버에서 받아오기 때문에 서버 과부하가 심하다.

## CSR(Client Side Rendering)

> 웹 페이지를 브라우저에서 렌더링하는 방법
> 
- 서버의 URI에 요청을 보내면, 서버는 웹 페이지의 데이터를 제외한 화면을 그리는 코드와 JS 파일을 전송받아서 브라우저에서 렌더링된다. ⇒ 위 과정에서 모든 파일을 받아온다.
- 필요한 데이터만을 요청하고 받는다.
- 장점
    1. 필요한 상황에서 데이터만 요청하고 받기 때문에 서버 과부하가 적다.
    2. 모든 파일을 가져오기 때문에 라우팅을 시도했을 때 빠르게 화면 전환이 이루어진다.
    3. 상호작용을 시도했을 때 데이터만 송수신 하기 때문에 통신 시간이 짧아서 변화가 빠르다.
- 단점
    1. 웹 페이지의 첫 페이지에서 모든 파일들을 받아올 때까지 화면은 비어있으며, 파일의 용량이 크고 많을수록 느리다.
    2. 빈 html을 받아서 그림을 그리는 것이기 때문에, SEO가 좋지 않다.
    ⇒ 하지만 이 케이스는 Next.js라는 프레임워크가 등장하면서 많이 해소되었다.

## 처음 듣거나 어려웠던 부분(암기할 부분)

아키텍쳐: 서비스의 동작 원리

프로토콜: 시스템이 다른 시스템들과 통신하기 위해서 사용되는 통신 규약

HTTP: 클라이언트-서버 프로토콜이라고도 불리며, 웹에서 HTML, JSON 등의 정보를 주고받는 프로토콜

[localhost](http://localhost): 127.0.0.1의 주소를 가진 hosts이고, 127.0.0.1은 나의 PC를 가리킴

IP: Internet Protocol의 줄임말로, 인터넷상에서 사용하는 주소체계

Domain name: ip를 대신하여 사용하는 주소(ip는 주소, 도메인 이름은 상호로 볼 수 있다)

DNS: Domain Name System으로 도메인 이름을 IP 주소로 변환하거나 IP 주소를 도메인 이름으로 변환하는 데이터베이스 시스템