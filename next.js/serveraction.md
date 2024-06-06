
HTML과 React의 폼 제출 방식 비교

### HTML에서의 폼 제출

HTML에서 폼 데이터를 제출할 때는 `action` 속성을 사용하여 데이터를 제출할 URL을 지정합니다. 이 URL은 일반적으로 데이터를 처리할 API 엔드포인트입니다.

```html
<form action="/submit-form" method="post">
  <input type="text" name="username">
  <button type="submit">Submit</button>
</form>
```
- `action="/submit-form"`: 이 폼이 제출되면, 데이터를 `/submit-form` URL로 전송합니다.
- `method="post"`: 데이터 전송 방식은 POST입니다.

### React에서의 폼 제출

React에서는 `action` 속성이 특수한 prop으로 간주됩니다. React는 이 속성을 사용하여 폼 제출 시 특정 동작을 수행할 수 있도록 확장합니다. 즉, React는 `action` 속성을 기반으로 서버 액션을 호출하는 메커니즘을 제공합니다.

```jsx
import React from 'react';
import { useServerAction } from 'your-server-action-library';

function MyForm() {
  const handleSubmit = useServerAction('/submit-form');

  return (
    <form onSubmit={handleSubmit}>
      <input type="text" name="username">
      <button type="submit">Submit</button>
    </form>
  );
}
```
- `useServerAction('/submit-form')`: 폼이 제출될 때 서버 액션을 호출하는 핸들러를 생성합니다.
- `onSubmit={handleSubmit}`: 폼 제출 시 생성된 핸들러를 사용합니다.

### 서버 액션과 API 엔드포인트

React에서 서버 액션을 사용하면 수동으로 API 엔드포인트를 생성할 필요가 없습니다. 서버 액션은 자동으로 POST API 엔드포인트를 생성하고, 이 엔드포인트를 통해 데이터를 처리합니다. 이는 서버 액션이 폼 데이터를 직접 서버에서 처리할 수 있게 해주기 때문입니다.

#### 서버 액션의 동작 방식

1. **서버 액션 생성**: 서버 액션을 정의하고, 이를 폼 제출 시 호출하도록 설정합니다.
2. **자동 API 엔드포인트 생성**: 서버 액션을 설정하면, React는 자동으로 POST API 엔드포인트를 생성합니다.
3. **폼 데이터 전송**: 폼이 제출되면, 서버 액션은 폼 데이터를 이 자동 생성된 API 엔드포인트로 전송합니다.
4. **서버에서 데이터 처리**: 서버 액션이 데이터를 처리하고 필요한 작업을 수행합니다. 예를 들어, 데이터베이스에 데이터를 저장하거나 검증을 수행할 수 있습니다.

### 요약

- **HTML 폼 제출**: `action` 속성을 사용하여 폼 데이터를 전송할 URL을 지정합니다.
- **React 폼 제출**: `action` 속성을 기반으로 서버 액션을 호출하여 데이터를 처리합니다.
- **서버 액션의 장점**: 수동으로 API 엔드포인트를 생성할 필요가 없으며, 폼 데이터 처리를 자동화하고 간소화합니다.

React의 서버 액션을 사용하면 폼 제출이 간단해지고, 서버에서 직접 데이터를 처리할 수 있어 효율적이고 보안이 강화된 웹 애플리케이션을 구축할 수 있습니다.
