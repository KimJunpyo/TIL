# 코드스테이츠 17일차 정리(Valid Check)

생성일: 2023년 3월 8일 오후 4:41
태그: 코드스테이츠 일일 정리

### visibility: hidden VS display: none VS opacity: 0

|  | visibility | display | opacity |
| --- | --- | --- | --- |
| 공간 차지 | O | X | O |
| 후방 요소 접근 | O | X | X |
| transition | O | X | O |

## event

특정 행동을 취했을때, 무언가가 일어났을 때 등의 어떤 사건을 의미

이벤트 핸들러를 통해 발생된 이벤트를 처리할 수 있음

## event handler

발생된 이벤트에 대한 동작을 담고 있는 함수

## event handler를 등록하는 방법

1. HTML 요소 속성으로 등록
2. DOM 요소 프로퍼티에 등록
3. addEventListener 메소드 사용

### HTML 요소 속성으로 등록

```html
<input type="button" value="click" onclick="printedValue(event)">
<script>
	function printedValue(e) {
		console.log(e); // PointerEvent 객체 출력
		console.log(e.target.value); // click 출력
	}
</script>
```

- HTML 태그 안에다가 속성으로 onclick을 추가하여 event handler가 동작되게 설정

### DOM 요소 프로퍼티에 등록

```html
<input id="test" type="button" value="click">
<script>
	let elButton = document.querySelector("#test");
	elButton.onclick = handleClick;
        
	function handleClick(event) {
		console.log(event); // PointerEvent 객체 출력
		console.log(event.target); // 노드 출력
		console.log(event.target.value); // click 출력
	}
</script>
```

- JS 내에서 DOM API를 통해 프로퍼티를 직접 추가하는 방식

### addEventListener 메소드 사용

```html
<input id="test" type="button" value="click">
<script>
	let elButton = document.querySelector("#test");
	elButton.addEventListener("click", function(e) {console.log(e.target.value)}, false);
	// click 출력
</script>
```

- addEventListener(이벤트 타입, 동작될 이벤트 핸들러, useCapture);
- JS 내에서 분리적으로 이벤트 핸들러의 동작을 구현할 수 있는 방법
- 이벤트 핸들러는 중복으로 여러개를 사용 할 수 있음

### 코드 내에서의 event

- 현재 이벤트 핸들러가 동작됐을 때, 관련된 실행 정보를 담고 있는 PointerEvent 객체를 의미

### event.target

- PointerEvent의 target 프로퍼티로, 이벤트 핸들러가 동작이 된 요소 노드를 의미
(DOM 요소 프로퍼티를 기준으로 **input#test**를 의미)

### event.target.value

- 이벤트 핸들러가 동작된 요소 노드의 value 프로퍼티
- input 태그에는 value=”click”의 코드가 있어서 **“click”**이 출력된다.

## 처음 듣거나 어려웠던 부분(암기할 부분)

useCapture