### Primary Key

**Primary Key**는 데이터베이스 테이블에서 각 레코드를 고유하게 식별하는 데 사용되는 컬럼 또는 컬럼들의 집합입니다. Primary Key는 데이터베이스 설계에서 매우 중요한 역할을 하며, 다음과 같은 특징을 가집니다:

- **고유성 (Uniqueness)**: 테이블 내의 모든 레코드는 고유한 값을 가져야 합니다. 즉, 동일한 Primary Key 값을 가진 두 개의 레코드는 존재할 수 없습니다.
- **NULL 불허 (Not Null)**: Primary Key는 NULL 값을 가질 수 없습니다. 이는 각 레코드를 고유하게 식별해야 하기 때문입니다.
- **단일 열 또는 다중 열 (Single or Composite Key)**: Primary Key는 하나의 컬럼으로 구성될 수도 있고, 여러 컬럼의 조합으로 구성될 수도 있습니다. 여러 컬럼으로 구성된 Primary Key를 복합 키(Composite Key)라고 합니다.

#### 예제

다음은 `users` 테이블의 예입니다. 이 테이블에서는 `id` 컬럼이 Primary Key로 설정되어 있습니다.

```sql
CREATE TABLE users (
    id INT PRIMARY KEY,
    username VARCHAR(50) NOT NULL,
    email VARCHAR(100) NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

이 예제에서:

- `id` 컬럼은 각 사용자 레코드를 고유하게 식별합니다.
- `username` 및 `email` 컬럼은 사용자의 추가 정보를 저장합니다.
- `created_at` 컬럼은 사용자 레코드가 생성된 시간을 저장합니다.

#### 복합 키 예제

다음은 `orders` 테이블의 예입니다. 이 테이블에서는 `order_id`와 `product_id` 컬럼의 조합이 Primary Key로 설정되어 있습니다.

```sql
CREATE TABLE orders (
    order_id INT,
    product_id INT,
    quantity INT,
    PRIMARY KEY (order_id, product_id)
);
```

이 예제에서:

- `order_id`와 `product_id`의 조합이 각 주문 레코드를 고유하게 식별합니다.
- 동일한 `order_id`에 대해 여러 `product_id`를 가질 수 있지만, 동일한 `order_id`와 `product_id` 조합은 중복될 수 없습니다.

Primary Key는 데이터 무결성을 유지하고 테이블 내의 각 레코드를 빠르게 조회하는 데 중요한 역할을 합니다. 이를 통해 데이터베이스의 성능을 최적화하고, 데이터를 효과적으로 관리할 수 있습니다.