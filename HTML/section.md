
## HTML 코드 설명

- `<header>My Header</header>`: 
  - 페이지의 헤더를 나타냅니다. 배경색, 텍스트 정렬, 패딩 등으로 스타일링이 되어 있습니다.
  
- `<main>`: 
  - 페이지의 주요 콘텐츠를 담는 영역입니다. 내부에 두 개의 섹션이 있습니다.
  - `<section class="content">Main Section</section>`: 
    - 메인 콘텐츠 영역을 나타냅니다. 배경색, 텍스트 색상, 패딩, 높이, flex 값으로 스타일링이 되어 있습니다.
  - `<section class="side">Side Section</section>`: 
    - 사이드바 콘텐츠 영역을 나타냅니다. 배경색, 패딩, flex 값으로 스타일링이 되어 있습니다.
    
- `<footer>My Footer</footer>`: 
  - 페이지의 푸터를 나타냅니다. 배경색, 텍스트 색상, 텍스트 정렬, 패딩 등으로 스타일링이 되어 있습니다.

## HTML 코드

```html
<header>My Header</header>
<main>
    <section class="content">Main Section</section>
    <section class="side">Side Section</section>
</main>
<footer>My Footer</footer>
```

## CSS 코드 설명

- `header`:
  - 배경색을 `#77adda`로 설정.
  - 텍스트를 가운데 정렬.
  - 20픽셀의 패딩 적용.

- `footer`:
  - 배경색을 검정(`black`)으로 설정.
  - 텍스트 색상을 흰색(`white`)으로 설정.
  - 텍스트를 가운데 정렬.
  - 10픽셀의 패딩 적용.

- `.content`:
  - 배경색을 `#2ca152`로 설정.
  - 텍스트 색상을 흰색(`white`)으로 설정.
  - 20픽셀의 패딩 적용.
  - 높이를 200픽셀로 설정.
  - flex 속성을 3으로 설정하여 main 요소 내에서 공간을 더 많이 차지하도록 함.

- `.side`:
  - 배경색을 `#e6e6a5`로 설정.
  - 20픽셀의 패딩 적용.
  - flex 속성을 1로 설정하여 main 요소 내에서 공간을 덜 차지하도록 함.

- `main`:
  - display 속성을 `flex`로 설정하여 내부 요소들이 가로로 배치되도록 함.

## CSS 코드

```css
header {
    background-color: #77adda;
    text-align: center;
    padding: 20px;
}
footer {
    background-color: black;
    color: white;
    text-align: center;
    padding: 10px;
}
.content {
    background-color: #2ca152;
    color: white;
    padding: 20px;
    height: 200px;
    flex: 3;
}
.side {
    background-color: #e6e6a5;
    padding: 20px;
    flex: 1;
}
main {
    display: flex;
}
```
