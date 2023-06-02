# 코드스테이츠 76일차 정리(TypeScript 3(제네릭))

생성일: 2023년 6월 1일 오후 1:23
태그: 코드스테이츠 일일 정리

# TypeScript 제네릭

> 사용될 데이터의 타입을 미리 지정하지 않고, 인자로 전달된 데이터의 타입에 따라 자동으로 타입을 추론하게 하는 기능
> 

### 일반 정적 타입 지정 함수 선언

```tsx
function printData(text: string): string {
	return text;
}

function printData2(text: number): number {
	return text;
}

printData("Yes");
printData2(1);
```

- 일반 정적 타입 지정 함수는 명시된 타입만 받을 수 있고, 그 외의 타입이 들어오면 컴파일 에러를 발생시킨다.
- 따라서 같은 기능이라도 string과 number로 들어오는 경우라면 위의 코드처럼 타입이 다른 동일한 함수를 중복 선언 해야 한다.

### 유니온 타입 지정 함수 선언

```tsx
function printData(text: string | number) {
	return text;
}

printData("Yes");
printData(1);
```

- 일반 정적 타입으로만 지정하는 경우를 유니온 타입으로 묶어서 선언하는 방법이다.
- 하지만, 이런 경우에는 string과 number가 모두 접근할 수 있는 프로퍼티나 메서드만을 참조할 수 있다.
- 대표적으로는 valueOf() 메서드가 있다.

### any 타입 지정 함수 선언

```tsx
function printData(text: any): any {
	return text;
}
```

- 유니온 타입의 문제를 해결하기 위해 모든 타입을 받을 수 있는 any로 선언하는 방법이다.
- 하지만, 이런 경우에는 any 타입으로 인해 함수의 인수가 어떤 타입인지 추론할 수 없고, 반환값 또한 어떤 타입인지 추론할 수 없어서 TypeScript의 장점을 전혀 사용하지 못한다.
- 이 세가지 방법으로 인해 사용되는 방법이 “제네릭” 이다.

## 제네릭

```tsx
function printData<T>(text: T): T {
	return text;
}

const str = printData<string>("hello");
```

- 제네릭은 함수를 호출할 때 타입 변수를 만들어 전달하고, 전달된 타입 변수로 함수 내에서 사용되는 값들에게 타입을 지정해줄 수 있는 기능이다.
- 제네릭을 사용하는 방법은 함수 혹은 배열 등에 <타입>을 지정하여 사용한다.
(ex. const A: Array<number> = [];)
- 또는 단순하게 `printData("hello");` 만으로도 제네릭을 사용할 수 있다.
    - 이는 “hello”가 string이기 때문에 타입 추론 기능으로 T 변수에 string이 할당되기 때문이다.

### 인터페이스에 제네릭 사용하기

```tsx
interface Item<T> {
	name: T;
	stock: number;
}

const item1: Item<number> = {
	name: 12345,
	stock: 2
};

const item2: Item<string> = {
	name: "과자",
	stock: 3
};
```

- interface 내에서도 타입 변수를 통해 어떤 값이 들어오든 재사용할 수 있도록 만들 수 있다.

### 클래스에 제네릭 사용하기

```tsx
class GenericClass<T> {
  private data: T;

  constructor(x: T) {
    this.data = x;
  }

  getData(): T {
    return this.data;
  }
}

let myGenericNumber = new GenericClass<number>(42);
console.log(myGenericNumber.getData()); // 42

let myGenericString = new GenericClass<string>('hello');
console.log(myGenericString.getData()); // "hello"
```

- class 또한 제네릭을 선언할 수 있으며, 다음과 같이 어떤 데이터가 들어오든 상관없이 재사용이 가능한 class를 만들 수 있다.

### 제네릭 타입 변수의 변형

- 만약, 제네릭 타입으로 선언한 값이 number인데, 전달받은 값 혹은 반환할 값이 배열인 경우에는 제네릭 타입 변수에 약간의 변형을 줘야 한다.

```tsx
function lengthPrint<T>(data: T[]): void {
  console.log(...data);
}

lengthPrint([1, 2, 3]); // 1, 2, 3
lengthPrint(['a', 'b', 'c']); // "a", "b", "c"
```

- 위의 코드는 각각 숫자형 배열, 문자열 배열을 전달하여 spread 문법으로 풀어 출력하는 코드이다.
- 이 경우 T는 전달받은 배열의 요소 타입들을 추론하여 정해진다.
즉, 1번 함수 호출은 T가 number이고 2번 함수 호출은 string이다.
- 만약 배열이 [’a’, 1, ‘b’] 로 전달된다면, T의 타입은 number | string이 된다.

### 제네릭 제약 조건

- 제네릭을 사용할 때, 특정 타입에 대한 조건을 설정할 수 있다.

```tsx
interface WithLength {
  length: number;
}

function showLength<T extends WithLength>(data: T): void {
  console.log(data.length);
}

const arrayWithValue: number[] = [1, 2, 3];
const stringWithValue = 'Hello';

showLength(arrayWithValue);
showLength(stringWithValue);
```

- showLength는 전달받은 값이 length 프로퍼티를 가진 경우에만 처리하도록 선언한 함수이다.
- 제약 조건을 설정할때는 상속에서 사용하는 extends 키워드를 사용한다.
- interface로 반드시 전달받아야 하는 데이터를 정의하고 제네릭 변수에 적용하는 방식이다.
- 또는 string만을 받게 할 수도 있다.
(ex. T extends string)

### keyof

```tsx
interface Item {
  id: number;
  name: string;
}

function showItem<T extends keyof Item>(data: T) {
  console.log(data);
}

showItem('name'); // "name"
showItem('asd'); // 에러 발생
```

- keyof로 제네릭 제약 조건을 거는 방법이다.
- keyof 이후에 첫번째로 받는 객체에 없는 key값이 들어오게 되면 접근할 수 없도록 설정하는 방법이다.

### TS 빌드 순서

**TypeScript 컴파일러 → Babel 트랜스파일러 → 실행**