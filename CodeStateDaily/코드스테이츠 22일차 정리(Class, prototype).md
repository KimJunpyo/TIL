# 코드스테이츠 22일차 정리(Class, prototype)

생성일: 2023년 3월 15일 오후 1:41
태그: 코드스테이츠 일일 정리

# 클래스 정의

```jsx
class Person {
	// 생성자
	constructor(name) {
		this.name = name;
	};
	// 프로토타입 메소드
	sayHi() {
		console.log(`Hi, My name is ${this.name}`);
	}
	// 정적 메소드
	static sayHello() {
		console.log("Hello");
	}
}
// 클래스 생성 및 변수에 할당
const me = new Person("lee");

console.log(me.name);
me.sayHi();
Person.sayHello();
```

- 클래스는 일급 객체이다. 즉, 변수에 할당도 가능하고 일반적인 함수처럼 사용될 수 있다.

# 인스턴스 생성

인스턴스 : 클래스의 생성자 함수로 구조와 프로퍼티, 프로토타입 등을 똑같이 가지고 있는 새롭게 만들어진 객체

## new 연산자

- 새로운 인스턴스를 만들 때 사용하는 연산자
- const 변수 = new 클래스이름(); 의 패턴으로 새로운 인스턴스를 생성 할 수 있다.
- new를 사용하지 않는 방식은 모두 에러를 반환한다.

## constructor(생성자)

```jsx
class DeepDive {
	// 생성자
	constructor(name) {
		this.name = name;
		this.age = 0;
	}
}

const Kim = new DeepDive("kim");
```

1. constructor 내부에서 this로 선언한 값들은 새로 만들어진 인스턴스의 프로퍼티에 담긴다.
2. constructor는 클래스 내에 한 개만 존재할 수 있다.
3. constructor는 생략할 수 있다.  암죽걱으로 빈 constructor가 생성되어 빈 객체 인스턴스를 반환한다.
4. 초기 프로퍼티 값을 매개변수로 전달하여 내부에서 동적으로 값을 변환시키거나, 기본 값을 고정 할당을 하는 방식들을 사용할 수 있다.
5. ⚠️클래스에서는 return을 반드시 생략해야 한다.⚠️
return으로 객체를 반환하는 경우, this로 작성된 모든 인스턴스 프로퍼티는 무시된다.
return으로 원시값을 반환하는 경우, return은 무시된다.

## ES5 클래스 작성 문법

```jsx
function Student(name, score, grade) {
	this.name = name;
	this.score = score;
	this.grade = grade;
}

Student.prototype.getScore = function(){
    console.log(`${this.score}점 입니다.`);
}

const A = new Student("kim", 90, "3학년");

A.getScore(); // 90점 입니다.
```

- ES5에서는 생성자 함수의 방식이 function이였고, 그 함수의 prototype에 메소드를 추가함으로써, 마치 클래스를 사용하는 것 처럼 코드를 작성하였다.

## ES6 클래스 작성 문법

```jsx
class Student {
    constructor(name, score, grade) {
        this.name = name;
        this.score = score;
        this.grade = grade;
    }

    getScore () {
        console.log(`${this.score}점 입니다.`);
    }
}

const A = new Student("kim", 90, "3학년");

A.getScore();
```

- class, constructor가 생겨나, 실제로 클래스의 패턴과 동일하게 코드를 작성할 수 있게 되었다.
- ES5의 function Student === class Student의 constructor이며, prototype에 추가하지 않아도 클래스의 몸체에다가 function 키워드 없이 prototype 메소드를 만들 수 있게 되었다.

---

# OOP

- 객체 지향 프로그래밍
- OOP는 모든 것이 “객체로 그룹화”된다.

## 클래스와 인스턴스

1. 클래스는 객체를 생성하기 위한 청사진이다.
2. 클래스의 인스턴스는 청사진으로 찍어낸 생성물이다.
    - 인스턴스는 클래스로 만들어낸 “객체” 이다.
    - 클래스의 생성자로 인스턴스의 세부 속성들(프로퍼티)을 추가하여 객체를 만든다.
3. 클래스에는 인스턴스가 가져야할 “프로퍼티”와 기능을 담당하는 “메소드”가 존재해야 한다.

## OOP 기본 개념 4가지

- 캡슐화
- 추상화
- 상속
- 다형성

### 캡슐화

> 클래스 안에 서로 연관된 프로퍼티 및 기능들을 하나로 묶어 캡슐처럼 관리하고, 데이터를 외부로부터 보호할 수 있도록 하는 개념
> 
- 느슨한 결합(Loose Coupling) : 코드 실행 순서에 따라 절차적인 코드를 작성하는 것이 아니라, 서로 연관된 프로퍼티 및 기능들을 모아서 결합하는 것을 의미
    - 느슨한 결합을 추구하는 코드 작성법 : 코드만 보고도 인스턴스의 사용 방식과 기능을 상상할 수 있도록 작성하는 방법
