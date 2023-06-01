# 코드스테이츠 75일차 정리(TypeScript enum, interface, 타입 별칭, 타입 추론, Class)

생성일: 2023년 5월 31일 오전 9:13
태그: 코드스테이츠 일일 정리

# Enum

```jsx
enum Heros {
  SpiderMan,
  IronMan = "IronMan",
  Thor, // enum member must have initializer
}

let hero1: Heros = Heros.SpiderMan;
let hero2: string = Heros[0];

console.log(hero1); // 0
console.log(hero2); // "SpiderMan"
```

- 특정 값을 고정하는 독립된 타입이다.
- Enum 타입은 기본적으로 각 요소에 인덱싱이 된다.
- 요소에 “= 숫자” 를 통해 인덱스 값을 지정할 수 있으며, 이렇게 지정된 값에 따라 이후의 요소들의 인덱스 값이 연속적으로 변한다.
(ex. IronMan = 5를 하게 되면 Thor는 6이다.)
- 요소로 접근하면 인덱스가 반환되며, 인덱스로 접근하면 요소의 값이 전달된다.

### enum member must have initializer

Heros enum에서 IronMan에 “IronMan” 문자열을 지정해줬는데, 이 때 “enum member must have initializer” 라는 에러가 발생한다.

이 에러는 enum이 자동적으로 Thor의 값을 지정할 수 없기 때문이다.

일반적인 enum은 0부터 시작하여 1씩 증가하는 값을 지정해주는데, IronMan의 값을 문자열로 지정함으로써 연속적인 숫자값을 가지지 않게 되어 TS가 자동으로 숫자값을 할당할 수 없는 문제가 발생한 것이다.

따라서, TS에서 Enum을 사용할 때에는 **숫자값만을 가지는 숫자형 Enum, 문자열만을 가지는 문자형 Enum**으로 확실하게 구분지어 사용해야 한다.

### 역 매핑 (Reverse mappings)

- 숫자형 Enum에서만 존재하는 특징으로, key로 value를, value로 key를 얻을 수 있다.
- Enum에서 설명한것처럼 인덱스(key)로 접근하여 값(value)을 가져올 수 있으며, 반대로도 가져올 수 있다.

```jsx
enum Enum {
  A,
}

let a = Enum.A; // key를 이용하여 value 획득
let nameOfA = Enum[a]; // value를 이용하여 key 획득

console.log(a, nameOfA); // 0, "A"
```

# Interface

> 객체의 구조를 정의하기 위해 주로 사용되는 예약어
> 
- 일반적으로 타입 체크를 위해 사용하며 변수, 함수, 클래스에 사용할 수 있다.
- Interface에 선언된 메서드 또는 프로퍼티의 구현을 강제하여 일관성을 유지하기 위해 사용한다.
- 클래스와 형태가 유사하여 헷갈릴 수 있으나 직접 인스턴스를 생성할 수 없고, 모든 메서드는 추상 메서드로 구현되어 있다.

## 변수와 Interface

```jsx
interface User {
  name: string;
  age: number;
}

const kim: User = {
  name: 'Kim',
  age: 26,
};

const park: User = {
  age: 24,
  name: 'Park',
};

const lee: User = { // 프로퍼티가 적어서 Error
  name: 'Lee',
};

const choi: User = { // 프로퍼티가 많아서 Error
  name: 'Choi',
  age: 30,
  height: 175,
};
```

- Interface의 네이밍 컨벤션 관례는 첫 문자를 대문자로 표기하는 것이다.
- 어떤 Interface를 사용하여 변수를 선언할 때는 반드시 정의된 프로퍼티나 메서드들을 전부 작성해야 한다.
- 프로퍼티가 많아도 TS는 에러를 발생시킨다.
- 하지만, 특별한 경우에 특정 프로퍼티가 필요하지 않다면 ? 연산자를 이용해 선택적으로 프로퍼티를 작성할 수 있다.

```jsx
interface User {
  name: string;
  age?: number;
}

const lee: User = { // 에러가 발생하지 않음
  name: 'Lee',
};
```

## 함수와 Interface

```jsx
interface User {
  name: string;
  age: number;
  job: string;
}

interface Greeting {
  (user: User, greeting: string): string;
}

const kim: User = {
  name: 'Kim',
  age: 26,
  job: 'developer',
};

const greet: Greeting = (user, greeting) => {
  return `${greeting}, ${user.name}! Your job : ${user.job}.`;
};

const message = greet(kim, 'Hi');

console.log(message); // Hi, Kim! Your job : developer.
```

- 함수의 Interface를 구현하는 방법은 함수의 인수들과 반환값의 타입을 명시해주는 것이다.
- 이렇게 미리 타입 지정을 해줌으로써 greet 함수의 인수와 반환값에 관한 타입을 지정해줄 필요가 없어지므로 코드의 반복되는 부분들을 제거할 수 있다.

