# 코드스테이츠 16일차 정리(DOM)

생성일: 2023년 3월 7일 오전 9:15
태그: 코드스테이츠 일일 정리

## 노드와 요소의 차이점

노드 : document, 요소, 텍스트, 주석 등 존재하는 모든 것들을 노드라고 표현한다.

요소 : element라고도 부르며, 태그로 정의된 노드들을 요소라고 부른다.

## document 객체

웹 페이지 그 자체를 의미

웹 페이지에 존재하는 모든 HTML 노드에 접근하기 위해서는 반드시 document 객체로부터 시작해야한다.

---

## DOM 접근 객체

### children

- HTML Collection으로 표현됨

document를 포함한 DOM 노드 객체들이 가지고 있는 자식 요소들을 보여주는 속성

### childNodes

- NodeList로 표현됨

DOM 노드 객체들이 가지고 있는 자식 노드들을 보여주는 속성(텍스트,  주석 등 모두 포함)

### parentElement

DOM 노드 객체들이 가지고 있는 부모 요소를 보여주는 속성

### parentNode

DOM 노드 객체들이 가지고 있는 부모 노드를 보여주는 속성(텍스트,  주석 등 모두 포함)

---

# DOM CRUD

## Create

- document.createElement(”태그”)

특정한 태그를 가진 HTML 요소를 만드는 메소드

## Append

- document.요소.append(추가할 요소)

특정한 요소에 어떤 요소를 추가하는 메소드

## Read

- document.querySelector(”셀렉터”)

tag, id, class를 셀렉터로 입력하여 원하는 노드를 가져올 수 있는 메소드

(중복되는 노드들이 있다면, 가장 처음 들어오는 노드가 들어옴)

## Update

- element.classList.add(”클래스”)

요소들이 가진 클래스 리스트에 새로운 클래스를 추가하는 메소드

- element.textContent = “내용”

요소에 Text를 추가 및 사용하는 속성

## Delete

element.remove()

요소를 DOM에서 제거하는 메소드

## document.querySelector(”셀렉터”).innerHTML = “”;

특정 셀렉터로 정해진 요소의 모든 자식 요소를 제거하는 방법

(하지만, 보안 문제로 인해 사용을 지양하는 편이다.)

- element.removeChild(”셀렉터”)

특정 셀렉터가 자식 요소중에 존재한다면, 제거하는 메소드

## 처음 듣거나 어려웠던 부분(암기할 부분)

추가적인 document 관련 메소드들

Array-like Object