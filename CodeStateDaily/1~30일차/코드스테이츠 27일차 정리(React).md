# 코드스테이츠 27일차 정리(React)

생성일: 2023년 3월 22일 오전 10:21
태그: 코드스테이츠 일일 정리

# React

> 프론트엔드 개발을 위한 **JavaScript 오픈소스 라이브러리**
> 

## 왜 React를 써야 하는가?

1. **선언형**
    - JSX를 이용해 **HTML / CSS / JS를 하나의 파일에서 명시적으로 작성**할 수 있다.
2. **컴포넌트 기반**
    - 하나의 기능 구현을 위해 **여러 종류의 코드를 묶어둔 것**
    - ex) 장바구니 물건 단일 리스트를 컴포넌트로 분리
    - 기능 중심 개발이 가능하고, 의존성이 적기 때문에 **유닛 테스트에 용이**하다.
    - 유지보수를 할 일이 있다면, 특정 기능 컴포넌트만 고치면 되기 때문에 **유지보수가 좋다.**
3. **범용성**
    - 라이브러리이기 때문에 **JavaScript 프로젝트 어디에서든 적용**될 수 있다.
    - Facebook 주도하에 개발이 이뤄지고 있어서 안정적이고, 상당히 유명하다.
    - React Native를 이용하여 모바일 개발도 가능하다.

## JSX 규칙

1. 여러 Element를 작성하고 싶을 때는 **최상단에서 Tag로 감싸**주어야 한다.
2. **class 대신 className**을 사용한다.
3. JSX에서 JavaScript를 사용할 때는 중괄호로 표기해야 한다.
ex) <h1>{name}</h1>
4. **컴포넌트는 “대문자”로 시작**해야 한다. ⇒ 사용자 정의 컴포넌트
5. **조건부 렌더링은 “삼항연산자”**를 사용해야 한다.
6. 여러개의 HTML Element를 표시할 때는 반복문이 아닌 **map() 함수로 표현**한다.
각 Element에는 **고유의 key**를 반드시 넣어주어야 한다.

## CRA(Create React App)

> React를 쉽고 빠르게 개발할 수 있도록 만들어진 **툴 체인**
> 
- Babel, PostCss, jest 등을 포함한 다양한 툴들을 한번에 설치하여 개발환경을 쉽게 구현해주는 방법이다.

## 처음 듣거나 어려웠던 부분(암기할 부분)

JSX(JavaScript XML): JavaScript를 확장한 문법이며, Babel을 통해 브라우저에서 JavaScript 코드로 컴파일된다.

reportWebVitals?

Hot reloading

<code>