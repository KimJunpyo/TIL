# 코드스테이츠 8일차 정리

생성일: 2023년 2월 22일 오전 11:32
태그: 코드스테이츠 일일 정리

## ES6 문법

### 기본값 할당 방식

1. **함수 내부 할당**

```jsx
function sum(x, y) {
	x = x || 0; // 매개변수에 값이 들어오지 않으면 undefined가 됨(falsy)
	y = y || 0; // falsy || 0으로 undefined라면 0이라는 기본값을 할당

	return x + y;
}

console.log(sum()); // 0
console.log(sum(2)); // 2
console.log(sum(3, 5)); // 8
```

1. **매개변수 할당**

```jsx
function sum(x = 0, y = 0) { // 함수 매개변수 자체에 기본값을 할당
	return x + y;
}

console.log(sum()); // 0
console.log(sum(2)); // 2
console.log(sum(3, 5)); // 8
```

### 스프레드 문법

```jsx
function sum (arr) {
    console.log(...arr) // 1, 2, 3, 4
    console.log(arr) // [1, 2, 3, 4]
}

sum([1, 2, 3, 4]);
```

### 레스트 파라미터

```jsx
function foo(...rest) {
  console.log(rest); // [ 1, 2, 3, 4, 5 ]
}

foo(1, 2, 3, 4, 5);
```

### 스프레드 문법은 배열의 요소들을 개별로 분리시키는 방식

### 레스트 파라미터는 배열로 만드는 방식

! 레스트 파라미터는 마지막 파라미터여야 한다.

### 객체 반복문

for-in, for-of

### 크롬 debugger

브라우저 엔진에서 **디버깅**을 도와주는 도구

1. 순차적으로 코드가 진행되는 것을 한 줄 한 줄씩, 데이터와 함께 확인 할 수 있음
(f9 : 코드 한 줄 씩 이동하는 버튼)
2. **중단점(Break Point)**를 작성하여 특정 위치 내에서 혹은 빠른 진행을 위해서 설정(함수마다 설정하는 편)
3. **js 코드 내에 debugger; 를 작성하면 자동으로 중단점이 생성됨**

### 원시 자료형

     string, number, bigint, boolean, undefined, symbol, null

### 원시 자료형은 값의 변화가 불가능하다.

값을 변경하는 방식이 아닌, 할당하는 방식으로 처리한다.

(str[1] = “z” 와 같은 방식은 원시 자료형에서 불가능)

### 참조 자료형

     배열, 객체, 함수

### 참조 자료형은 index, key 등을 참조하여 값을 변경할 수 있다.

(원시 자료형과 다르게 참조 자료형은 동적 데이터 보관함으로 주소를 통해 연결되어 있다.)