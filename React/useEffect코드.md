# React useState와 useEffect 훅을 사용한 예제

이 문서에서는 `useState`와 `useEffect` 훅을 사용하여 간단한 카운터 애플리케이션을 구현하는 방법을 설명합니다. 이 예제에서는 버튼을 클릭할 때 카운터를 증가시키고, 윈도우 클릭 이벤트에 반응하는 이벤트 리스너를 관리합니다.

## 코드 설명

```javascript
import { useState, useEffect } from 'react';

export default function App() {
  const [counter, setCounter] = useState(0);

  function handleClick() {
    setCounter((prev) => prev + 1);
  }

  useEffect(() => {
    function addMouseEvent() {
      console.log(counter);
    }

    window.addEventListener('click', addMouseEvent);

    return () => {
      console.log('클린업 함수 실행!', counter);
      window.removeEventListener('click', addMouseEvent);
    };
  }, [counter]);

  return (
    <>
      <h1>{counter}</h1>
      <button onClick={handleClick}>+</button>
    </>
  );
}
```

### 주요 개념 설명

#### 1. `useState` 훅

- `const [counter, setCounter] = useState(0);`
  - `useState` 훅은 상태 변수를 선언합니다. 여기서는 `counter`라는 상태 변수를 선언하고, 초기값을 `0`으로 설정합니다.
  - `setCounter` 함수는 `counter` 상태를 업데이트하는 함수입니다.

#### 2. `handleClick` 함수

- `function handleClick() { setCounter((prev) => prev + 1); }`
  - 이 함수는 버튼이 클릭될 때 호출됩니다.
  - `setCounter` 함수를 사용하여 `counter` 값을 1 증가시킵니다. 이전 상태값 `prev`를 사용하여 안전하게 상태를 업데이트합니다.

#### 3. `useEffect` 훅

- `useEffect(() => { ... }, [counter]);`
  - `useEffect` 훅은 컴포넌트가 렌더링될 때와 `counter` 값이 변경될 때 실행됩니다.
  - 첫 번째 인수는 실행할 함수이고, 두 번째 인수는 의존성 배열입니다. 이 배열에 포함된 값이 변경될 때마다 `useEffect`가 실행됩니다.

- `function addMouseEvent() { console.log(counter); }`
  - `addMouseEvent` 함수는 클릭 이벤트가 발생할 때 실행되며, 현재 `counter` 값을 콘솔에 출력합니다.

- `window.addEventListener('click', addMouseEvent);`
  - `addMouseEvent` 함수를 전역 클릭 이벤트 리스너로 추가합니다. 즉, 윈도우에서 클릭이 발생할 때마다 `addMouseEvent` 함수가 호출됩니다.

- `return () => { ... }`
  - `useEffect` 내에서 반환되는 함수는 클린업(clean-up) 함수입니다. 이는 컴포넌트가 언마운트되거나 `useEffect`가 재실행되기 전에 실행됩니다.
  - 여기서는 클릭 이벤트 리스너를 제거하고, "클린업 함수 실행!" 메시지와 현재 `counter` 값을 콘솔에 출력합니다.

#### 4. JSX 반환값

- `<h1>{counter}</h1>`
  - 현재 `counter` 값을 화면에 표시합니다.

- `<button onClick={handleClick}>+</button>`
  - 이 버튼을 클릭하면 `handleClick` 함수가 호출되어 `counter` 값을 1 증가시킵니다.

### 코드 실행 흐름

1. 컴포넌트가 처음 렌더링될 때 `useState` 훅으로 초기 상태 `counter`가 `0`으로 설정됩니다.
2. `useEffect` 훅이 실행되어 클릭 이벤트 리스너가 추가됩니다. 현재 `counter` 값(`0`)이 콘솔에 출력됩니다.
3. 사용자가 버튼을 클릭하면 `handleClick` 함수가 호출되어 `counter` 값이 1 증가합니다.
4. `counter` 값이 변경되면 `useEffect` 훅이 다시 실행됩니다.
   - 이전 이벤트 리스너가 제거되고(클린업 함수), 새로운 이벤트 리스너가 추가됩니다. 새로운 `counter` 값이 콘솔에 출력됩니다.
5. 윈도우에서 클릭 이벤트가 발생하면 `addMouseEvent` 함수가 실행되어 현재 `counter` 값을 콘솔에 출력합니다.

### 요약

이 코드는 `useState`와 `useEffect`를 사용하여 상태와 이벤트 리스너를 관리하는 방법을 보여줍니다. `useEffect`의 클린업 함수를 통해 컴포넌트가 업데이트되거나 언마운트될 때 이벤트 리스너를 정리하는 방법도 함께 제공합니다.
