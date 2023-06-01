# 코드스테이츠 74일차 정리(TypeScript)

생성일: 2023년 5월 30일 오전 8:23
태그: 코드스테이츠 일일 정리

# TypeScript

> MS에서 개발한 JavaScript의 상위 집합(Superset) 언어
> 
- JavaScript에 정적타입 검사, 클래스 기반 OOP 등의 기능을 추가하여 개발한 언어이다.
- JavaScript가 발전하면서 생긴 여러 단점을 보완하기 위해 등장했다.

## TypeScript의 등장 배경

- JavaScript는 다른 언어들과 다르게 자료형의 타입을 정적으로 선언하지 않는 언어이다.
- 이런 동적 타입 지정 방식은 장점도 있지만 치명적인 단점이 있다.
- 두 개의 인수를 받아 덧셈을 하는 코드가 있을 때, 만약 인수1에 숫자 / 인수2에 문자열을 넣게 된다면 JavaScript는 인수1의 숫자값을 문자열로 암묵적 형변환하여 의도치 않은 문자열의 값을 반환하게 된다.
- 타입의 동적 변환을 제어하기 위해 TypeScript가 등장하게 되었다.

```jsx
const sum = (n1, n2) => {
	return n1 + n2;
}

console.log(sum(1, "2")); // 기대했던 값 = 3, 결과값 = "12"
```

## TypeScript의 장점

- TypeScript는 정적 타입 검사 기능을 제공한다.
    - 정적 타입 검사 기능으로 인해 코드의 가독성, 유지 보수성을 높일 수 있다.
    - 런타임 에러를 최소화(타입의 문제 해결), 협업시 코드의 이해에 도움을 준다.
- ES6 문법을 포함한 최신 JS 문법을 지원한다.
- Interface, Generic, Decorators 등의 OOP 기능을 제공한다.

```jsx
interface User {
  id: number;
  name: string;
}

function greetingUser(user: User) {
  console.log(`Hello, ${user.name}!`);
}

const parkUser = {
  id: 1,
  name: '박해커',
};

greetingUser(parkUser);
```

# TypeScript의 데이터 타입별 지정 방법

## Boolean

```jsx
let isShow: boolean = true;
let isDone: boolean = false;
```

## Number

```jsx
let number1: number = 5;
let number2: number = 0.7;
let bigint1: bigint = 100n;
let bigint2 = BigInt(100);
```

## String

```jsx
let myName: string = '김준표';
let live: string = '수원';
let introduce = `안녕하세요.
${myName}입니다.`;
```

## Array

```jsx
//첫 번째 방법
let userList: string[] = ["김", "박", "최"];

//두 번째 방법
let numberList: Array<number> = [10, 100, 1000];
```

- 배열은 두 가지 방법으로 표현이 가능하다.
- 타입의 뒤에 []를 입력하여 배열임을 나타내도록 하거나, 제네릭 배열 타입을 이용해 <\>안에 타입을 표현하는 방법이다.

## Tuple

```jsx
let user: [string, number, boolean] = ['김준표', 15, true];

console.log(user[2]); // true
```

- 튜플은 여러 데이터나 객체들을 배열처럼 담는 자료구조이다.
- 튜플은 추가, 삭제, 수정이 되지 않는다.
고정된 값이 필요한 경우에 사용할 수 있다.
- 모든 요소에 각각 자료형을 선언해줘야 한다.

## Object

```jsx
let user: { name: string; age: number } = {
  name: '김준표',
  age: 18,
};
```

- TS에서 Object 타입은 모든 타입을 프로퍼티로 수용한다.
- 프로퍼티 타입들이 any 타입으로 지정된다.
- 하지만, TS의 장점인 정적 타입 명시를 해주는 것이 더 좋다.
프로퍼티 하나하나에 타입을 지정해줄 수 있다.

## Any

```jsx
let maybe: any = 4;
console.log(maybe); // 4

maybe = false;
console.log(maybe); // false
```

- 타입을 알지 못하는 경우에 사용하는 타입이다.
- Any 타입은 타입 검사가 이뤄지지 않는다.
- 또한, 엄격한 타입 검사를 진행하지 않기 때문에, 할당된 값이 가지지 않은 메서드나 프로퍼티를 접근해도 에러가 발생하지 않으며 undefined가 반환된다.
- Any 타입의 경우, 어떤 타입의 값이든 재할당할 수 있다.

# TypeScript의 함수

- TS에서 함수를 선언할 때는 JS와 마찬가지로 function 함수, arrow 함수로 구현할 수 있다.
- 각 매개변수에 타입을 지정해줘야 하고, 반환값에 대한 타입도 지정해줘야 한다.
- 반환값에 대한 타입 지정은 매개변수의 바로 다음에 작성한다.
- 만약 함수가 return이 없는 경우에는 void를 지정해주는 것이 필수다.
- 또한, 매개변수의 개수와 함수의 전달인자의 개수가 다르면 에러가 발생한다.
    - 이를 해결하기 위해, JS의 default parameter처럼 기본적으로 할당될 값을 지정해줄 수 있다.

```jsx
function sum(a: number, b: number): number {
	return a + b;
}

const subtraction = (a: number, b: number): number => {
	return a - b;
}

const divide = (a: number, b = 1):number => {
	return a / b;
} // 인수를 1개만 보내면 1로 나눠서 반환
```

# TypeScript의 연산자 활용 타입

> OR, AND 연산자를 이용하여 만드는 타입
> 

## 유니온(Union Type)

> 둘 이상의 타입을 |(OR) 연산자로 합쳐서 만들어진 새로운 타입
> 
- |(OR) 연산자를 이용하여 A or B라는 의미의 타입을 만든다.
- number | string 으로 지정하면 숫자 또는 문자열의 타입이라는 의미이다.

