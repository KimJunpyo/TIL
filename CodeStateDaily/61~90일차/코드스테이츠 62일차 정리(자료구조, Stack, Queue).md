# 코드스테이츠 62일차 정리(자료구조, Stack, Queue)

생성일: 2023년 5월 10일 오전 9:05
태그: 코드스테이츠 일일 정리

# 자료구조

> 여러 데이터의 묶음을 저장하고, 사용하는 방법을 정의한 것
> 
- 내가 원하는 방식으로 데이터를 분석하고 정리하여 활용할 수 있어야 한다.
- 규칙없이 아무렇게나 데이터를 정리하기보단 체계적으로 정리하여 저장하는 것이 활용에 더 유리하다.

## 자료구조의 종류

![](https://velog.velcdn.com/images/player1552/post/ce6cb6d5-5e47-4dc3-9f1a-7180d3b30cfb/image.png)

- 이미 선배 개발자들이 무수히 많은 상황에 따라 어떤 방식으로 데이터를 정리할 것인지에 대한 방법들을 모아서 “자료구조” 라는 이름을 붙여놓았다.
- 특히 알고리즘 문제(코테)에서는 선형구조, 비선형구조를 많이 다루게 되며 특히 Stack, Queue, Tree, Graph 정도는 반드시 알아야 한다.

## 자료구조의 RoadMap

1. 각 자료구조의 특성과 사용하기 적합한 상황에 대해 학습
2. class 키워드를 이용하여 자료구조의 데이터 타입을 직접 정의
3. 자료구조를 활용하여 알고리즘 문제 풀이
(알고리즘 문제를 처음 보자마자 어떤 알고리즘을 적용해야할지 모를 수 있다.
그러나, 코테와 같은 경우에는 시간적 제약이 존재하기 때문에 Array와 같은 JavaScript에서 제공하는 데이터 타입들을 이용해 자료구조의 형태처럼 유사하게 구현하여 문제를 풀어야 한다.)

# Stack

> 데이터를 순서대로 쌓는 자료구조
> 
- 후입 선출의 구조를 가지고 있다.
(1, 2, 3) ⇒ (1, 2, 3, 4) - 4 입력
(1, 2, 3, 4) ⇒ (1, 2, 3) - 4 출력
- 입출력이 하나만 존재한다.
스택의 최상단 위치에서만 값을 넣거나 빼게 된다.
- 데이터는 하나씩 넣고 뺄 수 있다.
한번에 여러개의 데이터를 뺄 수 없고, 마찬가지로 한번에 여러개를 넣을 수 없다.
많은 데이터를 다루기 위해서는 반복문으로 하나씩 입출력을 해야 한다.

## Stack의 실사용 예제

- 대표적으로 **“브라우저의 뒤로 가기, 앞으로 가기”** 와 **“JavaScript의 실행 컨텍스트”** 가 있다.
    1. 새로운 페이지로 이동할 때 현재 페이지를 Prev Stack에 저장
    2. 뒤로 가기 버튼으로 페이지를 이동하면 현재 페이지를 Next Stack에 저장하고 Prev Stack에 있는 가장 최상단의 페이지를 현재 페이지로 꺼내옴
    3. 앞으로 가기 버튼으로 페이지를 이동하면 현재 페이지를 Prev Stack에 저장하고 Next Stack에 있는 가장 최상단의 페이지를 현재 페이지로 꺼내옴

## JavaScript Stack 코드

```jsx
class Stack {
	constructor {
		this.storage = {};
		this.top = -1;
	}
	
	size() {
		return this.top + 1;
	}

	push(element) {
		this.top += 1;
		this.storage[this.top] = element;
	}

	pop() {
		if(this.size() <= 0)
			return;

		const result = this.storage[this.top];
		delete this.storage[this.top];
		this.top -= 1;

		return result;
	}
}
```

# Queue

> 데이터를 줄을 세워서 저장하는 자료구조
> 
- 선입 선출의 구조를 가지고 있다.
(1, 2, 3) ⇒ (1, 2, 3, 4) - 4 추가
(1, 2, 3, 4) ⇒ (2, 3, 4) - 1 제거
- 두 개의 입출력 방향을 가지고 있다.
Queue는 head와 tail로 구성되어 데이터를 출력할 때는 head로 출력을 하고, 새로운 값을 넣을 때는 tail로 입력을 하게 된다.
- 데이터는 하나씩 넣고 뺄 수 있다.
Stack과 마찬가지로 데이터는 하나씩만 입.출력이 진행된다.

## Queue의 실사용 예제

- 대표적으로 **“컴퓨터의 프린트”** 가 있다.
    1. 컴퓨터에서 어떤 문서를 인쇄 요청을 하면, 설정에 따라 문서의 순서를 Queue에 순서대로 입력한다.
    2. Queue에 모든 문서가 들어갔다면, 먼저 들어온 순서부터 인쇄를 시작한다.
- 또한, 프린터나 동영상 시청 등 컴퓨터 장치끼리 데이터를 주고받을 때, 각 장치 사이에 존재하는 속도의 차이나, 시간 차이를 극복하기 위해 **“buffer”**를 사용한다.
- 이 buffer가 Queue로 만들어져 있다.
- 동영상 시청의 경우, 영상을 실행할만한 데이터가 buffer에 담기기 전까지 진행이 되지 않고 대기 상태가 되는데, 이것을 **“buffering”** 이라고 한다.

## JavaScript Stack 코드

```jsx
class Queue {
  constructor() {
    this.storage = {};
    this.front = 0;
    this.rear = 0;
  }

  size() {
    return this.rear - this.front
  }
	
  enqueue(element) {
    this.storage[this.rear] = element;
    this.rear += 1;
  }
	
  dequeue() {
    if(this.size() <= 0) {
      return;
    }

    const result = this.storage[this.front];
    delete this.storage[this.front];
    this.front += 1;

    return result;
  }
}
```

## 처음 듣거나 어려웠던 부분(암기할 부분)

circular queue-원형 큐