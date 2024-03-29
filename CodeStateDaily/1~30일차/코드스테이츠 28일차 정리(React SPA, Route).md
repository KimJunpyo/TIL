# 코드스테이츠 28일차 정리(React SPA, Route)

생성일: 2023년 3월 23일 오전 9:38
태그: 코드스테이츠 일일 정리

# SPA(Single Page Application)

> 서버로부터 완전한 새로운 페이지를 불러오지 않고 **페이지 갱신에 필요한 데이터만 받아 현재의 페이지를 업데이트** 함으로써 사용자와 소통하는 웹 어플리케이션이나 웹 사이트
> 

## SPA의 장점

- 필요한 부분의 데이터만 업데이트 하면 되기 때문에 **상호작용의 반응이 빠르다.**
- 서버에서는 **요청받은 데이터만 전송**해주면 되기 때문에 **서버 과부하 문제가 상당히 줄어든다.**
- 상호작용 때마다 전체 페이지를 렌더링 하지 않기 때문에 **더 좋은 UX를 제공**한다.

## SPA의 단점

- SPA는 HTML에 데이터가 거의 존재하지 않고, **JavaScript에 대부분의 코드가 모여**있다보니 **첫 로딩시에 많은 시간을 소요**하게 된다.
- **검색 엔진 최적화(SEO)가 좋지 않다.** 웹 페이지의 URL, HTML 내의 각종 태그나 링크 등을 분석하여 검색 기능을 동작시키는데, SPA는 HTML에 데이터를 담지 않기 때문이다.
    - 하지만, 검색 엔진의 발전으로 인해 **이 단점은 점점 사라지는 추세**이다.

## WireFrame

> 웹 페이지의 레이아웃, UI 요소 등에 대한 뼈대를 만드는 방법
> 
- 웹 페이지 디자인을 하기 전에 선을 이용해 구조를 표시하는 방법이다.

## MockUp

> WireFrame의 뼈대에 색상, 사진 등을 추가하여 시각적으로 화면의 디자인을 표현하는 방법
> 
- 이 레이아웃에서 어느 위치에 어떤 데이터가 나타나고 어떤 디자인이 들어갈 것인지를 나타내는 모형이다.

# React Router

> React에서 Routing을 적용하기 위해 사용하는 라이브러리
> 

## 컴포넌트 종류

### <BrowserRouter\>

<aside>
💡 웹 애플리케이션에서 History API를 이용해 페이지를 새로고침하지 않고 주소를 변경할 수 있게 해준다.

</aside>

- BrowserRouter가 상위에 있어야 React Router의 컴포넌트들을 사용할 수 있게 된다.
- 혹은 index.js에 <APP\>을 감싸서 처리할 수도 있다.

### <Routes\>

<aside>
💡 여러개의 Route를 감싸서 그 중 경로가 일치하는 단 하나의 Route만 렌더링을 시켜준다.

</aside>

- 만약 Routes로 감싸지 않는다면, 경로가 일치하는 모든 요소를 렌더링한다.

### <Route\>

<aside>
💡 path에 주소 경로를 지정하고, element에 이동할 컴포넌트를 입력하여 Link 컴포넌트가 호출된 경로와 일치하다면, 작동된다.

</aside>

- ❗만일 지정된 주소가 아닌 다른 경로를 입력해서 접근을 시도하면, path=”*” 으로 공통된 화면이 출력되게 할 수 있다.

### <Link\>

<aside>
💡 경로를 연결하는 역할을 하는 컴포넌트

</aside>

- ReactDOM으로 렌더가 완료되면 Link는 a 요소로 변경된다.
하지만, a 요소의 기본 이벤트인 새로고침 현상은 나타나지 않는다.

## 처음 듣거나 어려웠던 부분(암기할 부분)

Prototyping: WireFrame으로 구조를 짜고, MockUp으로 시각적인 디자인이 만들어졌을 때, 특정 상호작용에 따른 화면간 이동의 흐름을 표기하는 방법

Routing: 주소에 따라 다른 화면을 보여주는 과정

CSR, SSR
