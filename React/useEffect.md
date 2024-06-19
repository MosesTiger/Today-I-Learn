
# useEffect와 의존성 배열

리액트(React)에서 `useEffect` 훅과 의존성 배열은 컴포넌트의 상태 관리와 사이드 이펙트를 다루는 중요한 도구입니다. 이 문서에서는 `useEffect` 훅과 의존성 배열의 개념, 사용 방법, 그리고 주의사항에 대해 깊이 있게 설명합니다.

## 리액트 (React)

리액트는 사용자 인터페이스(UI)를 만들기 위한 자바스크립트 라이브러리입니다. 웹 애플리케이션을 만들 때, 리액트를 사용하면 컴포넌트를 이용해 화면을 구성할 수 있습니다.

## 컴포넌트 (Component)

컴포넌트는 UI를 구성하는 블록입니다. 예를 들어, 버튼, 입력 상자, 전체 페이지 등이 컴포넌트가 될 수 있습니다.

## 훅 (Hook)

훅은 리액트의 기능 중 하나로, 함수형 컴포넌트에서 상태(state)와 라이프사이클(lifecycle) 기능을 사용할 수 있게 해줍니다. `useEffect`는 그 중 하나입니다.

## 상태 (State)

상태는 컴포넌트 내부에서 관리하는 동적인 데이터입니다. 예를 들어, 사용자 입력 값이나 서버에서 가져온 데이터가 상태가 될 수 있습니다.

## 속성 (Props)

props는 부모 컴포넌트가 자식 컴포넌트에게 전달하는 데이터입니다. 컴포넌트 간에 데이터를 주고받을 때 사용됩니다.

## useEffect 훅

`useEffect`는 컴포넌트가 화면에 나타날 때나 컴포넌트의 상태 또는 props가 바뀔 때 실행되는 사이드 이펙트를 수행하는 데 사용됩니다. `useEffect`는 두 가지 주요 인수를 가집니다:
1. 실행할 함수
2. 의존성 배열 (dependency array)

### 사용 방법

```javascript
import React, { useEffect } from 'react';

function MyComponent(props) {
  const [count, setCount] = useState(0);

  useEffect(() => {
    // 이 부분은 부수 효과를 수행하는 함수입니다.
    console.log('Component rendered or updated');

    // 여기서 데이터를 가져오거나, 구독을 설정하거나, 타이머를 설정할 수 있습니다.

    // 정리(clean-up) 함수
    return () => {
      console.log('Cleanup before next effect');
      // 타이머를 해제하거나 구독을 취소할 수 있습니다.
    };
  }, [count, props.someProp]); // 의존성 배열

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
}
```

### 의존성 배열 (Dependency Array)

의존성 배열은 `useEffect`가 언제 실행될지를 결정하는 배열입니다. 배열 안에 있는 값이 바뀔 때 `useEffect`가 실행됩니다.

#### 빈 배열 (`[]`)

의존성 배열을 빈 배열로 설정하면, `useEffect`는 컴포넌트가 처음 마운트될 때 한 번만 실행됩니다.

```javascript
useEffect(() => {
  console.log('Component mounted');

  return () => {
    console.log('Component will unmount');
  };
}, []);
```

#### 특정 값이 있는 배열

의존성 배열에 특정 값을 포함하면, 그 값이 변경될 때마다 `useEffect`가 실행됩니다.

```javascript
useEffect(() => {
  console.log('Count changed');

  return () => {
    console.log('Cleanup before count changes');
  };
}, [count]);
```

#### 의존성 배열을 생략

의존성 배열을 생략하면, `useEffect`는 매번 렌더링될 때마다 실행됩니다.

```javascript
useEffect(() => {
  console.log('Effect runs on every render');
});
```

## 주의사항

- **의존성 배열에 필요한 모든 값을 포함**: 의존성 배열에 모든 필요한 값을 포함하지 않으면 예상치 못한 동작이 발생할 수 있습니다. 예를 들어, 상태나 props를 의존성 배열에 포함하여 최신 값을 기반으로 사이드 이펙트를 관리해야 합니다.
- **무한 루프 방지**: 의존성 배열을 올바르게 설정하지 않으면 무한 루프가 발생할 수 있습니다. 이는 성능 저하를 일으킬 수 있으므로 주의가 필요합니다.
- **정리 함수 사용**: `useEffect` 내에서 정리(clean-up) 함수를 사용하여 타이머 해제, 구독 취소 등의 작업을 수행할 수 있습니다. 이는 메모리 누수를 방지하는 데 유용합니다.

## 요약

리액트의 `useEffect` 훅과 의존성 배열은 상태와 속성의 변화에 따른 부수 효과를 관리하는 데 필수적인 도구입니다. 이를 통해 컴포넌트의 라이프사이클 동안 필요한 작업을 효율적으로 수행할 수 있습니다. 의존성 배열을 올바르게 설정하여 부수 효과가 언제 실행될지를 제어하는 것이 중요합니다.

