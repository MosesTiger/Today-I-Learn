# React의 Suspense

React의 Suspense는 비동기 작업(예: 데이터 가져오기, 코드 분할 등)이 완료될 때까지 컴포넌트 렌더링을 지연시키는 기능입니다. 이는 사용자 경험을 개선하고, 비동기 작업이 완료될 때까지 로딩 상태를 보여줄 수 있게 해줍니다. 현재 Suspense는 코드 분할과 같은 특정 용도에서만 안정적으로 사용할 수 있지만, 데이터 가져오기와 같은 비동기 작업에서도 점진적으로 지원이 확대되고 있습니다.

## 주요 개념

1. **로딩 상태 표시**:
    - Suspense를 사용하여 비동기 작업이 완료될 때까지 로딩 스피너나 대기 메시지를 표시할 수 있습니다.

2. **동작 방식**:
    - Suspense는 자식 컴포넌트가 비동기 작업을 수행할 때, 해당 작업이 완료될 때까지 렌더링을 일시 중단하고 대기 상태를 표시합니다.

## 사용 예시

### 코드 분할에서의 Suspense

React.lazy를 사용하여 동적으로 컴포넌트를 로드하고, Suspense를 사용하여 로딩 상태를 표시하는 예시입니다.

```javascript
import React, { Suspense } from 'react';

// Lazy-loaded 컴포넌트
const OtherComponent = React.lazy(() => import('./OtherComponent'));

function MyComponent() {
  return (
    <div>
      <h1>My Component</h1>
      {/* Suspense를 사용하여 로딩 상태를 표시 */}
      <Suspense fallback={<div>Loading...</div>}>
        <OtherComponent />
      </Suspense>
    </div>
  );
}

export default MyComponent;
```
##데이터 가져오기에 대한 Suspense (실험적 기능)
```
import React, { Suspense } from 'react';

function fetchData() {
  return new Promise((resolve) => {
    setTimeout(() => {
      resolve('Fetched Data');
    }, 2000);
  });
}

const resource = fetchData();

function DataComponent() {
  const data = resource.read();
  return <div>{data}</div>;
}

function App() {
  return (
    <div>
      <h1>Suspense Example</h1>
      <Suspense fallback={<div>Loading...</div>}>
        <DataComponent />
      </Suspense>
    </div>
  );
}

export default App;
```
##요약
Suspense: 비동기 작업이 완료될 때까지 컴포넌트 렌더링을 지연시키고 로딩 상태를 표시하는 기능.
코드 분할: React.lazy와 함께 사용하여 동적으로 로드되는 컴포넌트에 대해 로딩 상태를 표시할 수 있습니다.
데이터 가져오기: React 18에서는 데이터 가져오기에 대해 실험적 지원을 제공하며, Suspense를 사용하여 비동기 데이터 로딩을 처리할 수 있습니다.
