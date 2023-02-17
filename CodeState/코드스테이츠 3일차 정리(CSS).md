# 코드스테이츠 3일차 정리

생성일: 2023년 2월 15일 오전 9:05
태그: 코드스테이츠 일일 정리

# CSS

- **Cascading Style Sheets**
- 웹 페이지 스타일 및 레이아웃을 정의하는 스타일시트 언어

## 인터페이스

- 컴퓨터와 교류하기 위한 연결고리
- 기존에는 CLI를 사용해서 컴퓨터와 소통했으나, 현재는 알아서 컴퓨터와 소통을 할 수 있는 **버튼이나 드래그** 등이 있다.
- 일반 사용자들이 컴퓨터에 무지해도 컴퓨터에게 명령을 내릴수 있게 해 주는 것이 **UI(User Interface)**이다.
- 또한 사용자들이 UI를 경험하는 행위를 **UX(User Experience)**라고 한다.

### 개발자의 기본 소양

1. UI는 직관적이고 **유저친화적**이여야 한다.
2. 좋은 UX를 위해서는 사용자가 UI를 사용할 때 최대한 편안함을 느끼고 직관적인 정보를 얻을 수 있게 해야 한다.
3. 디자인은 디자이너만 하는 것이 아니다.
4. 웹 페이지를 모방해보며 감각을 익히자.

**font family** : **generic family를 작성하여 기본 글꼴을 설정**하지만, 글꼴이 시스템에 존재하지 않을 때 추가로 글꼴을 작성하여 **글꼴의 우선순위**를 작성

**letter-spacing** : 자간(글자 사이의 공간), line-height : 행간(줄 사이의 공간)

### 웹 폰트 기술

- 사용자가 폰트를 설치하지 않았어도 필요에 따라 **웹에서 다운로드 하게 하는 기술**
- link로 작동(웹 폰트는 stylesheet로 작동)

**<link\>** : 다른 파일과 연결하기 위해 사용

- rel : 연결한 파일의 역할이나 특징(CSS는 StyleSheet기 때문에 stylesheet로 작성)
- href : 파일 주소
- 그 외

## 크기를 정의하는 요소들

### 글꼴 사이즈

- 고정적인 크기 **px(어떤 경우에도 크기 고정)**
- **rem** : 상대 단위, 브라우저의 **기본 글자 크기는 1rem, 브라우저 글꼴 크기에 비례**하여 변경
- **em** : 상대 단위, **부모 엘리먼트의 크기에 비례**하여 크기 변경

### 화면 사이즈

- **반응형 웹 기준**
    - 일반적으로 **디바이스 크기가 변경**될 때 **각각의 CSS 를 적용**시켜야 한다.
    - **디바이스 크기를 나누는 기준은 px다**
    (ex. iPhone 12 Pro Max = 414px)
- **화면 너비나 높이에 따른 상대적인 크기**
    - 웹 사이트가 보이는 영역 - Viewport
    - **vw, vh** - Viewport Width, Height로 1vw는 보이는 영역 기준 1/100의 너비를 말한다.

### display Box

![](https://velog.velcdn.com/images/player1552/post/ec263d34-6d65-4cef-9ed6-631a318a1b36/image.png)


**box-shadow :** x, y, radius, color

**margin, padding**

- top, right, bottom, left(**시계 방향**)
- 두개만 입력 시 **top, bottom / left, right**
- margin은 **음수값 입력 가능**

![](https://velog.velcdn.com/images/player1552/post/c30ef261-8538-483f-8af8-a759934a1a3c/image.png)


**box-sizing : box의 전체 크기를 content + 여백으로 설정하는 것**

(기본적으로 html 문서 전체에 사용하는 편)

## css Selector

```css
* { } - **전체 셀렉터**

h1 { }
div { }