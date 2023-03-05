# 3주차 new information

다중 선택: Error, Method
생성일: 2023년 2월 27일 오전 9:23
태그: 코드스테이츠 주간 정리

### slice() VS splice()

> slice, splice는 배열을 특정 범위로 자르는 메소드들이다.

slice : start, end를 이용해 범위를 특정하고 그 범위 내의 값들을 가진 새로운 배열을 생성 및 반환한다.

**Use : Array이름.slice(1, 2) ⇒ 1번 요소 삭제**

splice : start, deleteCount, item을 이용해 시작 범위를 정하고, deleteCount만큼 값을 제거한 뒤, item을 추가한다.

**Use : Array이름.splice(2, 4, 5) ⇒ 2번 요소의 다음인 3번 요소부터 4개를 제거하고 삭제된 자리에 5 추가**

**⭐ slice는 새로운 배열을 생성, splice는 원본 배열 자체를 변경한다.**

---

**SyntaxError** : 문법적으로 유효하지 않은 코드를 해석하려고 시도할 때 발생하는 오류

---

## 객체 추가 정리

### 1. 빈 객체 생성

```jsx
let myProfile = new Object(); //빈 객체 생성
myProfile.firstName = "김";
myProfile["secondName"] = "준표";

let myProfile = {}; //빈 객체 생성
```

### 2. hasOwnProperty()

**prototype 속성**으로 생성된 키를 제외하고 객체 스스로가 만들어낸 키들 중에 존재하는지의 여부 판단

```jsx
let obj = {
	a : 1,
};

obj.b = 2;
Object.prototype.c = 3; // 모든 객체에 c = 3 이라는 키-값이 생성됨

obj.hasOwnProperty("a") // true
obj.hasOwnProperty("b") // true
obj.hasOwnProperty("c") // false - prototype으로 생성되어서 false 반환

```

### 3. prototype 객체(나중에 OOP에서 자세히 공부)

- 새로운 객체가 생성되기 위한 원형이 되는 객체
- prototype : 원형이 되는 객체들을 포함한 상위 객체들에게 상속받은 정보(상위 객체에서 만든 메소드 혹은 데이터들)

### 4. for in

- 객체에서 사용 가능한 반복문 형태, 객체의 키 값을 반복문 변수에 넣어서 사용하는 방식

```jsx
let obj = {a:1, b:2, c:3};

for(let i in obj){
	console.log(i); // a, b, c가 한 줄에 하나씩 차례대로 출력
}
```

### 5. 객체 원본 데이터 변경

- **⚠️ 함수로 넘어온 객체의 값을 변경해도 원본 객체가 함께 변한다 ⚠️**

### 6. Object.keys(), Object.values(), Object.entries()

- 객체의 키, 값, 키와 값들을 배열로 반환하는 메소드
- entries()는 이차원 배열로 입력된다.

### 7. Object.assign()

- 객체들의 내부 요소들을 합치는 메소드
- 중복된 key가 있다면, 뒤에 합쳐지는 객체의 key의 value값으로 덮어진다.

```jsx
const target = { a : 1, b : 2}
const source = { c : 3, d : 4}

const returnedObject = Object.assign(target, source);

console.log(target); // {a: 1, b: 2, c: 3, d: 4}
console.log(returnedObject); // {a: 1, b: 2, c: 3, d: 4}
```

- 위의 코드에서 볼 수 있듯이, **첫번째 객체가 두번째 객체의 값을 합친 결과로 변환되며, 반환되는 객체 또한 변환된 첫번째 객체가 반환된다.**

---

### **symbol(차후 블로깅 예정)**

- 변경 불가능한 원시 타입의 자료형
- 다른 값과 중복되지 않는 고유한 값을 가지며, 고유한 상수값을 만들때 사용할 수 있다.

```jsx
const symbolA = Symbol('a');
const symbolB = Symbol('b');

console.log(symbolA === symbolB); // false
```

---

# JSON

- JavaScript Object Notation의 약자로, 서버에서 클라이언트로 데이터를 보낼 때 사용하는 양식
- 클라이언트의 언어에 상관없이 통일된 데이터를 주고 받기 위해 일정한 패턴을 가진 **문자열**을 생성해 내보내면, 클라이언트가 자신의 언어에 맞게 데이터를 관리 및 표시할 수 있다.

## JSON.parse