```jsx
const whatType = (value: number | string): void => {
  if (typeof value === 'number') {
    console.log('number');
  } else {
    console.log('string');
  }
};
whatType(1); // "number"
```

### 유니온 타입을 쓰는 이유

1. 값의 타입이 any로 선언되면 어떤 타입으로 들어올지 추론할 수 없다.
특정 타입들 중에 하나가 들어온다는 것을 명시해주면 코드를 추론할 수 있고 가독성이 향상된다.
2. any로 선언되면 그 값이 어떤 타입인지 TS가 추론할 수 없기 때문에 메서드나 프로퍼티를 자동완성으로 추천해주지 못한다.

### 사용 시 주의사항

1. 유니온 타입의 모든 타입에 공통인 멤버들에만 접근할 수 있다.
    
    ```jsx
    interface Developer {
      name: string;
      skill: string;
    }
    
    interface Person {
      name: string;
      age: number;
    }
    
    const askSomeone = (someone: Developer | Person): void => {
      console.log(someone.name); // "kim"
    	console.log(someone.age); // 에러 발생
    };
    
    const askUser = {
      name: 'kim',
      age: 26,
    };
    
    askSomeone(askUser);
    ```
    
    - 만약 interface로 유니온 타입을 사용했다면, 두 인터페이스에서 공통으로 나타나는 name만 사용할 수 있게 된다.
    - 왜냐하면, 공통되고 보장된 프로퍼티만을 제공해야하기 때문이다.
    - 이를 해결하기 위해서는 “타입 가드” 를 사용해야 한다.
2. 타입 가드
    - TypeScript에서 타입을 보호하기 위해 사용되는 기능 중 하나이다.
    - 특정 코드 블록에서 타입의 범위를 제한하여 블록 안에서의 타입 안정성을 보장한다.
    
    ```jsx
    const askSomeone = (someone: Developer | Person): void => {
    	if("skill" in someone) {
    		console.log(someone.skill);
    	}
    
    	if("age" in someone) {
    		console.log(someone.age);
    	}
    
      console.log(someone.name);
    };
    ```
    

## 인터섹션(Intersection Type)

> 둘 이상의 타입을 &(AND) 연산자로 합쳐서 만들어진 새로운 타입
> 
- &(AND) 연산자를 이용하여 A and B라는 의미의 타입을 만든다.
- number & string 으로 지정하면 숫자 또는 문자열의 타입이라는 의미이다.
- 유니온과는 다르게, 인터섹션은 정해진 매개변수를 정확히 맞춰서 전달해야하며, 그렇지 않으면 에러가 발생한다.
- 또한, 결합된 두 타입의 모든 타입을 지정해야 한다.

```jsx
const askUser = {
  name: 'kim',
  age: 26,
};

const askUser2 = {
  name: 'kim',
  age: 26,
	skill: "good",
};

const askSomeone2 = (someone: Developer & Person): void => {
  console.log(someone.name);
  console.log(someone.age);
  console.log(someone.skill);
};

askSomeone2(askUser); // 에러 발생
askSomeone2(askUser2); // "kim" 26 "good"
```

- 인터섹션 타입은 선택지가 주어지지 않고, 모든 경우의 수를 맞춰야 하기 때문에 상대적으로 선택지가 넓은 유니온 타입이 더 선호된다.

## 처음 듣거나 어려웠던 부분(암기할 부분)

### -g로 설치하면 window에서 되는데 왜 -d로 하면 안되는지 검색 = 오류였음

- -g로 설치하면 디렉토리에 전역적으로 패키지를 설치하여 사용하도록 하는것이다.
- -d로 설치하면 devDependencies 패키지에 설치하며 로컬 dependencies에만 등록하기 때문에 개발 환경에서만 사용하도록 하는것이다.

### mac은 잘 모르겠으나 window의 경우 tsc가 동작이 되지 않는 오류가 있다.

![](https://velog.velcdn.com/images/player1552/post/9ff758f1-1247-46df-9fcc-492888517bcc/image.png)

1. Powershell을 관리자 권한으로 실행 후, Get-ExecutionPolicy로 현재 정책 확인
2. 만약 RemoteSigned로 되어있지 않다면, Set-ExecutionPolicy RemoteSigned 입력 후 A 입력
3. 다시 vscode로 돌아가서 tsc 실행

### type number trivially inferred from a number literal remove type annotation 오류

- TS의 타입 추론 기능으로 발생한 오류
- 타입 추론이란 컴파일러가 스스로 판단해서 타입을 넣어주는 것을 말한다.
- let num = 12, function sum(n1: number, n2: number) { return n1 + n2 }; 처럼 컴파일러가 문맥상 타입을 추론하여 “타입을 추론했으니 작성되어 있는 타입 형식을 제거해주세요.” 라는 오류가 발생한 것이다.

### sourceMap

- TypeScript와 컴파일되어 변환된 JavaScript간의 연결 정보를 제공하여 컴파일된 js 파일에서 에러 발생 시 TS 코드의 어떤 위치에서 오류가 발생했음을 알려주게 된다.
- 브라우저에서 디버깅을 진행할 때 sourceMap을 이용하여 TS를 디버깅할 수 있다.

### tsc --project tsconfig.json

- tsc로 ts를 컴파일할 때 tsconfig.json의 설정을 적용하여 컴파일을 하도록 지시하는 명령어이다.
- 그냥 tsc로 선언한 것과의 차이점은 tsc는 만약 tsconfig.json이 없다면 기본 컴파일러 옵션으로 컴파일을 진행하고, 존재한다면 tsconfig.json을 자동으로 찾아 사용한다.
- tsc —project tsconfig.json은 명확히 tsconfog.json 파일을 지정하여 사용하도록 한다.
