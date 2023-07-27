# React

## Q1. 의존성 주입에 대해서

- `A 가 B 에 의존한다` 는 `A 가 B 를 사용한다.` 와 동일하다.
- 의존성은 둘 이상의 객체의 관계에 대해서 설명할때 사용하며 나쁜 것은 아니다.
- 의존성의 정도를 결합도라고 표현하며, 결합도가 강한 관계일수록 좋지못하다.
- 응집도는 하나의 목적과 책임을 위해 객체 내부의 것들이 모여있는 정도를 말하며, 높을수록 좋다.
- 의존 관계를 만들기위해 의존성을 주입할 수 있다. (A 에 B 의 의존성을 주입한다.)
- 왜 주입하는가. A 는 B 가 변하면, A 는 변한다. 의존하기때문에 B 에 끌려다닌다.
- B 를 A 에 주입하는 방식을 적용하게되면, B 의 사용처인 A 가 제어를 역전할 수 있다. 사용처에서 의존하는 것들을 컨트롤할 수 있다. B 는 A 의 존재에 대해 모르게 하기때문에 하고싶은 것들을 한다.
- 방법은 중간에 인터페이스를 두는 것. B 가 사용하는 것들을 인터페이스로 추상화하고, A 는 인터페이스의 구현체가 된다. A 구현체가 변경이 되더라도, B 는 사용하는 것들에 대한 인터페이스를 참조하기때문에 결합도가 낮아진다.

## Q2. Re-rendering 에 대해서

- Concurrency 이란, 하나의 스레드가 여러작업들을 컨텍스트 스위칭하며, 동시다발적을 정지하고 실행해나가는 것을 의미한다.
- Parallelism 이란, 여러개의 스레드가 여러작업들을 각각 병렬 실행하는 것을 의미한다.
- 리액트는 UI 렌더링 동작을 선언화한다. 컴포넌트를 정의하면, 어떻게 그려질지는 리액트에 위임한다.
- 리액트는 재조정(Reconciliation) 과 (렌더링)Render 두 동작을 한다. 재조정은 VirtualDOM 과 실제 DOM 의 바뀐부분을 찾는 것을 의미하고, 렌더링은 실제 DOM 에 바뀐 부분을 그리는 것을 의미한다.
- 재조정은 React v16 이전의 Stack 리컨사일러에서 Fiber 리컨사일러로 대체되었다.
- Stack Reconciler 는 재조정하고, 렌더링하는 작업을 하나의 큰 동기적 태스크로 삼는다. 때문에 도중에 일시정지되고 취소될 수 없다.
- Fiber Reconciler 는 우선순위로 정해진 작업의 조각들을 동시적(Concurrency)으로 일시정지와 재실행을 반복해나간다. Fiber 는 트리 아키텍처이며, 노드의 참조를 가리키는 링크드 리스트 자료구조를 가진다.
- 노드(작업의 조각) 을 실행하다가 다른 노드 참조로 이동하고 하면서, 변경사항의 정보들을 각 노드마다 들고 있다가. 모든 Fiber 트리가 탐색이 완료되면 실제 DOM 에 반영한다. (렌더링)
- Fiber 는 디바운스와 비슷하지만 다르다. 액션의 딜레이가 아니라 액션은 바로바로 일어나면서 렌더링을 한번에 한다. (인풋에 검색어를 마구 입력해도 결과를 한번에 그리기때문에 화면이 중간중간 멈추지않는다.)

## Q3. 왜 import React 를 하지않아도 되는걸까

- React 17 이전의 방식은 JSX 를 React.createElement() 로 변환하는 방식이다.
- 두가지 단점이 있다. (1) import React 되어야하고, (2) 성능에 제약이 있다.
- JSX 를 react/jsx-reuntime 의 jsx 함수로 변환한다. react/jsx-runtime 은 명시하지않아도 되고 바벨이 알아서 주입한다.

```jsx
import { jsx as _jsx } from "react/jsx-runtime";

function App() {
  return _jsx("h1", { children: "Hello world" });
}
```

Reference

- <https://jbee.io/developments/frontend-testing-and-dependency/>
- <https://blog.mathpresso.com/react-deep-dive-fiber-88860f6edbd0>
- <https://so-so.dev/react/import-react-from-react/>
- <https://tv.naver.com/v/23652451>
