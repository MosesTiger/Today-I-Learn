
# PostgreSQL

## 개요

PostgreSQL는 객체-관계형 데이터베이스 관리 시스템(ORDBMS)으로, 높은 확장성과 SQL 준수성을 제공합니다. 오픈 소스 프로젝트로서, 여러 기능과 성능 최적화를 통해 데이터베이스의 안정성과 효율성을 보장합니다.

## 특징

- **오픈 소스**: PostgreSQL는 오픈 소스 라이선스 하에 배포되어 누구나 자유롭게 사용할 수 있습니다.
- **확장성**: 다양한 데이터 타입, 인덱스, 함수 등을 사용자 정의로 추가할 수 있습니다.
- **표준 준수**: SQL 표준을 준수하여 높은 호환성을 제공합니다.
- **고가용성**: 리플리케이션과 클러스터링을 통해 고가용성을 보장합니다.
- **보안**: 다양한 인증 메커니즘과 권한 관리 기능을 제공합니다.

## 설치

### Linux

1. 패키지 관리자를 통해 PostgreSQL를 설치합니다.

    ```bash
    sudo apt-get update
    sudo apt-get install postgresql postgresql-contrib
    ```

2. PostgreSQL 서비스를 시작합니다.

    ```bash
    sudo systemctl start postgresql
    ```

3. PostgreSQL 서비스를 부팅 시 자동으로 시작하도록 설정합니다.

    ```bash
    sudo systemctl enable postgresql
    ```

### Windows

1. [PostgreSQL 공식 웹사이트](https://www.postgresql.org/download/windows/)에서 Windows용 설치 파일을 다운로드합니다.
2. 설치 파일을 실행하고, 설치 마법사의 지시에 따라 PostgreSQL를 설치합니다.

## 기본 사용법

### 데이터베이스 생성

1. PostgreSQL에 접속합니다.

    ```bash
    sudo -i -u postgres
    psql
    ```

2. 데이터베이스를 생성합니다.

    ```sql
    CREATE DATABASE mydatabase;
    ```

3. 데이터베이스 목록을 확인합니다.

    ```sql
    \l
    ```

### 테이블 생성

1. 데이터베이스에 접속합니다.

    ```bash
    psql -d mydatabase
    ```

2. 테이블을 생성합니다.

    ```sql
    CREATE TABLE users (
        id SERIAL PRIMARY KEY,
        name VARCHAR(100),
        age INT
    );
    ```

3. 테이블 목록을 확인합니다.

    ```sql
    \dt
    ```

### 데이터 삽입

1. 데이터를 삽입합니다.

    ```sql
    INSERT INTO users (name, age) VALUES ('Alice', 30);
    INSERT INTO users (name, age) VALUES ('Bob', 25);
    ```

2. 데이터를 조회합니다.

    ```sql
    SELECT * FROM users;
    ```

## 고급 기능

### 트랜잭션

PostgreSQL는 ACID 속성을 준수하는 트랜잭션을 지원합니다.

```sql
BEGIN;
UPDATE accounts SET balance = balance - 100 WHERE name = 'Alice';
UPDATE accounts SET balance = balance + 100 WHERE name = 'Bob';
COMMIT;
```

### 인덱스

인덱스를 생성하여 조회 성능을 향상시킬 수 있습니다.

```sql
CREATE INDEX idx_users_name ON users (name);
```

### 뷰

뷰를 생성하여 복잡한 쿼리를 단순화할 수 있습니다.

```sql
CREATE VIEW user_names AS
SELECT name FROM users;
```

## 참고 자료

- [PostgreSQL 공식 문서](https://www.postgresql.org/docs/)
- [PostgreSQL 튜토리얼](https://www.postgresqltutorial.com/)
- [PostgreSQL GitHub 저장소](https://github.com/postgres/postgres)

