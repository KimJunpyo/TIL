# 4주차 new information

다중 선택: Method
생성일: 2023년 3월 6일 오후 1:31
태그: 코드스테이츠 주간 정리

## 명시적으로 this를 설정하는 메소드 방법

```jsx
const obj = {
    a: "a"
}

function A (b, c) {
    console.log(this.a, b, c);
}

A("b", "c"); // undefined "b" "c"
A.apply(obj, ["new_b2", "new_c2"]); // "a" "new_b2" "new_c2"
A.call(obj, "new_b", "new_c"); // "a" "new_b" "new_c"

const B = A.bind(obj);
B("bb", "cc"); // "a" "bb" "cc"
```

### apply(this로 지정할 대상, [매개변수…])

- A.apply(obj) : obj 객체를 this에 바인딩하는 방식
- this.a를 호출하게 되면, obj에서 a key를 찾고 그 value를 출력함
- 매개변수가 함께 전달되어야 하는 경우라면, “[]”로 묶어 내용을 전달해야한다.
ex. A.apply(obj, ["new_b2", "new_c2"]);

### call(this로 지정할 대상, 매개변수…)

- A.call(obj) : apply 메소드와 동일하게 obj 객체를 this에 바인딩
- 매개변수를 전달하는 경우에 쉼표로 구분지어 값을 전달한다.
ex. A.call(obj, "new_b", "new_c");
- this를 정하지 않고, 특정 메소드 혹은 함수에 배열을 모두 보내고 싶을때에는 “null”을 이용한다.
ex. A.call(null, 배열이름)

### bind(this로 지정할 대상)

- const B = A.bind(obj) : obj 객체를 바인딩한 상태의 함수를 반환
- 직접 원하는 this를 바인딩할 수 있는 방법이다.

reference) [https://wooooooak.github.io/javascript/2018/12/08/call,apply,bind/](https://wooooooak.github.io/javascript/2018/12/08/call,apply,bind/)

## 즉시 실행 함수 표현식(IIFE)

- 함수가 정의되자마자 즉시 실행되게 하는 표현식

```jsx
(function() {
	console.log("IIFE");
})();

(() => {
	console.log("IIFE");
})();
```

- 함수의 정의식에 괄호를 씌워주면 IIFE가 된다.
- IIFE는 익명 함수를 사용하는 것이 일반적이다.
⇒ IIFE는 정의가 되자마자 단 한번만 실행이 되고, 그 이후로 재사용할 수 없기 때문에 이름을 지어줄    필요가 없다.
- 괄호를 치는것 외에도 !를 붙이거나, +를 붙여서 IIFE로 만들 수 있다.
- 왜 사용하는가?
    - IIFE의 내부 선언 변수는 private 하다.
    ⇒ 애초에 내부 함수에 절대 접근할 수 없기 때문에, 변수 또한 private하게 된다.
    - 코드 모듈화에 용이하다.
    (일반 클로저 함수의 모듈 패턴화 방식과 IIFE 방식의 차이점은 return에서 메소드를 보낼때 내부 변수를 참조하는가, 참조하지 않는가에 대한 차이점인데, 정확하게 모르겠습니다.)

reference) [https://jongminfire.dev/java-script-즉시실행함수-iife](https://jongminfire.dev/java-script-%EC%A6%89%EC%8B%9C%EC%8B%A4%ED%96%89%ED%95%A8%EC%88%98-iife), chatGPT

### TDZ: 일시적 사각지대(효정님이 잘 설명해주셔서 생략)

## DOM 관련 추가 정리

node.append(노드 or 문자열) : 노드나 문자열을 node 끝에 삽입하는 메소드

node.prepend(노드 or 문자열) : 노드나 문자열을 node 맨 앞에 삽입하는 메소드

node.before(노드 or 문자열) : 노드나 문자열을 node 이전에 삽입하는 메소드

node.after(노드 or 문자열) - 노드나 문자열을 node 다음에 삽입하는 메소드

node.replaceWith(노드 or 문자열) - node를 새로운 노드나 문자열로 대체하는 메소드

### setAttribute

```jsx
const elDiv = document.querySelector("div");
elDiv.setAttribute("style", "color: red");
```

- setAttribute(속성, 프로퍼티: 값)을 통해 특정 DOM 요소의 프로퍼티를 변경할 수 있다.

## Array-like Object

- length 프로퍼티를 가지고 있으며, 배열의 형태를 띄고 있으나 배열이 아닌 유사 배열 혹은 유사 배열 객체

```jsx
const Human = {
	0: "kim",
	1: "good",
	length: 5
}

console.log(Human[0]); // kim
Human.push("asd"); // error, function이 아니라는 error 발생
console.log(Object.keys(Human)); // ['0', '1', 'length']
```

- 유사 배열 객체는 배열이 아니기 때문에, 배열의 prototype 메소드를 사용할 수 없다.
- 객체 prototype 메소드들은 사용할 수 있다.
- 배열처럼 사용하고 싶다면, 두 가지 방법이 있다.

```jsx
// 1. Array.from으로 배열화
const Arr = Array.from(Human);
console.log(Arr); // ['kim', 'good']

// 2. slice.call로 배열화
const Arr2 = Array.prototype.slice.call(Human);
console.log(Arr2); // ['kim', 'good']
```

**Array-like Object 종류** : arguments, NodeList, HTMLCollection, String, TypedArray, Map, Set 등이 있다.

### visibility: hidden VS display: none VS opacity: 0

|  | visibility | display | opacity |
| --- | --- | --- | --- |
| 공간 차지 | O | X | O |
| 후방 요소 접근 | O | X | X |
| transition | O | X | O |

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

## event.preventDefault()

- <a>, <submit>, <button> 태그들은 html에서 제공하는 표준 기본 이벤트가 존재
- 표준 기본 이벤트가 동작되지 않도록 제한을 하는 메소드
- **이벤트 버블링이 동작됨**

## .stopPropagation()

- **이벤트 버블링을 제한하는 메소드**