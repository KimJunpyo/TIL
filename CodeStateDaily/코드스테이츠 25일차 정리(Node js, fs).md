# 코드스테이츠 25일차 정리(Node.js)

생성일: 2023년 3월 20일 오후 1:09
태그: 코드스테이츠 일일 정리

# Node.js

> 비동기 이벤트 기반 Javascript 런타임
> 

[내장 모듈 목록](https://nodejs.org/dist/latest-v16.x/docs/api/)

## Node.js 파일 시스템 모듈

### readFile

> readFile(path[, options], callback)
> 
- path는 파일의 경로를 전달인자로 받는다.
사용할 수 있는 타입은 (string, buffer, url, integer)가 가능하다
- options는 문자열 혹은 객체로 받을 수 있으며, 문자열의 경우에는 utf8과 같은 인코딩 형태를 보내야 합니다.
추가적으로, options를 객체의 형태로 보내는 코드의 예시이다.

```jsx
let options = {
	encoding: 'utf8', // 인코딩 방식
	flag: 'r' // 읽기 전용
}
// encoding 형태와 사용 형태를 한번에 정의해주기 위해서 객체 형태로 보냄

fs.readFile('/etc/passwd', options, ...);
```

- callback은 파일을 읽은 뒤, 비동기적으로 실행할 함수를 전달인자로 받는다.
err, data의 매개변수가 있으며 err은 에러를 의미하고 에러가 발생하지 않으면 null을 가진다.
data는 파일의 내용이며, 문자열 혹은 버퍼를 가진다.
**⚠️utf8과 같이 인코딩을 해주지 않으면, data에 버퍼로 입력된다.⚠️**

### writeFile

> readFile과 사용법은 동일하지만, 파일을 읽는게 아닌 생성한다.
> 

## require 구문

- <script src=”원하는 js 파일”></script> 처럼 특정 파일을 불러오는 구문이다.
- require(”fs”), require(”dns”)와 같은 형태로 사용한다.

## 3rd-party 모듈

- 프로그래밍 언어에서 제공하는 빌트인 모듈이 아닌 외부 모듈을 말한다.
- npm install ㅇㅇ 의 형태로 다운받는다.

## 처음 듣거나 어려웠던 부분(암기할 부분)

require 추가 정보: 1. common.js 2. module.export 관련된 것으로 작성 - test3, 4로 공부

오류 : illegal operation on a directory : 파일을 불러올 때 폴더를 부른 경우에 발생하는 에러

CRLF, LF의 차이