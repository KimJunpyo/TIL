# 2주차 new information

생성일: 2023년 2월 20일 오후 8:42
태그: 코드스테이츠 주간 정리

### REPL(Read-Evaluate-Print loop)

- **읽고, 평가하고, 출력을 반복**하는 가장 간단한 개발 환경
- 내가 작성한 코드가 문법에 맞는지 틀린지 간단하게 실행해 볼 수 있음.

**number.toFixed(소수점 위치)** : 소수점 위치만큼 숫자를 반올림, 반내림, 0 추가를 통해 변경하고 문자열로 반환

```jsx
1.2354.toFixed(1) ⇒ 1.2 => 문자열
123.toFixed(5) => 123.00000 => 문자열
```

### slice, substring의 공통점

1. 시작 인덱스 = start, 종료 인덱스 = end로써 사용
2. end 인덱스는 필수가 아님
3. end 인덱스가 없다면 마지막까지 출력
4. start = end의 경우 빈 문자열 반환

### **slice, substring**의 차이점

1. **slice**는 음수 인덱스가 역방향으로 사용됨

```jsx
let str = "gookbab";
str.slice(-2) // ab;
str.slice(3, -3) // k
```

1. **substring**은 음수 인덱스가 0으로 치환됨

```jsx
let str = "gookbab";
str.substring(-3) // gookbab
str.substring(2, -2) // go => 2, 0은 0, 2으로 치환된다.
```

## classList

`classList`는 DOM 요소의 속성으로, 요소의 클래스를 **DOMTokenList** 개체로 반환한다.

이를 사용하여 요소에 CSS 클래스를 추가, 제거 및 전환 할 수 있다.

```jsx
const action = target.classList[0];

if(action === "number") {
}

// number는 클래스 이름이다.
```

`DOMTokenList` : 공백으로 구분된 **토큰 집합**. ⇒ **토큰 : 클래스**

**⭐ innerText, innerHTML**

## package.json 내부 코드 설명

### name

패키지의 `이름`을 나타낸다.

lowercase로 작성되어야 하고, one-word로 작성되어야 하며, 두 단어 이상을 붙일때는 -, _를 붙인다.

### version

[Major].[Minor].[Patch]의 형태를 따른다. 
(ex. “version” : “1.2.0”)

**Major** : 이전 버전과 호환성을 깨는 변경사항

**Minor** : 이전 버전과 호환되는 새로운 기능 추가

**Patch** : 이전 버전과 호환되는 버그 수정

### description

패키지에 대한 설명이다.

npm에서 검색할 때 리스트에 설명이 표시된다.
![](https://velog.velcdn.com/images/player1552/post/bdd77e84-e65b-4b48-95dc-62ee2bbaf085/image.PNG)


### main

패키지를 동작시키기 위한 모듈을 작성하는 곳이다.

기본값으로 index.js가 되어 있으며, require(”패키지 이름”) 을 입력했을 때, main에 작성된 모듈이 반환된다.

![](https://velog.velcdn.com/images/player1552/post/a815e9fa-cc79-46b9-8b7d-c21eac67a02e/image.png)

### author

배포자를 표시한다. ⇒ 다수의 사람을 표시할때는 “contributors” 로 작성한다.

### license

패키지에 대해 어떤 제한 사항과 권한, 저작권이 있는지 명시한다.

### repository

소스 코드가 관리되고 저장되는 저장소 위치를 지정한다.

type으로 지정 방식을 정하고, url로 저장소를 지정한다.

### devDependencies

“이름” : “버전” 으로 구성된 정보 / 특정 버전들에 의존하여 만들었기 때문에 의존성이라는 단어로 불린다.

### dependencies

이 프로젝트가 돌아가기 위해서 반드시 필요한 모듈들을 담고 있는 정보.

### scripts

CLI에서 사용 가능한 명령을 작성한 정보

npm run <script 이름> 으로 실행함.

## 단어 정리(추가로 공부하여 글로써 정리할 내용들은 별표)

**프로그램**: task(작업) 수행을 위한 정적인 코드의 모음

**프로세스**: 프로그램 실행의 결과물

**자연어**: 인간이 쓰는 언어. 컴공에서 프로그래밍 언어와 구분하기 위해 주석을 통해 사람의 언어를 구별.

**표현식**: 값으로 평가될 수 있는 코드(ex. 1995, 1900+95 등)