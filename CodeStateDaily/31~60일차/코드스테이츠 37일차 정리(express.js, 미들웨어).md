# 코드스테이츠 37일차 정리()

생성일: 2023년 4월 5일 오전 10:26
태그: 코드스테이츠 일일 정리

## MERN stack

> MongoDB, Express.js, React.js, Node.js를 지칭하는 것
> 
- 위 네 가지의 기술 스택들로 앱을 만들 수 있고, 그렇게 만들어진 앱을 MERN stack 기반 앱이라고 한다.

## express.js

> Node.js 환경에서 웹 서버 혹은 API 서버를 제작하기 위해 사용되는 프레임워크
> 
- HTTP 모듈로 개발한 서버와의 차이점
    1. Express 프레임 워크는 미들웨어를 추가할 수 있다.
    2. HTTP 메소드를 이용한 라우팅 기능을 제공한다.

## 미들웨어(middle-ware)

> 클라이언트에게서 온 요청에 대한 응답을 하기 위해 코드 진행의 중간마다 수행되는 함수
> 

### 미들웨어를 사용하는 상황 4가지

1. **POST 요청 등에 포함된 body(payload)를 구조화할 때**
    - body-parser 미들웨어를 이용하여 body를 구조화할 때 사용할 수 있다.
    
    ```jsx
    npm install body-parser
    
    const bodytParser = require('body-parser');
    const jsonParser = bodyParser.json();
    
    app.post('/users', jsonParser, (req, res) => {});
    ```
    
    - 하지만, Express.js의 업데이트로 인해 최근에는 위와 같은 방법으로 body를 구조화하지 않고 express.json() 이라는 내장 미들웨어를 사용할 수 있다.
2. **모든 요청/응답에 CORS 헤더를 붙여야 할 때**
    - 헤더를 붙이는 경우에는 객체안에 Access-Control 관련 헤더들을 작성하여 응답 Message의 헤더에 함께 보내줘야 한다.
    - 하지만, cors 미들웨어를 사용하면 app.use(cors()) 라는 코드로 간단하게 cors 처리가 가능하다.
3. **모든 요청에 대해 URL이나 메소드를 확인할 때**
    - 프로세스 중간에 특정 역할을 수행하는 미들웨어를 직접 구현할 수 있다.
    
    ```jsx
    app.get('/', function(req, res, next) {
    	next();
    })
    ```
    
    - next()를 이용하여 현재 미들웨어의 다음 미들웨어를 실행시키는 구조를 담당한다.
4. **요청 헤더에 사용자 인증 정보가 담겨있는지 확인할 때**
    - 인증 정보 관련 헤더 데이터(token 등)의 유무를 판단하고 존재하지 않을때는 통신 에러를 나타내고, 존재할때는 next() 를 이용하여 다음 미들웨어로 동작시키는 로직을 작성하여 사용한다.

## 처음 듣거나 어려웠던 부분(암기할 부분)

React.js는 라이브러리이고, React.js와 서드 파티 라이브러리들을 함께 사용하여 하나의 앱을 만든 경우 “React 기반에 라이브러리를 추가한 React 프레임워크로 만들어진 앱이다.” 라고 의미할 수 있다.

Vue.js는 프로그레시브 프레임워크이고, Vue.js는 설계부터 라이브러리처럼 사용할 수 있게끔 만들어졌고, 그로인해 라이브러리라고 통상적인 표현을 할 수 있다. 이는 React를 React 프레임워크라고 통상적으로 이야기 할 수 있는 것과 같은 맥락이다.