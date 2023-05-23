# 코드스테이츠 69~70일차 정리-2(Hook, Custom Hook, 코드 분할)

생성일: 2023년 5월 20일 오전 11:11
태그: 코드스테이츠 일일 정리

# Hook

> React 16.8에 추가되었으며, 기존 클래스형 컴포넌트에서만 가능했던 상태 값 및 생명 주기 등의 기능을 함수형 컴포넌트에서 사용할 수 있도록 만들어진 메서드
> 
- React에서 미리 만들어놓은 함수형 컴포넌트 전용 메서드들이다.
- 클래스 컴포넌트에서는 사용할 수 없는데, 이는 React에서 클래스 컴포넌트 대신 함수형 컴포넌트로 쉽게 코드를 구현할 수 있도록 방식을 변경하기 위해 추가한 기능이기 때문이다.

## Hook 사용 규칙

1. 함수 컴포넌트의 최상위에서만 호출
    - 반복문, 조건문, 중첩된 함수 내에서 Hook을 사용할 수 없다.
    - 컴포넌트 안에서는 useEffect, useState 등 다양한 Hook들을 여러 번 사용할 수 있고, React는 호출된 Hook들을 순서대로 저장한다.
    - 하지만, 반복적이거나 조건에 맞춰 Hook을 호출하게 된다면 React는 순서대로 Hook을 저장할 수 없고, 예기치 못한 버그를 야기시킬 수 있다.
2. 리액트 함수 내에서만 사용되어야 함
    - 함수형 컴포넌트, 커스텀 Hook이 아닌 JavaScript 함수 안에서 호출되면 안된다.
    - 예를 들어 window 전역 객체의 어떤 요소가 준비되었을 때 useState를 생성하거나 useEffect를 동작시키게 코드를 구현하면, 에러가 발생한다.
    - 이는 React가 Hook 자체를 함수 컴포넌트 내에서 사용할 수 있도록 개발했기 때문이다. JavaScript 함수는 함수 컴포넌트가 아니다.

[useMemo](https://www.notion.so/09-new-information-useMemo-c3c9576960bd429f84292ea2a15638aa)

[useCallback](https://www.notion.so/10-new-information-useCallback-39db5e2743ff4990b52fe4361290468f)

## Custom Hooks

> 개발자가 원하는 방식으로 커스텀한 hook
> 
- 특정 상태 관리나 로직을 재사용할 수 있도록 분리한 hook이다.
- 함수형으로 작성하기 때문에 명료한 이해가 가능하다.
- 커스텀 훅은 아래의 조건을 지켜야 한다.
    1. 커스텀 훅의 이름에는 함수 이름 앞에 use가 앞에 있어야 한다.
    2. 커스텀 훅들은 대부분 Hooks 디렉토리에 파일로 저장한다.
    3. 커스텀 훅은 특정 조건에 따라 반환값이 변하면 안된다.

## 코드 분할(Code Spliting)

- 대부분 React 앱들은 Webpack, Rollup과 같은 툴을 사용해 번들링하여 웹 페이지를 처리한다.
- 과거에는 위의 방식이 상관없을 정도로 최소한의 수준을 요구했으나, 현대에 들어서는 DOM을 다루는 정도가 정교해지고 JavaScript 자체가 무거워지면서 특정 시점에서 코드의 해석 및 실행이 많이 느려졌다.
- 따라서, 필요한 코드만 먼저 불러오고 불필요한 코드는 필요할 때에 부르는 방식이 채택되었는데, 이것이 코드 분할이다.
- 코드 분할은 물리적으로 코드를 나누는 것이다.
- 서드 파티 라이브러리를 예를 들어, 첫 렌더링 당시 상위 컴포넌트에서 모든 라이브러리의 메서드를 호출하여 골라 사용하는 것 보다, 필요한 컴포넌트에서 서드 파티 라이브러리의 특정 메서드만을 호출하여 사용하는 방법이 있다.

## React에서의 코드 분할

- React에서 코드 분할은 Static, Dynamic으로 나뉜다.
- **Static**
    - 파일의 최상위에서 import를 통해 특정 메서드 혹은 컴포넌트, 라이브러리 등을 가져오는 방법이다.
    - 하지만 구문 분석 및 컴파일하는 데이터가 많은 경우에는 동적으로 import를 하는 방법을 사용하게 된다.
- **Dynamic**
    - 코드 중간에 import하여 필요한 메서드를 가져오는 방법이다.
    - then으로 메서드 이후의 데이터 관리를 처리한다.
    - SPA 기반의 React는 당장 사용하지 않는 컴포넌트들도 모두 불러온 뒤에 렌더링 되기 때문에 초기 렌더링 시간을 줄이기 위해서는 이 기능을 고려할 수 있다.
    
    ```jsx
    form.addEventListener("submit", e => {
      e.preventDefault();
    	/* 동적 불러오기는 이런 식으로 코드의 중간에 불러올 수 있게 됩니다. */
      import('library.moduleA')
        .then(module => module.default)
        .then(someFunction())
        .catch(handleError());
    });
    
    const someFunction = () => {
        /* moduleA를 여기서 사용합니다. */
    }
    ```
    
    - React.lazy 메서드로 dynamic import를 구현할 수 있다.

## React.lazy

- dynamic import를 구현해주는 메서드
- React.lazy(callback) 으로 callback 함수 안에서 동적으로 import하는 방법이다.
- Suspense와 함께 사용해야 하며, Suspense 컴포넌트의 하위에서 import된 컴포넌트가 렌더링 되어야 한다.

```jsx
import Component from "./Component"; // static import

const Component = React.lazy(() => import("./Component"));
```

## React.Suspense

- Suspense는 아직 렌더링이 준비되지 않은 컴포넌트가 있을 때 특정 화면을 보여주고 렌더링이 완료되면 준비된 컴포넌트를 보여주는 기능이다.
- Suspense는 fallback prop으로 렌더링 이전에 보여줄 화면을 전달한다.

```jsx
import { Suspense, lazy } from 'react';
import { BrowserRouter as Router, Routes, Route } from 'react-router-dom';

const Home = lazy(() => import('./routes/Home'));
const About = lazy(() => import('./routes/About'));

const App = () => (
  <Router>
    <Suspense fallback={<div>Loading...</div>}>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<About />} />
      </Routes>
    </Suspense>
  </Router>
);
```

- React.lazy로 import하는 컴포넌트들을 반드시 감싸야 한다.

## 처음 듣거나 어려웠던 부분(암기할 부분)