# 코드스테이츠 46일차 정리(CCD, useRef)

생성일: 2023년 4월 18일 오후 6:20
태그: 코드스테이츠 일일 정리

# CDD

> Component Driven Development의 약자로 재사용할 수 있는 UI 컴포넌트를 미리 디자인하고 개발하여 사용하는 개발 방법
> 
- 작은 부품 단위로 하나씩 UI 컴포넌트를 개발하여 하나의 페이지를 조립하는 개발 방법이 가능해진다.

## 구조화된 CSS의 필요성

1. 많은 사람들이 CSS 개발 작업을 진행하면 일관된 패턴이 없기 때문에 작업 시간이 훨씬 많이 걸린다.
2. 모바일, 데스크탑, 태블릿 등 다양한 디바이스의 등장으로 CSS에서 처리해야할 디자인의 양이 많이 늘어나서 코드가 복잡해졌다.
3. 구조화를 통해 일관된 코드로 개발을 하면 효율성이 늘어나고 호환성이 높아질 수 있다.

# 1. Styled Components

> CSS를 컴포넌트화 하여 JS 파일에서 컴포넌트처럼 사용할 수 있는 라이브러리
> 
- Styled Components에서는
const 컴포이름 = styled.태그`
     css: asd
`;
로 코드를 작성하여 하나의 CSS 컴포넌트를 만들고 기존에 사용하던 태그 대신 사용한다.
- 이미 생성된 CSS 컴포넌트를 **“const 새로운 컴포 = styled.컴포넌트”** 로 호출하여 CSS를 추가할 수 있다. 즉, 재활용이 가능하다.
- Props를 내려줄 수 있고, CSS속성에서 Props를 사용할 수 있다.
- Props를 전달하는 방법은 아래처럼 두 가지의 방법이 있으며, CSS 내부 코드에서 함수로 삼항 연산자 혹은 OR 연산자로 처리할 수 있다. 그 외에도 여러 방법이 있다.

```jsx
import styled from "styled-components";
import GlobalStyle from "./GlobalStyle";

const Button1 = styled.button`
	background: ${(props) => (props.skyblue ? "skyblue" : "white")};
`;
const Button2 = styled.button`
	background: ${props.color => props.color || "white"};
`;

export default function App() {
	return (
		<>
			<GlobalStyle />
			<Button1 skyblue>Button1</Button1>
			// skyblue를 props로 전달하였다.
			<Button2 color="orange">Button1</Button2> 
			// orange를 color라는 이름으로 props에 전달하였다.
		</>
	)
}
```

- GlobalStyle을 설정할 수 있으며, CSS 파일을 작성하는 것 처럼 코드를 작성하여 전역적으로 스타일을 지정해주는 기능이 있다.
이를 통해서 기초적인 스타일 설정이 가능하다.

```jsx
import { createGlobalStyle } from "styled-components";

const GlobalStyle = createGlobalStyle`
	button {
		padding : 5px;
    margin : 2px;
    border-radius : 5px;
	}
`

function App() {
	return (
		<>
			<GlobalStyle />
			<Button>전역 스타일 적용하기</Button>
		</>
	);
}
```

# Storybook

> CDD를 하기 위한 도구이며 각각의 컴포넌트들을 따로 볼 수 있게 구성해 주어 한번에 하나의 컴포넌트에서 작업할 수 있다.
> 
- 컴포넌트들을 카탈로그화 할 수 있다.
- 컴포넌트의 변화를 Stories로 저장할 수 있다.
- 핫 모듈 재 로딩과 같은 개발 툴 경험을 제공한다.
- 다양한 뷰 레이어 지원을 제공한다.

# useRef

> DOM 노드, 엘리먼트, React 컴포넌트 주소값을 참조할 때 사용하는 React Hook
> 
- useRef로 가져온 주소값은 렌더링이 될 때마다 값이 다시 할당 될 뿐, 값이 변하지는 않는다.
- 하지만, useRef를 남용하면 선언형 프로그래밍 원칙과 대비되기 때문에 조심해서 사용해야 한다.

```jsx
function App() {
	const El = useRef(null);

	useEffect(() => {
		console.log(El.current); // <div></div>
	});

	return (
		<div ref={El}></div>
	);
}

export default App;
```

## 처음 듣거나 어려웠던 부분(암기할 부분)

Storybook의 사용법은 포스팅으로 처리

media playback