# 7주차 new information

생성일: 2023년 3월 27일 오후 6:11
태그: 코드스테이츠 주간 정리

# 에러 공유

## **에러 1**

<aside>
💡 is a void element tag and must neither have `children` nor use `dangerouslysetinnerhtml`.

</aside>

> input 태그를 열림태그와 닫힘태그로 작성하여 그 안에 내용을 추가하는 경우에 생기는 오류
> 

### **당시 에러 상황**

- 특정 Page에서 Modal 레이아웃의 div 태그를 input으로 잘못 바꾸고 발생한 오류

### **해결 방법**

1. div 태그로 다시 변경
2. input 태그를 한줄 태그로 변경 후, 안의 내용을 value={}로 처리

## **에러 2**

<aside>
💡 react form submission canceled because the form is not connected

</aside>

> form 형식에 button 태그가 두 개 이상 있을 때 생기는 오류
> 

### 당시 에러 상황

- form 형식에서 submit이 엔터로 눌리지 않고 나타난 오류

### 해결 방법

1. button 태그에서 submit 버튼이 아닌 경우, type=”button” 이라는 속성 명시해주기
2. button을 form 내에서 하나로 사용

# 파일(이미지)을 서버에 전송 및 저장, 불러오기를 하는 방법

1. FormData로 서버에 전송하기
2. AWS S3에 저장 후, 링크를 서버에 전송하기

## FormData 객체

> 폼(HTML Form 데이터)을 쉽게 보내도록 도와주는 객체
> 
- form 태그의 속성에는 name, action, method, autocomplete, enctype이 있다.
- enctype 속성에는 세 가지 값이 존재한다.
    - application/x-www-form-urlencoded: 기본 값. 서버에 보내기 전에 인코딩하여 전송한다는 뜻
    - text/plain: 해당 form을 HTML까지 모두 “읽을 수 있는 값들만 문자열화” 하여 전송한다는 뜻
    - multipart/form-data: 파일을 전송할 때 파일의 형태로 전송한다는 뜻
- FormData 객체는 이 multipart/form-data의 형태로 서버에 전송하기 위해서 사용되는 객체이다.

```jsx
import "./App.css";

function App() {

  const onChangeImg = (e) => {
    e.preventDefault();
    const fileObject = new FormData();

    if (e.target.files) {
      fileObject.append("files", e.target.files[0]);
      for (let key of fileObject.entries()) {
        console.log(key);
      }
    }
  };

  return (
    <div>
      <form id="asd">
        <input type="file" value="" onChange={(e) => onChangeImg(e)} />
      </form>
    </div>
  );
}

export default App;
```

![](https://velog.velcdn.com/images/player1552/post/c96bc5e9-1167-484a-9822-60cb5ba13b12/image.PNG)

- FormData 객체는 console.log로 간단하게 데이터를 확인할 수 없고, entries, keys 등을 이용하여 배열화 한 뒤, 확인이 가능하다.
- FormData 객체는 그 파일의 수정 시간, 이름, 크기, 종류 등 여러가지 meta data를 담고 있다.

<aside>
❗ 백엔드와 기능 설계를 할 때, 프론트단에서 파일을 외부 스토리지 서비스에 올리고 그 링크를 서버에 전달할 지, 백엔드에서 직접 FormData 객체를 파일화하여 외부 스토리지 서비스에 올리고, 링크를 저장해놓을지는 논의하여 정하게 된다.(보통 백엔드에서 많이 한다)

</aside>

### 추가로 공부하면 좋은 부분

1. blob - json 파일을 담아서 보낼 때 처리하는 방법
2. aws s3에 직접 저장 후 보내는 방법

## 프레임워크와 라이브러리의 차이

- 프레임워크와 라이브러리의 대표적인 차이점은 “제어 흐름”이 어디에 있는지이다.
- 프레임워크는 어플리케이션 개발에 필수적인 코드, 알고리즘, DB 커넥션 등 구조를 제공하며, 이 구조에서 개발자가 코드를 작성하여 개발을 하게 된다.
- 라이브러리는 외부 도구로써 재사용성이 있는 모듈 등을 담고 있으며, 개발자가 원하는 경우 선택하여 호출할 수 있다.

<aside>
❗ 프레임워크는 제어 흐름을 가지고 있으며, 작성된 코드는 프레임워크의 구조 안에서 동작되지만, 라이브러리는 개발자가 만들어놓은 코드에서 개발자가 원하는 기능만 호출하여 개발자만의 제어 흐름을 가지게 되는 것이 가장 큰 차이점이다.

</aside>

## 멱등성

> 어떤 대상에 같은 연산을 여러번 적용해도 결과가 달라지지 않는 성질
> 

대표적인 예) HTTP 메소드 기준 GET 메소드⇒ 아무리 요청을 하더라도 결과값은 변하지 않는다.

## custom hooks

> 개발을 할 때 useState, useEffect, 기타 여러 React hook들과 로직을 반복적으로 사용하게 되는데, 반복되는 로직을 하나로 묶어서 새로운 hook으로 사용하는 것
> 
- 코드의 중복을 줄이고 재사용성을 높이며 유지보수를 쉽게 하기 위해 사용한다.
- 커스텀 훅의 시작 이름은 반드시 use여야한다.

### 기존 코드

```jsx
// App.js
import "./App.css";
import {useState, useEffect} from "react";

function App() {
  const [userList, setUserList] = useState([]);
  const url = "https://jsonplaceholder.typicode.com/users";

  useEffect(() => {
    fetch(url)
      .then((response) => response.json())
      .then((response) => setUserList(response))
      .then(() => console.log(userList));
  }, []);
  return (
    <>
      <div>
        {userList.map((e) => (
          <li key={e.id}>{e.name}</li>
        ))}
      </div>
    </>
  );
}

export default App;
```

### 커스텀 훅을 적용한 코드

```jsx
// App.js
import "./App.css";
import useData from "./hooks/useData";

function App() {
  const userList = useData("https://jsonplaceholder.typicode.com/users");

  return (
    <>
      <div>
        {userList.map((e) => (
          <li key={e.id}>{e.name}</li>
        ))}
      </div>
    </>
  );
}

export default App;

// useData.js
import {useEffect, useState} from "react";

function useData(url) {
  const [userList, setUserList] = useState([]);
  useEffect(() => {
    fetch(url)
      .then((response) => response.json())
      .then((response) => setUserList(response));
  }, [url]);
  return userList;
}

export default useData;
```