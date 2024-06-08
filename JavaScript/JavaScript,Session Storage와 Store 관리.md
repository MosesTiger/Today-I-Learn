# Today I Learned

## JavaScript: Session Storage와 Store 관리

### 1. `sessionStorage`를 사용한 상태 관리

#### 목적
- 웹 페이지에서 세션 동안 데이터를 저장하고 유지하기 위해 사용합니다.
- 브라우저 탭을 닫으면 데이터가 사라집니다.

#### 주요 메서드
- `sessionStorage.setItem(key, value)`: 데이터를 저장합니다.
- `sessionStorage.getItem(key)`: 데이터를 가져옵니다.

### 2. JSON 변환

#### JSON.stringify
- JavaScript 객체를 JSON 문자열로 변환합니다.
- 주로 데이터를 저장하거나 전송할 때 사용합니다.

```javascript
const jsonString = JSON.stringify(store);
sessionStorage.setItem("store", jsonString);
```

#### JSON.parse
- JSON 문자열을 JavaScript 객체로 변환합니다.
- 주로 저장된 데이터를 다시 사용할 때 사용합니다.

```javascript
const storage = sessionStorage.getItem("store");
const jsonObject = JSON.parse(storage);
```

### 3. 객체 구조 분해 할당 (Destructuring Assignment)

#### 목적
- 객체의 여러 속성을 한 번에 추출하여 변수에 할당합니다.
- 코드가 더 간결하고 읽기 쉬워집니다.

#### 예시
```javascript
const { dateList, detailList, todayId, currentFunds, isFirstEdit } = JSON.parse(storage);
```

### 4. 함수 설명: `initStore`

#### 기능
- `sessionStorage`에서 `store` 데이터를 가져와 `store` 객체를 초기화합니다.
- 데이터가 없으면 `updateStorage`를 호출하여 초기 데이터를 저장합니다.

#### 코드
```javascript
function initStore() {
  // sessionStorage에서 'store' 키에 해당하는 값을 가져옵니다.
  const storage = sessionStorage.getItem("store");

  // 만약 저장된 데이터가 없다면, 초기 데이터를 sessionStorage에 저장합니다.
  if (!storage) updateStorage();

  // 저장된 데이터를 JSON 객체로 변환하고, 각 속성을 개별 변수로 추출합니다.
  const { dateList, detailList, todayId, currentFunds, isFirstEdit } = JSON.parse(storage);

  // 추출된 속성들을 store 객체의 속성으로 설정합니다.
  store.currentFunds = currentFunds;
  store.isFirstEdit = isFirstEdit;
  store.dateList = dateList;
  store.detailList = detailList;
  store.todayId = todayId;
}
```
