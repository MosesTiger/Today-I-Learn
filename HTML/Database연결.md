# HTML Form Attributes for Sending Data to a Database

## Introduction

HTML 폼은 사용자가 입력한 데이터를 서버로 전송하는 데 사용됩니다. 이 데이터를 데이터베이스에 저장하기 위해서는 폼의 여러 속성을 올바르게 설정해야 합니다. 주요 속성들은 다음과 같습니다:

### `action`

- **설명**: 폼 데이터를 전송할 URL을 지정합니다. 서버 측에서 이 URL을 처리하여 데이터를 데이터베이스에 저장합니다.
- **예시**: `<form action="/submit_form" method="post">`

### `method`

- **설명**: 폼 데이터를 전송할 HTTP 메서드를 지정합니다. 일반적으로 `POST` 또는 `GET` 메서드를 사용합니다. 데이터베이스에 데이터를 저장하기 위해서는 보통 `POST` 메서드를 사용합니다.
- **예시**: `<form action="/submit_form" method="post">`

### `name`

- **설명**: 폼 요소의 이름을 지정합니다. 서버 측 스크립트에서 이 이름을 사용하여 전달된 데이터를 식별합니다.
- **예시**: `<input type="text" name="username">`

### `id`

- **설명**: 폼 요소의 고유 식별자를 지정합니다. `label` 요소와 연결하거나 자바스크립트에서 해당 요소를 참조할 때 사용됩니다.
- **예시**: `<input type="text" id="username" name="username">`

### `type`

- **설명**: 입력 요소의 유형을 지정합니다. 일반적인 값으로는 `text`, `password`, `email`, `submit` 등이 있습니다.
- **예시**: `<input type="email" name="email">`

### `value`

- **설명**: 입력 요소의 초기 값을 지정합니다.
- **예시**: `<input type="text" name="username" value="JohnDoe">`

### `placeholder`

- **설명**: 입력 요소에 대한 안내 텍스트를 지정합니다. 사용자가 입력 필드를 비워두면 이 텍스트가 표시됩니다.
- **예시**: `<input type="text" name="username" placeholder="Enter your username">`

### `required`

- **설명**: 이 속성이 설정된 입력 필드는 반드시 값이 입력되어야 합니다.
- **예시**: `<input type="text" name="username" required>`

## Example Form

아래는 위의 속성들을 포함한 예시 폼입니다:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Form Example</title>
</head>
<body>
    <form action="/submit_form" method="post">
        <label for="username">Username: </label>
        <input type="text" id="username" name="username" placeholder="Enter your username" required>
        <br><br>
        <label for="email">Email: </label>
        <input type="email" id="email" name="email" placeholder="Enter your email" required>
        <br><br>
        <button type="submit">Submit</button>
    </form>
</body>
</html>
