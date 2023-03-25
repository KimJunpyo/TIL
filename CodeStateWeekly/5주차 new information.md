# 5주차 new information

생성일: 2023년 3월 13일 오후 10:27
태그: 코드스테이츠 주간 정리

## throttle

> 이벤트 핸들러가 호출되는 빈도를 제한하는 기술
> 
- 스크롤을 내릴때마다 이벤트 핸들러가 호출되는 이벤트가 있을 때, 진행중인 스크롤 이벤트가 있다면 진행을 하지 못하게 하는 기술이다.
- ex) 스크롤 이벤트 핸들러에 setTimeout으로 5초를 추가하고 throttle 방식을 이용한다면,
1. 처음 스크롤을 움직였을 때 함수 실행
2. 5초동안 스크롤 이벤트 핸들러가 동작
3. 5초 안에 스크롤을 다시 하게 되면, 스크롤 이벤트 핸들러 실행이 불가함
4. 5초 뒤에는 다시 스크롤 이벤트 핸들러 동작

## debounce

> 가장 마지막에 호출되는 이벤트 핸들러가 일정 시간 이후, 동작하게 하는 기술
> 
- 검색페이지에서 타이핑을 할 때, 타이핑이 모두 끝난 이후 일정 시간이 지났을 때 연관 검색어 API를 호출하여 화면에 보여주도록 하는 기술이다.
- ex) 이벤트 핸들러에 setTimeout으로 5초를 추가하고 debounce 방식을 이용한다면,
1. 키를 입력할 때 마다, 입력 이벤트 핸들러 호출
2. 5초안에 새로운 이벤트가 동작되었을 때, 현재 5초를 대기하고 있던 setTimeout 함수를 삭제 후 새로운 setTimeout 함수를 호출
3. 키를 5초동안 입력하지 않으면, setTimeout 함수에 있는 콜백 함수가 동작

## 엣지 케이스

> 소프트웨어 개발에서 예상치 못한 상황이나 예외 상황을 나타내는 용어
> 
- ex) 입력값에 대한 유효성 검사를 하는 과정중에 undefined, null, 공백 등 의도치 않은 값이 들어오는 경우

## 보일러 플레이트

> 소프트웨어 개발에서 반복적으로 사용하는 코드
> 
- 개발자가 자주 사용하는 코드 패턴, 기본적인 코드의 구조를 의미한다.
- 보일러 플레이트를 이용해서 코드를 작성하면 개발의 효율성 및 가독성을 높일 수 있다.

## 추가 고차함수

forEach, find, findIndex, sort, some, every, flat, flatMap

## MapReduce Model

> Map 함수와 Reduce 함수를 사용하여 대규모 데이터 처리를 하는 모델
> 
- 기본적인 구조는 Map 함수로 특정 데이터를 매핑 ⇒ Reduce 함수로 매핑된 데이터의 중간 결과값 데이터 생성을 반복한다.
- ex) 김으로 시작하는 name 데이터 매핑 ⇒ 매핑된 데이터들에서 성적을 모두 합산
      박으로 시작하는 name 데이터 매핑 ⇒ 매핑된 데이터들에서 성적을 모두 합산
       …
      결과 데이터를 합산하여 최종 결과값 도출
- 한번에 수많은 데이터를 매핑 및 결과값 도출을 하기에는 부적절하기 때문에 사용되는 방식이다.

## 커링과 클로저

> 클로저는 외부 함수의 변수에 접근할 수 있는 내부 함수
커링은 클로저의 원리를 이용한 함수 표현 기법이며, 함수를 반환하는 함수
> 

## 절차형 프로그래밍, 선언형 프로그래밍의 차이

절차형 프로그래밍은 **“어떻게”** 할 것인가에 초점이 맞춰져있는 **순서 프로그래밍 방식**이다.

선언형 프로그래밍은 **“무엇을”** 할 것인가에 초점이 맞춰져있는 **논리 프로그래밍 방식**이다.

```jsx
// 절차형 프로그래밍 - 어떤 방식으로 원하는 결과를 만들 것인지를 추구
function Multiply(arr, n) {
	let result = [];
	for(let i = 0; i < arr.length; i++){
		result.push(arr[i] * n);
	}
	return result;
}

// 선언형 프로그래밍 - 메소드를 이용해서 추상화된 코드를 작성하는 방향 추구
function Multiply(arr, n) {
	return arr.map(e => e * n);
}
```

## 클래스와 프로토타입에 대한 개념

1. 클래스를 선언하면 같은 depth에 constructor, prototype 객체가 정의된다.
2. constructor에는 prototype 객체에 접근할 수 있는 prototype 프로퍼티가 존재하며, prototype 객체에는 constructor에 접근할 수 있는 constructor 프로퍼티가 존재한다.
3. 따라서 prototype 객체에 접근하기 위해서는 constructor.prototype으로 접근해야 한다.
4. 클래스를 상속받은 경우, 부모 클래스의 prototype 객체를 담고 있는 새로운 객체를 생성한 뒤 자식 클래스의 prototype 객체에 저장되며, __proto__ 프로퍼티에는 부모 클래스의 prototype 객체 주소값이 들어간다.
5. 자식 클래스에서 부모 클래스의 prototype에 접근하기 위해서는 prototype 객체를 호출해야 하는데, 이 때, __proto__로 값을 접근해야 한다.
6. 자식 클래스.prototype.__proto__를 하게 되면, prototype 안에 __proto__가 부모 주소값을 가졌기 때문에 부모 클래스의  prototype 객체에 접근할 수 있다.
7. 하지만, 자식클래스.__proto__를 하게 되면 prototype 체인을 확인하지 않고 부모 클래스 내에 있는 constructor를 호출하게 된다.

```jsx
class A {
    constructor() {
        this.name = "asd";
    }
    getYes () {
        return "yes";
    }
}

class B extends A {
    constructor() {
        super();
    }
}

const C = new B();

console.log(C.prototype); // undefined
// 인스턴스는 prototype이 없다.

console.log(C.__proto__); // B.prototype
console.log(C.constructor.prototype); // B.prototype
// 인스턴스의 __proto__에는 인스턴스를 만든 클래스의 prototype
// 객체 주소값을 가지고 있다.
// 인스턴스.constructor는 인스턴스를 만든 클래스의 constructor를 의미
// 인스턴스.constructor.prototype === 클래스.prototype

console.log(B.prototype); // B.prototype
console.log(B.prototype.__proto__); // A.prototype
// B 클래스의 prototype에는 자기 자신의 prototype을 의미
// B 클래스의 prototype.__proto__는 부모 클래스의 prototype을 의미

console.log(B.__proto__); // 부모 클래스의 constructor
// 자식 클래스의 prototype 내에 있는 __proto__ 에만 주소값이 들어가고
// 자식 클래스가 가진 내부 __proto__는 자신의 부모 클래스 constructor
// 가 들어간다.
```