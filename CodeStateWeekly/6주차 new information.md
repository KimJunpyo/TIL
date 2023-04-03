# 6주차 new information

생성일: 2023년 3월 21일 오전 9:59
태그: 코드스테이츠 주간 정리

# Javascript는 싱글 스레드인데 어떻게 비동기 환경이 구현될 수 있을까?

~~심연을 보고 와서 나중에 하겠습니다.~~

- 이 개념을 알기 위해서는 이벤트루프, 콜 스택, 콜백 큐에 대한 개념을 알아야 한다.
- 그러므로, 아주 간단하게 요약하면 “싱글 스레드 형식으로 함수를 처리하는 콜스택이 있고, 콜 스택에 값이 빌 때마다 콜백 큐에 대기중인 함수를 콜스택으로 불러와서 실행”

## async / await 추가 공부

### 1. async / await은 try-catch문과 함께 사용된다.(필수는 아니다)

```jsx
const callMe = async() => {
	try {
		await calling();
		await calling();
	}
	catch (err) {
		console.log("통신이 가지 않습니다.");
	}
}

const calling = () => console.log("call");

callMe();
```

- try-catch문은 try에 있는 코드에서 에러가 발생하면 catch문을 동작시켜 예외처리를 할 수 있는 예외처리문이다.
- 하지만, callMe에 then을 붙이게 되면, error가 발생하여 내부에서 catch가 동작되어도 then이 동작한다(!!)
- 즉, 내부에서 try-catch를 사용한 경우, throw err와 같이 error 신호를 반환하여 callMe의 then 또한 동작되지 않도록 error handling을 해야한다.

### 2. async 함수의 return값은 암묵적으로 promise에 감싸진다.

```jsx
const foo = async() => {
	return 1;
}

const foo = () => {
	return Promise.resolve(1);
}
```

- 위 코드처럼, async foo 함수에서 return으로 값을 보내게 되면, 자동으로 Promise에 감싸져 resolve로써 반환된다.

```jsx
const foo = async() => {
	await 1;
}

const foo = () => {
	return Promise.resolve(1).then(() => undefined);
}
```

- 반환 값이 없이 await 1이라는 코드를 입력하면, 아래의 코드처럼 변경되어 반환된다.
- await으로 인해 비동기적으로 코드가 진행되며, then에서는 반환값이 없다는 의미의 undefined가 반환된다.

 

## CRLF, LF의 차이

- 새줄 문자의 차이이다.
- 리눅스는 LF(\n)으로 새줄을 표현한다.
- 윈도우는 CRLF(\r\n)으로 새줄을 표현한다.
- 따라서 리눅스에서 작성된 파일을 윈도우에서 작성한 문자열과 비교했을 때에는 문제가 발생할 수 있다.

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

## reportWebVitals?

> CRA 서드파티 라이브러리로, reportWebVitals(console.log) 라는 사용 방법으로 콘솔창에 앱의 퍼포먼스들을 분석하여 객체 형태로 나타내는 React 분석 도구이다.
> 

## WireFrame → MockUp → Prototyping

### WireFrame

> 웹 페이지의 레이아웃, UI 요소 등에 대한 뼈대를 만드는 방법
> 
- 웹 페이지 디자인을 하기 전에 선을 이용해 구조를 표시하는 방법이다.

### MockUp

> WireFrame의 뼈대에 색상, 사진 등을 추가하여 시각적으로 화면의 디자인을 표현하는 방법
> 
- 이 레이아웃에서 어느 위치에 어떤 데이터가 나타나고 어떤 디자인이 들어갈 것인지를 나타내는 모형이다.

### Prototyping

> WireFrame으로 구조를 짜고, MockUp으로 시각적인 디자인이 만들어졌을 때, 특정 상호작용에 따른 화면간 이동의 흐름을 표기하는 방법
> 


![](https://velog.velcdn.com/images/player1552/post/f48e2c7a-19f5-4792-b02e-dd93484f0bf1/image.png)출처: [https://webbybutter.com/difference-between-wireframe-mockup-and-prototype/](https://webbybutter.com/difference-between-wireframe-mockup-and-prototype/)

### prototyping 디자인 방법
![](https://velog.velcdn.com/images/player1552/post/dc617bee-7a3a-421c-a0c6-5f13a5276e3c/image.png)출처: [https://moqups.com/](https://moqups.com/)

# 단어

**illegal operation on a directory**: 파일을 불러올 때 폴더를 부른 경우에 발생하는 에러

**Hot reloading**: 페이지를 전체 리렌더링 하지 않고, 수정된 특정 부분들만 업데이트가 되는 렌더링 방식 ~~(얘도 공부하다가 심연을 봤습니다. 개념만 아시면 됩니다….)~~

**JSX(JavaScript XML)**: JavaScript를 확장한 문법이며, Babel을 통해 브라우저에서 JavaScript 코드로 컴파일된다.

**<code\>**: 프로그래밍 코드를 입력할 때 사용하는 시맨틱 태그, 보통 한 줄로 된 코드만 읽는다.
두 줄 이상의 코드를 출력하고 싶을때는 pre를 사용한다.
