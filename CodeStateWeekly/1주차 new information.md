# 1주차 new information

생성일: 2023년 2월 14일 오후 4:40
태그: 코드스테이츠 주간 정리

## form: 어떤 정보들을 담아 서버로 제출하기 위한 추상적인 입력 폼

```html
<form action="주소">
	이름 : <input type="text" name="name">
</form>
```

- input, button, option, select 등 입력에 사용되는 여러 태그들을 내부에 사용할 수 있다.
- **attribute**
    - action: 제출될 서버의 URL
    - accept-charset: 서버로 제출될 때의 문자 인코딩 방식
    - name: form의 이름을 정의
    - novalidate: 서버로 제출될 때 유효성 검사를 하지 않게함(기본적으로는 유효성 검사를 함)
    - target: 서버로 제출 후, _blank나 _self와 같은 위치를 명시하여 응답값이 열릴 위치를 정의
    - method: get, post로 서버에게 통신

### fieldset: form 요소들을 그룹으로 묶는 태그

- legend라는 태그를 통해 내부에서 fieldset 설명

---

### section: 시맨틱 태그로 각각의 큰 구역을 정의할 때 사용(div 대신 사용)

```html
<header>헤더<header>
<main>
	<section>
		첫번째 구역
	</section>
	<section>
		두번째 구역
	</section>
<main>
<footer>푸터</footer>
```

---

### select: option을 하나의 단위로써 목록을 생성

- size: 목록에서 기본적으로 보여주는 줄 수
    ![](https://velog.velcdn.com/images/player1552/post/b728967a-6307-444d-9815-c7f6d4ce8f84/image.PNG)
    
    size=”3”
    
- multiple: 메뉴에서 다수의 옵션을 선택할 수 있는 기능(드래그)

### option: select에서 보여줄 각각의 줄

- selected: 초기에 선택되어져 있게 설정

### optgroup: option의 그룹을 정의

- label: 그룹의 텍스트를 지정

---

### label: UI 요소의 설명을 나타내는 태그

- for 속성으로 입력과 관련된 태그들의 id값을 입력하면 서로 연결이 되어 라벨을 눌러도 입력이 인식된다.

**Selector** - css에서의 id, class 표현 방식(ex. id = #id, class = .class)

---

### <script\>

- Javascript 코드를 정의할 때 사용되는 태그
- src = “” 을 통해 Javascript 파일 호출 가능
- **async:** 페이지의 나머지 문서와 동시에 출력(HTML 로드를 진행하면서 JS 파일 다운 명령 시작)
- **defer:** 페이지가 모두 표시 된 후, 마지막에 실행
- 일반적으로는 async, defer 둘 다 문제점이 있기 때문에 </Body\>의 앞에 작성하기를 권장
(HTML이 모두 로드가 된 이후에 다운로드를 시작하기 때문에 상당히 느림)

---

### **background, background-color의 차이**

**background** : 배경에 줄 수 있는 다양한 옵션을 띄어쓰기로 한번에 입력 가능

<aside>
💡 background-color
background-image
background-repeat
background-attachment
background-position

</aside>

**background-color** : 배경의 색상만 변경

**background-size** : 배경의 크기만 변경

**♦️ 이미지를 배경으로 할 때 알아둬야할 background-size 속성**

- contain : 지정된 요소 안에 이미지가 다 들어오도록 이미지를 축소/확대
- cover : 이미지의 기존 해상도에 맞춰 배경이미지를 다 덮도록 축소/확대

---

### ⭐meta

- 해당 페이지에 대한 정보인 메타데이터(metadata)를 정의할 때 사용하는 태그
- base, link, script, style, title과 같이 메타데이터를 정의하는 태그가 존재하지 않는 경우에 사용.
- meta 태그는 언제나 head 내부에 있어야 함
- name : 키워드, 설명, 저자, 뷰포트 등 정의할 데이터를 설정

---

**flex-basis: 각각의 flex-basis 크기를 차지 → flex-grow의 비율 만큼 남은 여백을 가져가서 크기를 키움.**

---

### ⭐transform, transition, translate의 차이점

**transform** : 요소의 크기, 각도, 기울기 등을 변경할 때 사용하는 속성이다.

- transform : scale(5%, -5%) → 가로 크기를 50%, 세로 크기를 -50%로 변경
- transform : translate(5px, 6%) → X 좌표를 5px, Y 좌표를 6%만큼 이동

**transition** : 요소가 변화할 때 변환 시간 및 효과를 주는 속성이다. 변환 효과는 단일 속성에만 줄 수 있다.

- transition : 0.5s → 모든 요소에 0.5s의 변환 시간을 부여
- transition : margin-left 5s → margin-left 속성만 5초동안 변경

**translate** : transform의 속성으로 요소의 좌표를 변경할 때 사용하는 속성이다.

**⭐animation 속성**

- 요소에 적용되는 css 스타일을 keyframe을 통해 상태별로 변경하며 부드럽게 변화시키는 속성

---

## 단어 정리(추가로 공부하여 글로써 정리할 내용들은 별표)

**alt**: img 태그 내에서 사용하는 속성이며, 이미지 대체 설명(사진이 호출되지 못했을 때, 대체로 나올 설명)

**attribute name** : 속성 이름값

**attribute** **value** : 속성 입력값

**⭐렌더링** : 서버로부터 HTML, CSS, Javascript 등의 파일을 받아 브라우저에 그래픽 형태로 출력하는 행위

⭐**[DOM](https://velog.io/@player1552/HTML-DOM)** : Document Object Model의 약자로 HTML 문서에 대한 노드 트리형 인터페이스

**컴포넌트** : 전체 코드에서 특정 기능을 구현하는 코드를 캡슐화 및 분리하여 재사용성이나 커스텀을 할 수 있게 만들어진 코드

⭐**viewport** : 컴퓨터 화면의 영역을 말하며, 웹 브라우저 창의 크기를 말한다.

**doctype** : 브라우저가 문서를 렌더링 할 때 html의 버전이 무엇인지를 알려주는 역할.