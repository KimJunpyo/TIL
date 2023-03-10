# 코드스테이츠 2일차 정리

생성일: 2023년 2월 14일 오전 8:59
태그: 코드스테이츠 일일 정리

# 웹 개발의 한 줄 요약 : 웹은 건물을 짓는 것과 같다.

### 디자이너가 와이어프레임을 만들어준다 → HTML로 구조 작성 / CSS로 스타일 작성

### 기획자가 기능을 만들어준다 → JavaScript로 기능 작성

### HTML : Hyper Text Markup Language - 웹 페이지 틀을 만들기 위해 개발된 마크업 언어

- **마크업 언어** : 태그 등을 이용하여 문서나 데이터의 구조를 명시하는 언어
- 일반적으로는 데이터를 기술하는 정도의 언어이기에 프로그래밍 언어와 구별됨
- HTML은 tag로 구성된 언어이고 Tree Structure를 가지고 있다.
    - Tree Structure : 트리 구조

### 자주 사용하는 tag

<div\>, <span\>, <img\>, <a\>, <ul\>, <li\>, <input\>, <textarea\>

### <div\> vs <span\>

<div\> : 1줄씩 공간을 차지, 기본적으로 display: block 처리가 되어 있음

<span\> : 컨텐츠 크기만큼 공간을 차지, 기본적으로 어떤 css도 처리되어 있지 않음

### <img src=”이미지 주소”/>

src는 key, 이미지 주소는 value로써 key, value의 형태로 이미지파일의 주소를 속성에 담아 표현함

### <a\>

**href** : 하이퍼링크 = 주소 입력

**rel** : href가 있어야만 사용 가능, url에 대한 설명 혹은 특정 기능을 막는 용도(ex. noopener - 새 탭 열기 금지)

**target** : _blank - 새 탭에 표시

**<ul\>** : Unordered List - 순서가 없는 리스트

**<ol\>** : Ordered List - 숫자로 순서를 표시하는 리스트

**<li\>** : List - ul과 ol 안에서의 목록 값

**value** : 문자열로 숫자를 입력할 시, 그 숫자부터 목록 작성 

```html
<li value = "3">
```
![Untitled](https://user-images.githubusercontent.com/100808381/218663685-28d08546-f2bc-4ce6-858c-ce443f98142f.png)



### <input\> : 입력 폼

**type** : button, checkbox, color(색상 선택기), date(날짜 선택 달력), radio, range(막대 컨트롤 바), file(파일 선택기) 등등 다양함

**👍radio의 name을 동일하게 한 뒤, <div\>로 묶으면 그룹처리(한 개 씩만 체크됨)**

//지금 작업중인 프로젝트에도 적용될 수 있을 듯

**autofocus** : 화면이 렌더링 될 때 자동으로 커서가 표시

**autocomplete** : 기존에 입력한 값에 기반하여 브라우저가 자동으로 입력값을 추천

**readonly** : 사용자가 입력할 수 없고, 보기만 가능

**disabled** : 입력도, 클릭도 할 수 없음

**required** : 사용자가 필수로 입력해야 하는 것임을 나타내는 것

**max(min)length**: 최대(최소) 문자 갯수

**placeholder** : 입력 폼에 미리 입력되어 있는 값, 입력 시 사라짐

**min, max, step** : **type=number**일 때 사용 가능하고 최소, 최대, 수의 단위를 정할 수 있음

### <textarea\> : 여러 줄의 값을 입력할 때 사용하는 텍스트 입력 영역

autofocus, readonly, disabled, required, maxlength, placeholder는 동일

wrap : 입력값을 보낼 때 줄바꿈을 함께 보내는 것(데이터의 가시성 확보)

### **시맨틱 요소 : HTML5에서 <div\> 지옥을 해결하기 위해 나온 “의미를 가진 요소”이다.**

(ex. <article\> : 독립적인 콘텐츠, <aside\> : 사이드 바 와 같은 본문의 주요 내용을 제외한 남은 부분)

- 시맨틱 요소는 그 양이 무려 **약 100개**에 달할 정도로 상당히 많다.
- 모든 것을 외울 수 없기 때문에 **필요할 때 마다 한번씩 찾아보며** 천천히 내가 필요한 부분들만 **기억에 남게** 사용하는 것이 바람직하다.

### id와 class의 차이점

id : 고유한 이름을 붙일때

class: 반복되는 영역을 유형별로 분류할때 (ex. 댓글창 한 칸)

---

## 처음 듣거나 어려웠던 부분

form, section, select, option, optgroup, fieldset, label

Selector - css에서의 id, class 표현 방식(ex. id = #id, class = .class)

렌더링이란?

attribute name, attribute value

<script\>
alt
