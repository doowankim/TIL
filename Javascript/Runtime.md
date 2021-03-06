# Javscript 런타임에 대해 알아보자

> 일반적으로 런타임이란 `프로그래밍 언어가 구동되는 환경`을 말합니다.
> Node.js나 크롬 등의 여러 브라우저들은 자바스크립트가 구동되는 환경이기 때문에, Node.js나 브라우저들을 자바스크립트 런타임이라고 합니다.

## 싱글 스레드, 논 블로킹 언어: Javascript

![](https://images.velog.io/images/kimdw1991/post/843219e3-08ce-4947-af1f-e2cc34ed0c56/%E1%84%87%E1%85%B5%E1%84%83%E1%85%A9%E1%86%BC%E1%84%80%E1%85%B5%E1%84%8E%E1%85%A5%E1%84%85%E1%85%B5.png)

- 자바스크립트는 **Single-thread 언어**이다.
- Single-threaded란, **호출한 함수들이 쌓이는 call stack이 하나**인 것을 의미한다.
- 즉, call stack이 하나인 자바스크립트는 **한 번에 한 가지만 수행할 수 있는 언어**이다.

모든 자바스크립트 엔진은 **Memory Heap**과 **Call Stack**으로 이루어져 있다.
`Memory Heap`: 자바스크립트를 사용해 만든 함수, 배열, 객체 등의 저장 공간
`Call Stack`: 함수 실행 호출이 쌓이는 곳. 호출이 끝나면 사라진다.

### 구동 순서

call stack -> Web APIs -> callback queue -> event loop 동작 -> call statck 실행 -> call stack 제거

#### Web API

`Call Stack`에서 비동기 함수나 `setTimeout`, `setInterval` 등의 호출이 있을 때, `Web API`로 이동한다. 즉, 당장 실행되지 않는 함수들이 호출이 되기를 기다리는 공간이라고 볼 수 있으며, `Web API`로 이동될 때, `Call Stack`에서는 호출이 끝난 것으로 간주되어 사라지게 된다.

- _알고리즘 문제를 풀 때 setTimeout 등을 사용하지 않는(?) 사용할 수 없는(?) 이유이기도 하다._

정해진 시간이 지나면 함수 호출을 위해 `Web API`에서 빠져 나와 `Callback Queue`로 이동한다.

따라서 API로 이동된 순서는 중요하지 않으며, 정해진 시간이 짧은 경우에는 API에 늦게 들어온 함수라 해도 먼저 `Callback Queue`로 이동된다.

#### Callback Queue

`Web API`에서 넣어준 함수들이 단지 줄을 서 있는 공간이며, 이후 순서가 바뀌지 않는다.

#### Event Loop

`Event Loop`이 동작하려면 아래의 두 가지 조건이 충족되어야 한다.

1. `Callback Queue`에 실행해야 할 함수가 있다.
2. `Call Stack`이 비어 있다. (run to completion)

조건이 충족될 때, `Callback Queue`에 있는 함수들을 순서대로 `Call Stack`으로 이동시켜 해당 함수가 호출되도록 한다.

- Run to completion 이란?

  자바스크립트는 현재 위치한 곳의 함수들의 호출이 끝나야만 다음 작업을 실행한다.

  예를 들어 `setTimeout`에 3초의 시간을 두고 함수를 실행하고자 할 때, 3초 후 `Callback Queue`로 넘어가긴 하겠지만 그 사이 `Call Stack`이 비워지지 않는다면 `Event Loop`는 동작하지 않을 것이다.

  즉, `setTimeout`으로 걸어둔 함수가 반드시 3초 뒤에 실행될 것이라는 보장이 없다는 뜻이기도 하다.

  나아가 `Event Loop`는 `Callback Queue`뿐 아니라 `render Queue`, `job Queue` 등 여러가지 큐를 관리하고 실행하기 때문에 내가 원하는 정확한 시점에 `Event Loop`이 동작하여 함수를 실행하지 않을 수도 있다는 점을 유념하자.

  ***

  ***

  ***

  ***

  <자바스크립트 엔진 함수처리 예시>

1. setTimeout 함수가 실행되면서 call stack에 올라간다.

```jsx
setTimeout(() ⇒ {
	console.log('hi)
}, 1000)
```

![](https://images.velog.io/images/kimdw1991/post/af5f2205-7c39-40dd-9354-a80a127706e4/eventloop1.png)

1. call stack에서는 web API임을 확인하고 web API에 함수를 넘겨준다.

![](https://images.velog.io/images/kimdw1991/post/e7984a33-de5d-4a3d-8cbe-286e9a2818d0/eventloop2.png)

2. call stack 에서는 해당 함수를 web API에 넘겨줬으므로 pop(데이터 추출) 시킨다.

![](https://images.velog.io/images/kimdw1991/post/d377f2fd-df9b-4bec-8b94-18fc8e3b79d9/eventloop3.png)

3. web API에서는 1000ms 동안 대기한다.

![](https://images.velog.io/images/kimdw1991/post/ddc35b5f-5397-4fa0-a087-fcc7b29e5561/eventloop4.png)

4. 1000ms가 지나면 Event Loop에게 callback 함수를 넘겨준다.

![](https://images.velog.io/images/kimdw1991/post/f046b0d7-864e-4e52-8409-6ef81ab10651/eventloop5.png)

5. Event Loop에서는 call stack이 비어있는 것을 확인하고 callback 함수를 call stack에 올린다.

![](https://images.velog.io/images/kimdw1991/post/3f3138cf-0433-4539-9fea-0f2e5c5b50d7/eventloop6.png)

6. call stack에서 callback 함수가 실행되면서 최종적으로 hi가 console.log에 출력된다.

![](https://images.velog.io/images/kimdw1991/post/703698dc-7fd3-4b9f-90ad-e9d6d6a8a09d/eventloop7.png)
