# Today I Learned (TIL)

## HTML 기본 구조

### HTML 문서의 기본 구성 요소

- **`<!DOCTYPE html>`**: HTML5 문서임을 선언합니다.
- **`<html>`**: HTML 문서의 루트 요소입니다.
- **`<head>`**: 메타데이터를 포함하는 섹션입니다.
  - **`<title>`**: 브라우저 탭에 표시되는 문서의 제목을 정의합니다.
- **`<body>`**: 실제 문서 내용이 포함되는 섹션입니다.

### 예제 코드

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>yes</title>
</head>
<body>
    <h1>New Awesome Product</h1>
    <img src="https://blob.sololearn.com/courses/np.png" alt="Product Image">
    <p>This is a <i>landing page</i> about <u>our product</u></p>
    <form>
        <label for="name">Name: </label>
        <input type="text" id="name" name="name">
        <br>
        <label for="email">Email: </label>
        <input type="email" id="email" name="email">
        <br>
        <button type="submit">Submit</button>
    </form>
</body>
</html>
```

#### DOCTYPE 선언

- **`<!DOCTYPE html>`**: HTML5 문서를 선언하기 위해 사용합니다.

#### HTML 요소

- **`<html>`**: 문서의 루트 요소입니다.
- **`<head>`**: 문서의 메타데이터를 포함합니다.
- **`<title>`**: 문서의 제목을 정의합니다.
- **`<body>`**: 문서의 콘텐츠를 포함합니다.

#### 헤더 및 텍스트 요소

- **`<h1>`**: 주요 제목을 표시합니다.
- **`<p>`**: 단락을 정의합니다.
- **`<i>`**: 이탤릭체로 텍스트를 표시합니다.
- **`<u>`**: 밑줄로 텍스트를 표시합니다.

#### 이미지 요소

- **`<img src="URL" alt="Description">`**: 이미지를 문서에 삽입합니다.
  - `src`: 이미지 파일의 URL을 지정합니다.
  - `alt`: 이미지가 로드되지 않을 때 표시할 대체 텍스트를 지정합니다.

#### 폼 요소

- **`<form>`**: 사용자 입력을 받기 위한 양식을 정의합니다.
- **`<label for="id">`**: 입력 필드에 대한 설명을 제공합니다.
  - `for` 속성은 `<input>` 요소의 `id` 속성과 연결됩니다.
- **`<input type="text">`**: 텍스트 입력 필드를 정의합니다.
  - `type="text"`: 일반 텍스트 입력 필드입니다.
  - `id` 및 `name` 속성은 필드 식별과 서버로 전송될 데이터의 이름을 지정합니다.
- **`<input type="email">`**: 이메일 입력 필드를 정의합니다.
  - `type="email"`: 이메일 주소 형식의 입력 필드입니다.
- **`<button type="submit">`**: 제출 버튼을 정의합니다.
  - `type="submit"`: 폼 데이터를 제출합니다.

#### 기타 요소

- **`<br>`**: 줄 바꿈을 삽입합니다.

### 주요 포인트 요약

- HTML 문서의 기본 구조를 이해했습니다.
- `<head>`와 `<body>`의 역할을 배웠습니다.
- 다양한 HTML 요소 (`<h1>`, `<p>`, `<img>`, `<form>`, `<input>`, `<label>`, `<button>`)를 사용하여 웹 페이지를 구성하는 방법을 배웠습니다.
- 폼 요소를 사용하여 사용자 입력을 처리하는 방법을 이해했습니다.