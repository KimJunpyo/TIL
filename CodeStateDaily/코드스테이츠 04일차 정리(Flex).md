# 코드스테이츠 4일차 정리

생성일: 2023년 2월 16일 오전 9:04
태그: 코드스테이츠 일일 정리

## 와이어프레임

- **레이아웃의 뼈대**를 그리는 단계
- 단순한 **선이나, 도형으로** 웹이나 앱의 인터페이스를 <span style="background-color: #FBF3DB">**시각적으로 묘사**</span>한 것
- UX(상호작용, 애니메이션 등)를 작성하는 것이 아닌 <span style="background-color: #FBF3DB">**제품의 구조 자체만을 표현**</span>

<p align=center>
<img src="https://velog.velcdn.com/images/player1552/post/34c4e143-32a5-4e60-94e6-af9e1b158a77/image.PNG" style="margin-bottom: 3px" />
</p>
<p style="color: grey" align=center>
  좌측) 출결 및 POS기에서 사용 가능한 구조 / 우측) 장바구니를에 이용 가능한 구조
</p>


### 목업(Mock-up)

- 목업이란 <span style="background-color: #FBF3DB">**실물 크기의 모형**</span>을 말함(ex. 핸드폰 가게의 전시용 핸드폰)
- 실제 제품이 작동하는 방식과 동일하게 <span style="background-color: #FBF3DB">**HTML 문서를 하드코딩으로 작성한 것**</span>~~(기능적 요소 배제)~~
- **하드코딩?**
    - 하드코딩이란 날짜, 시간, 유저 이름 등 상호작용을 통해 얻을 수 있는 <span style="background-color: #FBF3DB">**데이터들을 하나하나 직접 입력하는 방식**</span>

### ⭐ 4일차 까지 배운 개발의 기본 진행 방식

1. <span style="background-color: #FBF3DB">**와이어프레임**</span>을 통한 레이아웃 작성(디자이너가 없다면 디자인도 따로 와이어프레임 작성)
2. <span style="background-color: #FBF3DB">**HTML로 레이아웃**</span> 작성
3. 디자이너 or 자체 제작한 <span style="background-color: #FBF3DB">**디자인 와이어프레임**</span>을 CSS로 적용
4. 값이 항상 변하는 값들은 <span style="background-color: #FBF3DB">**하드코딩**</span>으로 작성
5. 1~4번까지의 과정에서 디자인적인 문제가 없다면 <span style="background-color: #FBF3DB">**Javascript로 하드코딩된 데이터를 변경**</span>


[Atomic CSS 방법론](https://www.sitepoint.com/css-architecture-block-element-modifier-bem-atomic-css/) : 클래스 이름과 구현을 1:1로 일치시켜 아주 작은 단위로 CSS를 작성하는 기법

**Flexbox** : Flex를 통해 **박스를 유연하게** 늘리거나 줄여 **레이아웃을 잡는 방법**

(**Flex,** ⭐ **Grid** 2가지의 적응형 레이아웃 방식이 존재)

## 부모요소에서 적용해야하는 flex 속성

- **flex-direction**: 정렬 축 정하기(row, column, row-reverse, column-reverse)
- **flex-wrap**: 줄 바꿈 설정하기(wrap, wrap-reverse, nowrap)
- **justify-content**: 수평 정렬
- **align-items**: 수직 정렬(flex-start, flex-end, center, space-between(가장 멀리), space-evenly(여백이 모두 동일해짐), space-around(박스를 감싸는 여백이 동일해짐)

## ⭐ 자식요소에서 적용해야하는 flex 속성

### flex: grow shrink basis

- **grow**: 요소의 크기가 늘어날 때 얼마나 늘어나는지(팽창지수 / 전체 팽창지수)
    - (ex. box1 = grow 1, box2 = grow 3, box3 = grow 2일 때, box2는 50%의 공간을 차지한다.)
- **shrink**: 요소의 크기가 얼마나 줄어들 때 얼마나 줄어드는지
    - 기본적으로 1이며, 설정한 비율만큼 grow와 반대로 줄어든다.
    - grow와 함께 쓰는 방식은 권장하지 않는다.
- **basis**: 기본적인 요소의 크기
    - <span style="color: red">**(중요)grow가 0일때의 기본 크기값이다.**</span>
    - 아래 그림은 **flex-grow: 0**, **flex-basis: 50px**일때의 예시다.
        ![](https://velog.velcdn.com/images/player1552/post/874674dd-3825-44b7-8233-b0711099e28a/image.gif)
        
    - ⭐ 아래 그림은 **flex-grow: 1**일 때, **flex-basis: auto**인 경우와 **flex-basis: 0**인 경우이다.
        
        **flex-basis: auto**는 내부에 있는 컨텐츠를 기준으로 기본값을 정의한다.
        하지만 **flex-basis: 0**은 **기본값이 0, 즉 없다는 말**이므로 온전히 **flex-grow** 및 **flex-shrink**에 크기가 결정된다는 것이다.
        
<img style="margin-top: 5px" src="https://velog.velcdn.com/images/player1552/post/374bbf2a-dc0f-4191-83f9-d118fb622f32/image.png">