- 문자열을 객체로 변환할 때 사용하는 메서드

![](https://velog.velcdn.com/images/player1552/post/3f739ff0-f9d2-48b2-8f59-d588d4f83ad2/image.png)


- 위의 사진과 같이 JSON은 key-value같은 특정 패턴을 가진 “문자열”을 반환하는데, 이 데이터들을 실제로 사용하기 위해서는 객체화를 시켜줘야 접근이 가능하다.
- console.log를 보면 parse() 메서드를 사용하기 전에는 key 값들에 큰따옴표가 쳐져 있다.
객체화 시킨 console.log는 key에 큰따옴표가 떼어져 있는데, **객체의 key에는 큰따옴표가 없다.**
- 또한, 문자열의 경우에는 당연히 내부 값을 dot notation으로 접근할 수없지만, 객체화된 경우에는 dot notation으로 값을 가져올 수 있다.

## JSON.stringify

- 객체를 문자열로 변환할 때 사용하는 메서드

![](https://velog.velcdn.com/images/player1552/post/ad73393c-efe7-4569-9b39-9a7258ff4516/image.png)

- 단순하게 생각하면 parse의 역방향 메서드라고 생각하면 된다.
- 최하단의 console.log에서는 문자열화된 값에 key를 접근할 수 없기 때문에 undefined가 출력되는 것을 볼 수 있다.

---

## ⚠️배열.reduce() 메서드⚠️

- reducer 함수와 initialValue를 인수로 받아 reducer 함수의 실행 결과값을 반환하는 메서드

```jsx
const arr = [1, 2, 3, 4, 5];

const curResult = arr.reduce((acc, cur, idx) => acc += idx, 0);
// 위의 코드는 acc를 accumulator로, cur를 현재 요소명으로, idx를 현재 요소 index명으로 표현
// acc는 initialValue의 값이 0이기 때문에 초기값 0
// acc += idx(arr의 요소 index를 가져옴, 첫번째의 경우 0) = 0
// 0 + 1 = 1 ... 6 + 4 = 10
console.log(curResult); // 10

const idxResult = arr.reduce((acc, cur, idx) => acc += cur, 0);
// acc 초기값 = 0, acc += cur(arr의 요소를 가져옴, 첫번째의 경우 1)
// 0 + 1 = 1 ... 10 + 5 = 15
console.log(idxResult); // 15

const fiftyResult = arr.reduce((acc, cur, idx) => acc += cur, 50);
// acc 초기값 = 50(initialValue가 50), acc += cur = 50 + 1 = 51 ... 60 + 5 = 65
console.log(fiftyResult); // 65
```

- reducer : reduce 함수에 전해지는 매개변수들을 통해 진행되는 내부 함수
- reducer 매개변수
    - accumulator(누산기)
    1. initialValue에 값이 있다면 initialValue의 값을 초기값으로 가지며, 값이 없다면 첫 번째 요소의 값을 가짐
    2. 최종적으로 반환될 값이 누적되다가 함수가 종료되면 accumulator의 값이 반환됨
    - currentValue(현재 요소) : 현재 요소의 값을 나타내는 매개변수명을 작성함
    - currentIndex(Optional, 현재 요소 인덱스) : 현재 요소의 index 값을 나타내는 매개변수명을 작성함
    - array(Optional, reduce()를 호출한 배열) : reduce가 호출된 배열을 나타내는 매개변수명을 작성함
- initialValue(Optional) : 첫 번째 인수에 제공하는 초기값, 초기값을 지정해주지 않으면 배열의 첫번째 요소가 초기값이 됨

### ⭐reducer의 자리에는 외부 함수 또한 입력이 가능하다.

---

## strict mode

- 브라우저가 **엄격하게 코드를 체크하고 관리**하도록 만들어주는 모드
- 사용법 : ‘use strict’;
- 키워드 선언이 없는 변수 할당과 같은 문법적인 실수들도 에러로 판단하여 메세지를 출력해준다.

## 단어 정리(추가로 공부하여 글로써 정리할 내용들은 별표)

클로저 : 함수와 그 함수가 접근할 수 있는 변수의 조합

커링 : 여러 전달인자를 가진 함수를 연속적으로 리턴하는 함수로 변경하는 행위

모듈 : 하나의 기능을 온전히 수행하기 위한 모든 코드를 가지고 있는 코드 모음