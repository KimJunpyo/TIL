# 코드스테이츠 29일차 정리(Props, State)

생성일: 2023년 3월 24일 오후 1:39
태그: 코드스테이츠 일일 정리

# Props

> 외부로부터 전달 받은 값
> 
- 상위 컴포넌트에서 하위 컴포넌트로(TopDown) 특정 값을 전달해주거나, 특정 함수를 전달할 수 있다.
- attribute= “” 의 구조로 사용되며, attribute는 props에서 사용될 이름을 의미한다.
- props로 값을 보낼 때는 문자열, 객체, 배열, 함수 등이 가능하다.

```jsx
const Hello = ({props}) => {
	return <div>{props.text}</div> // aa
}

const Main = () => {
	return <div>
		<Hello text="aa" />
	</div>
}
```

## props.children

> 여는 태그와 닫는 태그 사이에 값을 입력하여 props를 보내는 방법
> 
- <컴포\>asdasd</컴포\> 와 같이 컴포넌트 태그 안에 값을 입력하면 props.children으로 내부 컴포넌트가 사용할 수 있게 된다.

# State

> 내부에서 변화하는 값
> 
- 버튼의 on/off 기능, 장바구니의 물건 count 등 지속적으로 값이 변화하는 상태를 나타낸다.

## useState

> React에서 state를 다루는 hook 중에 하나로, setState라는 특별한 함수를 통해 상태를 제어
> 
- useState는 두 가지의 값을 반환한다.
    1. 초기값
    2. state 설정 함수
- const [a, setA] = useState(”1”); 이라는 구문이 있다면, a에는 “1” setA에는 설정 함수가 들어가 있다.
- setA(”2”) 와 같이 state를 설정하는 함수로써 사용하고, 이 결과는 a = “2” 가 된다.

## useState주의사항

1. state의 값이 바뀌는 경우에는 자동으로 리렌더링이 된다.
2. state에는 setState 구문으로 설정하는 것 이외에는 정상적으로 값의 변화가 일어나지 않는다.

## 처음 듣거나 어려웠던 부분(암기할 부분)

Controlled Component: React가 state를 통제할 수 있는 컴포넌트

[https://reactwithhooks.netlify.app/docs/forms.html](https://reactwithhooks.netlify.app/docs/forms.html)

단일 책임 원칙: “하나의 컴포넌트(함수)는 하나의 일만 한다”는 원칙