## 클래스와 Interface

```jsx
interface Calculator {
  add(x: number, y: number): number;
  substract(x: number, y: number): number;
}

class SimpleCalculator implements Calculator {
  add(x: number, y: number): number {
    return x + y;
  }

  substract(x: number, y: number): number {
    return x - y;
  }
}

const calculator = new SimpleCalculator();

console.log(calculator.add(1, 2));
console.log(calculator.substract(4, 2));
```

- 클래스에 Interface를 지정하고 싶을때는 implements를 이용하여 작성해준다.
- 함수와 마찬가지로 인수, 반환값에 따라 타입을 명시해줘야 한다.
- 추가적으로 함수와 다른 점은 클래스 내에서도 타입 명시를 한번 더 해줘야 하는데, 이는 Interface와 클래스의 타입이 서로 같음을 표시해줘야 하기 때문이다.

### Interface와 상속

- JS에서 Class를 상속할 때 사용하는 extends 키워드를 Interface에서도 사용할 수 있다.
- 상속을 하면 기존에 존재하는 프로퍼티, 메서드에 상속된 프로퍼티, 메서드까지 모두 가진 새로운 Interface를 만들 수 있다.
- 이 상속 기능 또한 재사용성을 위해 사용되는 덩어리 별로 분할하여 구성하는 것이 좋다.

```tsx
interface FoodStuff {
  name: string;
}

interface FoodAmount {
  amount: number;
}

interface FoodFreshness extends FoodStuff, FoodAmount {
  isFreshed: boolean;
}

const food = {} as FoodFreshness;

food.name = 'egg';
food.amount = 16;
food.isFreshed = true;

console.log(food); // { name: 'egg', amount: 16, isFreshed: true }
```

## TypeScript의 타입 별칭

> type 키워드로 타입의 새로운 이름을 만드는 기능
> 
- number, string 등 interface로만 처리 했던 여러 타입의 묶음들을 type으로 구현하여 코드의 재사용성과 가독성을 더 높일 수 있다.

```tsx
type User = {
  name: string;
  age: number;
};

interface Student {
  grade: number;
  score: number;
  user: User;
}

const mrKim = {
  grade: 1,
  score: 100,
  user: {
    name: 'Kim',
    age: 26,
  },
};

console.log(mrKim);
```

- type 키워드로 생성된 타입은 interface처럼 모든 프로퍼티를 사용해야만 한다.

### 인터페이스 VS 타입 별칭

두 기능은 어떤 데이터의 입, 출력 타입을 명시하는 기능으로 동일하다.

하지만, 두 기능은 차이점이 존재한다.

1. type은 확장성이 부족하다. 그러나 interface는 다른 interface들을 상속받으면서 점점 하나의 큰 interface로 만들 수 있다.
2. vscode 기준으로, type으로 만든 타입에 마우스를 올리면 데이터의 타입들이 모두 보인다. 하지만 interface는 내부 데이터 타입이 보이지 않는다.
3. type은 interface보다 union, intersection 타입을 선언하기가 훨씬 유연하고 간편하다.
4. interface는 type 또한 상속 받아 확장시킬 수 있다.

## 타입 추론

> 변수나 함수의 타입을 선언하지 않아도 TypeScript가 자동으로 유추하는 기능
> 
- TypeScript는 정적 타입 지정을 위해 나타난 언어이지만, 때론 모든 경우에 엄격하게 타입을 지정하는 것이 코드의 개발 시간, 가독성을 저해하는 경우가 발생한다.
- 타입 추론 기능은 여러가지 상황을 고려하여 타입 명시를 굳이 해주지 않아도 되는 경우에는 코드가 더 깔끔해보이도록 도움을 준다.
- 예를 들어 let isNum: number = 5; 라는 코드는 누가 봐도 숫자임을 알 수 있다.
따라서 이 경우, let isNum = 5; 로 구현해도 TS에서 숫자 type임을 유추하게 된다.

### 최적 공통 타입(Best common type)

- 여러 표현식에서 타입 추론이 발생할 때, 해당 표현식의 타입을 통해 “모두가 공통적으로 가질 수 있는 타입을 유추” 한다.

```tsx
let x = [0, 1, null];
```

- 위 코드는 x의 타입이 배열임을 누구나 알 수 있다.
- 그러나 내부의 요소들에 따라 배열의 타입이 달라지는데, 현재 배열의 요소는 모두 number, null로 이루어져 있다.
- 따라서 x 배열의 내부 타입은 number로 유추가 되어 타입이 number[]가 된다.

### 문맥상의 타이핑(Contextual Typing)

- 코드의 위치를 기준으로 타입을 추론한다.