- 은닉화 : 내부 데이터나 내부 구현이 외부로 노출되지 않도록 하는 것
    - 객체 내의 메소드만 수정할 수 있고, 프로퍼티에 접근할 수 없도록 하는 방식이다.
    - 접근자 프로퍼티(getter, setter)를 이용해서만 접근할 수 있다.

### 추상화

> 구체적인 세부 정보를 감추고 중요한 기능과 속성만을 단순화하여 사용자에게 노출시켜 쉽게 이해하고 사용할 수 있도록 하는 개념
> 
- 클래스에 프로퍼티와 메소드만 존재한다면 “인터페이스” 라고 부른다.
- ⭐ 추상화와 캡슐화는 비슷하지만, 원하는 방향성이 다르다.
    - 캡슐화는 “코드나 데이터의 은닉을 방향성으로 추구하며, 객체의 내부를 보호하는 것”을 목적으로 한다.
    - 추상화는 “클래스나 객체를 단순하게 만들어서 사용성을 편리하게 하기 위함”을 방향성으로 추구한다.

### 상속

> 부모 클래스의 특징을 자식 클래스가 물려받는 개념
> 
- ex) 부모 클래스 = Person, 자식 클래스 = Student
Person 클래스에는 기본적으로 사람을 나타내는 모든 프로퍼티나 기능이 존재하고, Student는 “수업을 듣는다” 라는 기능을 추가하여 사용할 수 있다.

### 다형성

> 자식 클래스들이 모두 동일한 메소드를 사용했을 때, 표현되는 방식을 다르게 구현할 수 있다는 개념
> 
- ex) 부모 클래스의 showName() : 자식 클래스의 property 중에 name을 출력
자식 클래스들에서 showName()을 하게 되면 자식 클래스들이 가지고 있는 각기 다른 name들을 출력할 수 있다.

---

# 프로토타입

객체의 원형을 나타내는 객체

- 모든 객체는 prototype의 내부에 프로퍼티와 메소드를 가지고 있다.
- 특정 객체가 어떤 객체를 상속하게 되면, 서브 클래스의 prototype 객체에 슈퍼 클래스의 prototype 객체 주소값을 넣게 된다.

## __proto__

현재 상속받고 있는 prototype 객체를 가져온다.

```jsx
class Person {}
class Student extends Person{}
class Man extends Student{}

const A = new Man();

console.log(A.__proto__); // Man.prototype
console.log(A.__proto__.__proto__); // Student.prototype
console.log(A.__proto__.__proto__.__proto__); // Person.prototype
console.log(A.__proto__.__proto__.__proto__.__proto__); // Object.prototype
```

- 코드상에서 보면 A에서 __proto__를 했을때, 자신이 가져온 Man의 prototype 객체를 반환하고, 상위 prototype을 계속 거슬러 올라가게 된다.
- 하지만, __proto__는 현재 브라우저 명세서에 포함되지 않는 비표준 기능이기 때문에 Object.getPrototypeOf(), Object.setPrototypeOf() 메소드를 이용하는 것이 좋다.

## 프로토타입과 클래스, 인스턴스의 관계![](https://velog.velcdn.com/images/player1552/post/af439e59-8164-4930-a95a-e39a232b13bb/image.png)


- class의 .prototype을 통해 class.prototype 객체를 호출할 수 있다.
    - class.prototype에는 class의 property들이 존재
- new class();를 통해 class instance를 생성할 수 있다.
- instance에서 .__proto__를 통해 원본 클래스의 prototype 객체에 접근할 수 있다.
- class.prototype에 constructor 생성자 함수를 선언하고, new 키워드로 접근할 수 있으며, 접근시 class의 데이터를 담고 있는 instance를 생성한다.
    - instance에서 class의 메소드나 프로퍼티를 사용하게 되면, class.prototype에 존재하는 property를 가져옴

## 클래스 상속에서 알아둬야할 부분

1. 클래스에서 인스턴스를 생성하면 원본 클래스의 **모든 것을 복사**하여 가져간다.
2. 인스턴스에서 클래스의 메소드를 사용하면, **메소드는 클래스의 prototype 객체 안에서** 찾아온다.
3. 클래스가 다른 클래스를 상속했을 때에는, **클래스 자체를 가져오는 것이 아닌 클래스.prototype 객체**만을 가져오게 된다.

# 클래스와 프로토타입에 대한 최종 요약

1. class를 만들면 내부에는 constructor 함수, prototype 객체가 있다.
2. class에 프로퍼티나 메소드를 만들면 prototype안에 들어간다.
3. class에 정적 메소드들을 만들면 (constructor, prototype, 정적메소드1, 정적메소드2) 와 같은 형태가 된다.
4. class의 constructor에는 prototype 객체를 참조할 수 있는 프로퍼티 / prototype 객체에는 constructor를 참조할 수 있는 프로퍼티가 기본적으로 내장되어 있다.