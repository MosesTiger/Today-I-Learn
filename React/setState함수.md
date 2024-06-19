
# React useState와 setState에 대한 문제와 해결 방법

## 상황 설명

React에서 `useState` 훅을 사용하여 상태를 관리할 때, 구조 분해 할당을 통해 상태 값(`value`)과 그 상태를 업데이트하는 함수(`setValue`)를 할당합니다.

예를 들어, `const [value, setValue] = useState(initialValue);`와 같이 사용합니다. 이제 `setValue`를 사용하여 상태 값을 변경해도, 그 변경된 값이 즉시 반영되지 않는 문제가 발생할 수 있습니다. 이는 `useState`가 비동기적으로 동작하기 때문에 발생합니다.

## 문제 원인

`setValue`를 호출해 상태를 변경했지만, 그 변경 사항은 비동기적으로 처리되기 때문에 즉시 접근하려는 경우 여전히 이전의 상태 값을 참조하게 됩니다. 이는 특히 상태 값을 기반으로 다른 작업을 해야 할 때 문제가 됩니다. 예를 들어, 상태 값을 변경하고 그 변경된 값을 사용하여 다른 작업을 수행하려고 할 때, 여전히 이전 값이 사용될 수 있습니다.

## 해결 방법

상태를 함수 형태로 바꿔서, 상태 값을 호출할 때마다 현재 상태 값을 반환하게 합니다. 이는 상태 업데이트가 비동기적으로 처리되더라도 항상 최신 상태 값을 사용할 수 있도록 보장합니다.

`useState`의 `setState` 함수는 콜백 함수를 인자로 받을 수 있습니다. 이 콜백 함수는 이전 상태 값을 인자로 받아 새로운 상태 값을 반환합니다.

### 예시 코드

```javascript
import React, { useState } from 'react';

const ExampleComponent = () => {
  // 상태와 상태 업데이트 함수를 선언합니다.
  const [value, setValue] = useState(0);

  // 상태 값을 업데이트하는 함수입니다.
  const updateValue = () => {
    // setValue에 콜백 함수를 전달합니다.
    setValue((prevValue) => {
      // 콜백 함수는 이전 상태 값을 받아 새로운 상태 값을 반환합니다.
      const newValue = prevValue + 1;
      console.log(newValue); // 항상 최신 상태 값을 출력합니다.
      return newValue;
    });
  };

  return (
    <div>
      <p>Value: {value}</p>
      <button onClick={updateValue}>Increment</button>
    </div>
  );
};

export default ExampleComponent;
```

위 코드에서 `updateValue` 함수는 `setValue`에 콜백 함수를 전달하여 이전 상태 값(`prevValue`)을 받아 새로운 상태 값(`newValue`)을 계산하고 반환합니다. 이렇게 하면 상태 업데이트가 비동기적으로 처리되더라도 항상 최신 상태 값을 사용할 수 있습니다.

이와 같은 방법으로 상태 값을 함수 형태로 바꾸면, 상태 값을 호출할 때마다 항상 현재 상태 값을 반환하게 되어 문제가 해결됩니다.


