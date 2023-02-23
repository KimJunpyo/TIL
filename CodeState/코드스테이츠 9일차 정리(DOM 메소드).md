# 코드스테이츠 9일차 정리

생성일: 2023년 2월 23일 오후 4:31
태그: 코드스테이츠 일일 정리

# 계산기에서 사용된 JS 구문 정리

## 1️⃣ addEventListener

JavaScript에서 요소에 함수를 연결할 수 있게 해주는 **메소드**.

특정 이벤트가 해당 요소에서 발생하면 함수가 실행된다.

```jsx
element.addEventListener(event, function, useCapture);
```

- `event`: 함수가 실행되기 전에 발생해야 하는 이벤트 (예: "클릭", "마우스오버" 등).
- `function`: 이벤트가 발생했을 때 실행할 코드(함수 사용 가능).
- `**useCapture`: 선택적으로 사용할 수 있습니다. 캡처링 또는 버블링 단계에서 이벤트를 실행할지 여부를 결정하는 "true" 또는 "false" 값.**

### `addEventListener`를 사용하는 방법의 예시

```jsx
const button = document.querySelector('button');

button.addEventListener('click', (event) => {
  console.log('버튼이 클릭되었습니다!');
});

// 첫 번째 button 요소를 선택하고 "click" 이벤트 리스너를 추가한다.
// 버튼이 클릭되면, 두 번째 인수로 전달된 코드가 실행되어 콘솔에 "버튼이 클릭되었습니다!"를 기록한다.
```

---

## 2️⃣ querySelector

CSS 선택자를 기반으로 DOM에서 요소를 선택하여 선택자와 일치하는 첫 번째 요소를 반환하는 **메소드**.

DOM에서 요소에 접근하여 속성, 내용 등을 이용하거나 변경하는 경우에 사용한다.

```jsx
const element = document.querySelector('.example-class');

// DOM에서 클래스 이름이 "example-class"인 첫 번째 요소를 선택하고 element 변수에 할당한다.
```

태그 이름, ID, 속성 값 등을 기반으로 요소를 선택하기 위해 **다른 CSS 선택자**도 사용할 수 있다. 

```jsx
// DOM에서 첫 번째 <p> 요소 선택
const paragraph = document.querySelector('p');

// 특정 ID를 가진 요소 선택
const elementById = document.querySelector('#example-id');

// 부모 요소의 첫 번째 하위 요소 선택
const firstChild = document.querySelector('.parent-element > :first-child');
```

`querySelectorAll`은 `querySelector`와 유사하지만, 지정된 선택자와 일치하는 **모든 요소를 포함하는 NodeList를 반환한다.**

---

## 3️⃣ matches

요소가 지정된 CSS 선택자와 일치하는지 확인하는 **메소드**.

할당된 요소가 선택자와 일치하면 true를 반환하고 그렇지 않으면 false를 반환합니다.

### `matches()`를 사용하는 방법의 예시

```jsx
const element = document.querySelector('p');
if (element.matches('.example-class')) {
  console.log('The element has the class "example-class"');
}

// element 변수에 p 요소를 할당하고,
// .example-class와 element 변수의 요소가 같은지 확인 ( 결과값 false )
```

---

## 4️⃣ classList

`classList`는 DOM 요소의 속성으로, 요소의 클래스를 **DOMTokenList** 개체로 반환한다.

이를 사용하여 요소에 CSS 클래스를 추가, 제거 및 전환 할 수 있다.

```jsx
const action = target.classList[0];

if(action === "number") {
}

// number는 클래스 이름이다.
```

`DOMTokenList` : 공백으로 구분된 **토큰 집합**. ⇒ **토큰 : 클래스**

`DOMTokenList` 는 인덱스(0부터)로 접근할 수 있다.

**length Property** : `DOMTokenList`에 있는 토큰 수를 반환.

---

## 5️⃣ textContent

해당 Node 및 요소가 가지고 있는 값을 텍스트로 조회하거나 수정하는 프로퍼티.

## 처음 듣거나 어려웠던 부분(암기할 부분)

`DOMTokenList` : 공백으로 구분된 **토큰 집합**. ⇒ **토큰 : 클래스**

**⭐ innerText, innerHTML**