```tsx
function add(a, b) {
	return a + b;
}

window.onmousedown = function (event) {
    console.log(event.button);
};
```

- add 함수는 a와 b, return 값의 타입이 명시되어 있지 않은데, 정상적으로 동작된다.
- 이는 a와 b가 number 타입이라면, return은 당연히 number 타입이라는 유추가 되었기 때문이다.
- 하지만, a와 b가 서로 다른 타입이라면, return은 유추될 수 없다.
- onmousedown 또한 event 값이 어떤 타입인지 추론할 수 없으나, 문맥상 onmousedown 이라는 이름을 가졌기 때문에 event 값 또한 MouseEvent로 추론되었다.

### 타입 추론의 장, 단점

**장점**

1. **코드의 가독성 향상**: 명시적으로 모든 경우에 타입 지정을 해 줄 필요가 없으므로 코드가 간결해지고 가독성이 향상된다.
2. **개발 생산성 향상**: 코드 작성량이 줄어들어 개발 생산성이 향상된다.
3. **오류 발견 용이성:** 변수나 함수의 타입을 추론하여 타입 검사를 수행하기 때문에, 오류를 발견하기 쉬워진다.

**단점**

1. **타입 추론이 잘못될 경우 코드 오류 발생**: TS에서 자동으로 추론을 하기 때문에, 잘못된 추론을 하게 되면 코드 오류가 발생할 수 있다.
2. **명시적인 타입 지정이 필요한 경우가 있음**: 복잡한 함수나 객체의 경우에는 명시적으로 선언해줌으로써 가독성과 이해력을 높일 수도 있다.

# Class

## JavaScript와 TypeScript의 Class 차이점

### JavaScript

```tsx
class Person {
	constructor(name, age) {
		this.name = name;
		this.age = age;
	}
	
	greet() {
		console.log(`저는 ${this.age}살 ${this.name}입니다.`);
	}
}

const person = new Person("kim", 26);
person.greet();
```

- ES6(ECMAScript 2015)에 처음 도입되었다.
- 객체의 프로퍼티와 메서드를 정의하여 객체를 만들어낼 수 있는 거푸집을 만드는 방식이다.
- 거푸집을 통해 새로운 객체를 만들고 싶을때는 new 연산자와 생성자함수 인수값을 전달하여 인스턴스를 만들어내는 과정을 거친다.

### TypeScript

```tsx
class Person {
	name: string;
	age: number;

	constructor(name: string, age: number) {
		this.name = name;
		this.age = age;
	}

	greet(): void {
		console.log(`저는 ${this.age}살 ${this.name}입니다.`);
	}
}

const person = new Person("kim", 26);
person.greet();
```

- TypeScript와 JavaScript의 가장 큰 차이점은 다음과 같다.
    1. JS에서는 this.name과 this.age를 따로 정의하지 않았지만, TS에서는 this.name으로만 선언하게 되면 어떤 타입을 받는 프로퍼티인지 알 수 없기 때문에 최상단에서 선언한다.
    2. cconstructor의 인수값 전달에서 타입을 명시하고 있다.

### TypeScript 클래스와 상속(Inheritance)

- interface와 같이 class 또한 상속의 기능이 있다.
- extends로 상속할 수 있다.

## public, private, readonly를 선언하는 방법

### public

- 외부에 공개되어 내, 외에서 접근할 수 있는 접근 제한자
- 일반적으로는 default값이 public이며, TS에서는 명시적으로 public임을 표시해줄 수 있다.

```tsx
class Person {
	public name: string;
	public age: number;

	constructor(name: string, age: number) {
		this.name = name;
		this.age = age;
	}

	greet(): void {
		console.log(`저는 ${this.age}살 ${this.name}입니다.`);
	}
}
```

### private

- 내부에서만 접근할 수 있는 접근 제한자
- private로 사용하고 싶은 프로퍼티에 private 접근 제한자를 작성하여 사용한다.

```tsx
class Person {
	private name: string;
	private age: number;

	constructor(name: string, age: number) {
		this.name = name;
		this.age = age;
	}

	greet(): void {
		console.log(`저는 ${this.age}살 ${this.name}입니다.`);
	}
}
```

### readonly

- 프로퍼티를 읽기 전용으로 설정하는 키워드
- readonly를 프로퍼티에 작성하여 사용한다.

```tsx
class MyDog {
	readonly dogName: string;

	constructor(dogName: string) {
		this.dogName = dogName;
	}
}

let homeDog = new MyDog("poppy");
homeDog.name = "daniel"; // 에러 발생: 읽기 전용이기 때문에 에러 발생
```

## 처음 듣거나 어려웠던 부분(암기할 부분)

enum 역매핑 컴파일 시점이랑 런타임 시점의 차이점