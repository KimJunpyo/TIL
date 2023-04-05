# 코드스테이츠 15일차 정리(this, Array.from)

생성일: 2023년 3월 6일 오전 9:26
태그: 코드스테이츠 일일 정리

# this

### 여러 호출 방식에 따라 정의가 달라지는 실행 함수의 호출자이다.

(너무 많고 다양한 의미로 부르기에, 내가 이해할 수 있는 언어로 작성했다.)

## 함수 호출

```jsx
const func = function(){
	const name = "1";
	console.log(this);
	console.log(this.name);
}

func(); // 출력 : window 객체, 빈 값
```

- 일반적인 함수 내에서 this는 전역 객체를 바인딩함
- this.name의 경우 window의 name을 가져온다.(값이 없기 때문에 빈 값 출력)

## 메소드 호출

```jsx
const o = {
	prop: 55,
	foo: function() {
		return this.prop;
	}
}

console.log(o.f()) // 출력 : 37
```

- 객체 안에 있는 함수(메소드)에서의 this는 해당 메소드를 소유한 객체에게 바인딩됨
- 객체안에 있는 값들을 모두 사용할 수 있음

## 객체 생성 함수

```jsx
function getUserInfo(){
	this.name = "김준표",
	this.age = "26",
	this.tall = "186"
}

const user = new getUserInfo();

console.log(user); // {name: "김준표", age: "26", tall: "186"}
```

- 객체 생성 함수를 호출 시, this는 생성된 객체에게 바인딩됨
- 실제로 객체에 this뒤에 붙은 이름들을 가진 key와 값인 value로 변경되어 적용됨.

apply, call, bind 메소드를 통해 특정 객체에 this를 명시적으로 바인딩 할 수 있다.(4주차 정리 내용에 포함)

[https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/this](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/this)

## arguments

함수에 전달된 매개변수들을 index : value의 형태로 변경해 가지고 있는 객체

```jsx
function foo(10, 20, 50){
	console.log(arguments[0]); // 출력 : 10
  console.log(arguments[1] + arguments[2]); // 출력 : 70
}
```

- ES6에 들어서는 arguments보다 Rest 문법으로 표현하는 방식을 더 선호한다.

## Array.from

- 유사 배열 객체, 반복 가능한 객체, 문자열을 얕은 복사를 통해 새로운 배열을 만드는 메소드

```jsx
console.log(Array.form("kim")); // 출력 : ["k", "i", "m"]
console.log(Array.form([1, 2, 3], x => x + x));
// 출력 : [2, 4, 6]
```

- 문자열도 분해 후, 배열로 변환 가능하다.

## 처음 듣거나 어려웠던 부분(암기할 부분)

바인딩 : 특정 객체에 연결되는 것

apply, call, bind 메소드를 통해 특정 객체에 this를 명시적으로 바인딩 할 수 있다.(4주차 정리 내용에 포함)