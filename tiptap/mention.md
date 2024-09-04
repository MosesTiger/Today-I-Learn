### 1. Mentions 기능 구현 예시

```javascript
import { Editor } from '@tiptap/core';
import Mention from '@tiptap/extension-mention';
import StarterKit from '@tiptap/starter-kit';

const editor = new Editor({
  element: document.querySelector('#editor'),
  extensions: [
    StarterKit,
    Mention.configure({
      HTMLAttributes: {
        class: 'mention',
      },
      suggestion: {
        items: (query) => {
          return [
            { id: '1', label: 'Alice' },
            { id: '2', label: 'Bob' },
            { id: '3', label: 'Charlie' },
          ].filter(item => item.label.toLowerCase().startsWith(query.toLowerCase()));
        },
        render: () => {
          let popup;

          return {
            onStart: props => {
              popup = document.createElement('div');
              popup.className = 'mention-popup';
              props.items.forEach(item => {
                const button = document.createElement('button');
                button.innerText = item.label;
                button.addEventListener('click', () => {
                  props.command({ id: item.id });
                });
                popup.appendChild(button);
              });
              document.body.appendChild(popup);
            },
            onUpdate: props => {
              popup.innerHTML = '';
              props.items.forEach(item => {
                const button = document.createElement('button');
                button.innerText = item.label;
                button.addEventListener('click', () => {
                  props.command({ id: item.id });
                });
                popup.appendChild(button);
              });
            },
            onExit: () => {
              popup.remove();
            },
          }
        },
      },
    }),
  ],
});

// HTML Element for the editor
document.body.innerHTML = '<div id="editor"></div>';
```

### 2. 마크다운 문서

```markdown
# Tiptap Mention 기능 구현

Tiptap의 `Mention` 확장은 사용자 입력 중 특정 문자를 기반으로 제안을 표시하는 기능을 제공합니다. 이 문서에서는 기본적인 `Mention` 기능을 구현하고 설명합니다.

## 1. 설치

우선 `@tiptap/core`, `@tiptap/starter-kit` 및 `@tiptap/extension-mention` 패키지를 설치해야 합니다.

```bash
npm install @tiptap/core @tiptap/starter-kit @tiptap/extension-mention
```

## 2. 코드 설명

```javascript
import { Editor } from '@tiptap/core';
import Mention from '@tiptap/extension-mention';
import StarterKit from '@tiptap/starter-kit';

const editor = new Editor({
  element: document.querySelector('#editor'),
  extensions: [
    StarterKit,
    Mention.configure({
      HTMLAttributes: {
        class: 'mention',
      },
      suggestion: {
        items: (query) => {
          return [
            { id: '1', label: 'Alice' },
            { id: '2', label: 'Bob' },
            { id: '3', label: 'Charlie' },
          ].filter(item => item.label.toLowerCase().startsWith(query.toLowerCase()));
        },
        render: () => {
          let popup;

          return {
            onStart: props => {
              popup = document.createElement('div');
              popup.className = 'mention-popup';
              props.items.forEach(item => {
                const button = document.createElement('button');
                button.innerText = item.label;
                button.addEventListener('click', () => {
                  props.command({ id: item.id });
                });
                popup.appendChild(button);
              });
              document.body.appendChild(popup);
            },
            onUpdate: props => {
              popup.innerHTML = '';
              props.items.forEach(item => {
                const button = document.createElement('button');
                button.innerText = item.label;
                button.addEventListener('click', () => {
                  props.command({ id: item.id });
                });
                popup.appendChild(button);
              });
            },
            onExit: () => {
              popup.remove();
            },
          }
        },
      },
    }),
  ],
});
```

### 2.1 Editor 객체 설정

`Editor` 객체는 Tiptap의 핵심으로, 이 예시에서는 `StarterKit`과 `Mention` 확장을 함께 사용하여 에디터를 구성합니다.

```javascript
const editor = new Editor({
  element: document.querySelector('#editor'),
  extensions: [StarterKit, Mention.configure({...})],
});
```

### 2.2 Mention 확장

`Mention` 확장은 사용자가 '@'와 같은 특정 문자를 입력할 때 해당 문자를 기준으로 사용자 목록을 필터링하여 제안을 표시합니다.

#### `items` 함수

`items` 함수는 현재 입력된 query를 기준으로 목록을 필터링합니다.

```javascript
items: (query) => {
  return [
    { id: '1', label: 'Alice' },
    { id: '2', label: 'Bob' },
    { id: '3', label: 'Charlie' },
  ].filter(item => item.label.toLowerCase().startsWith(query.toLowerCase()));
}
```

#### `render` 함수

`render` 함수는 제안 목록을 화면에 그리는 역할을 합니다. `onStart`, `onUpdate`, `onExit`와 같은 메서드를 통해 팝업의 상태를 관리할 수 있습니다.

```javascript
render: () => {
  let popup;

  return {
    onStart: props => {
      popup = document.createElement('div');
      popup.className = 'mention-popup';
      props.items.forEach(item => {
        const button = document.createElement('button');
        button.innerText = item.label;
        button.addEventListener('click', () => {
          props.command({ id: item.id });
        });
        popup.appendChild(button);
      });
      document.body.appendChild(popup);
    },
    onUpdate: props => {
      popup.innerHTML = '';
      props.items.forEach(item => {
        const button = document.createElement('button');
        button.innerText = item.label;
        button.addEventListener('click', () => {
          props.command({ id: item.id });
        });
        popup.appendChild(button);
      });
    },
    onExit: () => {
      popup.remove();
    },
  }
}
```

### 3. HTML 예시

에디터를 표시하기 위한 간단한 HTML은 다음과 같습니다.

```html
<div id="editor"></div>
```

### 4. 스타일링

Mention 팝업을 위한 간단한 스타일링을 추가할 수 있습니다.

```css
.mention-popup {
  background-color: white;
  border: 1px solid #ccc;
  position: absolute;
  z-index: 1000;
  padding: 10px;
}

.mention-popup button {
  display: block;
  width: 100%;
  padding: 5px;
  text-align: left;
  border: none;
  background: none;
}
```

## 5. 결론

