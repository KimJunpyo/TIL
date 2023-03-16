# 코드스테이츠 23일차 정리(prototype chain)

생성일: 2023년 3월 16일 오후 12:29
태그: 코드스테이츠 일일 정리

# 프로토타입 체인

> Javascript에서 객체 간의 상속을 구현하는 방법으로, 객체가 원하는 메소드나 속성을 찾을 때 해당 객체의 프로토타입을 따라가며 찾을 수 있는 구조
> 
- Javascript에서는 모든 객체가 상속으로 이루어져 있으며, 부모 객체의 prototype을 상속받는다.
이때, 자식 객체에서 원하는 메소드를 찾지 못하면 상위 객체의 prototype을 접근하여 메소드를 찾고, 계속해서 원하는 메소드를 찾아낼 때 까지 거슬러 올라가는 것을 프로토타입 체인이라고 한다.
- 프로토타입을 거슬러 올라갈 때 사용하는 것이 __proto__이다.

## .prototype

> class의 prototype 객체에는 상속 클래스의 prototype 객체가 새로운 객체로(new Object) 생성되어 들어가는데, 이 prototype 객체에 접근할 수 있는 프로퍼티이다.
> 

```jsx
class A {
	constructor() {

	}
}

class B extends A {}

const C = new B();

console.dir(C.constructor.prototype); // B.prototype
console.dir(C.prototype); // undefined
console.dir(B.constructor.prototype) // function.prototype
console.dir(B.prototype); // A.prototype
```

- .prototype 프로퍼티는 class에서만 가지고 있는 객체이다.
인스턴스인 C는 .prototype 프로퍼티와 prototype 객체가 존재하지 않는다.
- 인스턴스.constructor는 인스턴스를 생성한 클래스 자체를 의미한다.
인스턴스.constructor.prototype은 클래스.prototype을 의미한다.
- 클래스.constructor는 클래스를 만들어낸 constructor가 담겨져 있다. 지금 코드에서는 A의 constructor가 들어가 있다.

## __proto__

> 현재 상속받고 있는 prototype 객체를 가져온다.
> 

```jsx
class Person {}
class Student extends Person{}
class Man extends Student{}

const A = new Man();

console.dir(A.__proto__); // Man.prototype
console.dir(A.__proto__.__proto__); // Student.prototype
console.dir(A.__proto__.__proto__.__proto__); // Person.prototype
console.dir(A.__proto__.__proto__.__proto__.__proto__); // Object.prototype
console.dir(Man.__proto__); // Student 
console.dir(A.__proto__ === Man.prototype); // true
console.dir(Man.__proto__ === Student); // true
```

- 코드상에서 보면 A에서 __proto__를 했을때, 자신이 가져온 Man의 prototype 객체를 반환하고, 상위 prototype을 계속 거슬러 올라가게 된다.
- 하지만, __proto__는 현재 브라우저 명세서에 포함되지 않는 비표준 기능이기 때문에 Object.getPrototypeOf(), Object.setPrototypeOf() 메소드를 이용하는 것이 좋다.

## Object

> 모든 객체 요소의 최상위에 존재하는 빌트인 클래스이다.
> 
- Array, Function, String 등의 빌트인 클래스들 또한 Object 클래스를 상속받는다.
- Javascript의 모든 객체 요소들은 Object의 메소드를 모두 사용할 수 있다.