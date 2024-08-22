# 웹 개발 학습 내용 정리

이 문서는 React와 FastAPI를 사용한 웹 개발 과정에서 학습한 주요 개념들을 정리한 것입니다.

## React

### 1. 컴포넌트 기반 구조
React의 핵심은 재사용 가능한 컴포넌트입니다.

```jsx
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}
```

### 2. JSX
JavaScript를 확장한 문법으로, React 엘리먼트를 생성합니다.

```jsx
const element = <h1>Hello, world!</h1>;
```

### 3. Props와 State
- Props: 부모 컴포넌트로부터 자식 컴포넌트로 데이터를 전달합니다.
- State: 컴포넌트 내부에서 관리되는 데이터입니다.

```jsx
function Counter() {
  const [count, setCount] = useState(0);
  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}
```

### 4. Hooks
함수형 컴포넌트에서 상태 관리와 생명주기 기능을 사용할 수 있게 해줍니다.

- useState: 상태 관리
- useEffect: 부수 효과 처리
- useContext: Context API 사용
- useReducer: 복잡한 상태 로직 관리

### 5. 라우팅 (React Router)
싱글 페이지 애플리케이션(SPA)에서 페이지 전환을 관리합니다.

```jsx
import { BrowserRouter as Router, Route, Switch } from 'react-router-dom';

function App() {
  return (
    <Router>
      <Switch>
        <Route path="/" exact component={Home} />
        <Route path="/about" component={About} />
      </Switch>
    </Router>
  );
}
```

## FastAPI

### 1. 경로 작업 선언
HTTP 메서드와 URL 경로를 정의합니다.

```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
async def root():
    return {"message": "Hello World"}
```

### 2. 요청 본문
Pydantic 모델을 사용하여 요청 데이터를 검증합니다.

```python
from pydantic import BaseModel

class Item(BaseModel):
    name: str
    price: float

@app.post("/items")
async def create_item(item: Item):
    return item
```

### 3. 쿼리 매개변수
URL의 쿼리 매개변수를 함수 매개변수로 받습니다.

```python
@app.get("/items")
async def read_item(skip: int = 0, limit: int = 10):
    return {"skip": skip, "limit": limit}
```

### 4. 의존성 주입
재사용 가능한 로직을 의존성으로 정의합니다.

```python
from fastapi import Depends

async def common_parameters(q: str = None, skip: int = 0, limit: int = 100):
    return {"q": q, "skip": skip, "limit": limit}

@app.get("/items/")
async def read_items(commons: dict = Depends(common_parameters)):
    return commons
```

## 일반적인 웹 개발 개념

### 1. 상태 관리
애플리케이션의 데이터 흐름을 관리합니다. React에서는 useState, useReducer, 또는 Redux 같은 라이브러리를 사용합니다.

### 2. 비동기 프로그래밍
서버와의 통신 등 시간이 걸리는 작업을 처리합니다.

```javascript
async function fetchData() {
  try {
    const response = await fetch('https://api.example.com/data');
    const data = await response.json();
    return data;
  } catch (error) {
    console.error('Error:', error);
  }
}
```

### 3. RESTful API 설계
리소스 중심의 API 설계 방식을 학습했습니다.

### 4. 인증과 인가
JWT(JSON Web Tokens)를 이용한 사용자 인증 방식을 이해했습니다.

### 5. CORS (Cross-Origin Resource Sharing)
다른 출처의 리소스를 공유할 수 있게 하는 메커니즘입니다.

```python
from fastapi.middleware.cors import CORSMiddleware

app.add_middleware(
    CORSMiddleware,
    allow_origins=["http://localhost:3000"],
    allow_credentials=True,
    allow_methods=["*"],
    allow_headers=["*"],
)
```

### 6. 데이터베이스 연동
ORM(Object-Relational Mapping)을 사용한 데이터베이스 조작 방법을 학습했습니다.

### 7. 배포 및 CI/CD
Docker를 이용한 컨테이너화와 GitHub Actions를 통한 CI/CD 파이프라인 구축 방법을 익혔습니다.

## 학습 후기

이러한 개념들을 학습하면서 프론트엔드와 백엔드의 상호작용, 그리고 전체 웹 애플리케이션의 구조에 대한 이해도가 크게 향상되었습니다. 특히 React의 컴포넌트 기반 구조와 FastAPI의 직관적인 API 설계 방식이 효율적인 개발을 가능하게 한다는 점을 체감했습니다.

앞으로는 이러한 기본 개념을 바탕으로 더 복잡한 애플리케이션을 구현하고, 성능 최적화와 보안 강화에 중점을 두어 학습을 이어나갈 계획입니다.
