# 8주차 new information

생성일: 2023년 4월 3일 오후 5:04
태그: 코드스테이츠 주간 정리

# 옵저버 패턴

> 객체들간의 상호작용에서 특정 객체의 상태 변화를 관찰하는 패턴
> 
- 참조에 의한 전달 방식으로 객체를 함수의 매개변수로 전달했을 때, 의도치 않은 원본 객체의 변화를 관측할 때 사용할 수 있다.
- 현재 동작되고 있는 객체의 상태가 어떤 값으로 변화하였는지를 체크하는 용도로 사용하는 디자인 패턴이다.
- “한 객체의 상태가 변화하면, 그 객체에 의존성을 가진 다른 객체들에게 알림을 보내는 개념” 이다.

```jsx
class Subject {
  constructor() {
    this.observers = [];
    this.state = null;
  }

  attach(observer) {
    this.observers.push(observer);
  }

  setState(state) {
    this.state = state;
    this.notify();
  }

  notify() {
    for (let observer of this.observers) {
      observer.update(this.state);
    }
  }
}

class Observer {
  constructor() {
    this.state = null;
  }

  update(state) {
    this.state = state;
    console.log("옵저버 상태값 변경", this.state);
  }
}

const subject = new Subject();

const observer1 = new Observer();
const observer2 = new Observer();

subject.attach(observer1);
subject.attach(observer2);

subject.setState("상태값1"); // 옵저버 상태값 변경 상태값1
subject.setState("상태값2"); // 옵저버 상태값 변경 상태값2
```

비슷한 예시로 React 기준 옵저버 패턴 디자인을 적용한 코드이다.

```jsx
import React, { useState, useEffect } from 'react';

function App() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    // count 상태가 변경될 때마다 실행될 함수
    console.log(`Count changed to ${count}`);
  }, [count]);

  const handleIncrement = () => {
    setCount(count + 1);
  };

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={handleIncrement}>Increment</button>
    </div>
  );
}

export default App;
```

하지만, 위 코드의 예시는 완벽한 옵저버 디자인 패턴이라고 부르지는 않고, 옵저버-like 패턴이라고 불린다.

## 옵저버-like 패턴

> 상태변화를 감지하는 객체가 존재하지 않으며, 상태값의 변화를 감지한다는 의미보다 특정 상태값이 변경되면서 렌더링이 됐다는 것을 인지하기 위해 사용하는 패턴

옵저버 패턴과는 사용 목적이 다르다.
> 

## 불변 객체 패턴

> 객체는 참조 자료형-객체로 분류되어 const로 선언한 객체임에도 내부 내용을 변경할 수 있고, 함수에 매개변수로 전달하면 참조에 의한 전달이 발생하여 내부에서 변경한 내용이 원본 객체에도 영향을 주는 특징이 있다.

이런 특징을 방지하여, 원본 객체가 변하지 않도록 하는 패턴을 불변 객체 패턴이라고 한다.
> 
- Object.assign(), 얕은 복사, 깊은 복사 등 원본 값을 기반으로 새로운 객체를 만들어서 변경사항을 적용시키는 패턴이다.
- 또는 Object.freeze() 메소드를 이용하여 불변 객체로 만들 수 있다.
하지만 객체 내부의 중첩 객체는 변경 가능하다.

## CSRF

> Cross Site Request Forgery의 약자로 웹 어플리케이션 취약점 중 하나로 인터넷 사용자가 자신의 의지와는 무관하게 공격자가 의도한 행위를 특정 웹사이트에 요청하게 만드는 공격이다.
> 
- 사용자가 특정 사이트를 신뢰하는 상태의 브라우저(로그인을 통해 쿠키값을 가진 브라우저 등)로 특정 공격 코드가 담긴 사이트 링크, 혹은 HTML 편집기로 HTML 공격 코드 자체를 담아 공격한다.
- 특히 HTML 편집기로 <img src=”공격할 링크의 개인정보 화면 링크” /> 와 같은 방식으로 메일창이 렌더링 될 때 같이 동작되는 방식으로 공격을 하는 경우가 가장 많고 위험하다.
- CORS 오류 외에도 SameSite 쿠키 방식, CSRF 토큰 방식으로 해결이 가능하지만, 특별한 케이스의 경우 SameSite 쿠키, CSRF 토큰 방식 등을 이용하여 추가 보안을 해줘야 한다.