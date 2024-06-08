
# Car Entity Class 설명

이 문서는 Java Persistence API(JPA)를 사용하여 정의된 `Car` 엔티티 클래스를 설명합니다. 이 클래스는 데이터베이스의 `Car` 테이블과 매핑됩니다.

## 클래스 정의

```java
package com.packt.cardatabase.domain;

import javax.persistence.Entity;
import javax.persistence.FetchType;
import javax.persistence.GeneratedValue;
import javax.persistence.GenerationType;
import javax.persistence.Id;
import javax.persistence.JoinColumn;
import javax.persistence.ManyToOne;

@Entity
public class Car {
    @Id
    @GeneratedValue(strategy=GenerationType.AUTO)
    private long id;
    private String brand, model, color, registerNumber;
    @Column(name="`year`")
    private int year;
    private int price;
    
    public Car() {}
    
    public Car(String brand, String model, String color, 
            String registerNumber, int year, int price, Owner owner) {
        super();
        this.brand = brand;
        this.model = model;
        this.color = color;
        this.registerNumber = registerNumber;
        this.year = year;
        this.price = price;
        this.owner = owner;
    }

    @ManyToOne(fetch = FetchType.LAZY)
    @JoinColumn(name = "owner")
    private Owner owner;

    // Getter and setter methods

    public Owner getOwner() {
        return owner;
    }

    public void setOwner(Owner owner) {
        this.owner = owner;
    }
    
    public long getId() {
        return id;
    }

    public void setId(long id) {
        this.id = id;
    }

    public String getBrand() {
        return brand;
    }

    public void setBrand(String brand) {
        this.brand = brand;
    }

    public String getModel() {
        return model;
    }

    public void setModel(String model) {
        this.model = model;
    }

    public String getColor() {
        return color;
    }

    public void setColor(String color) {
        this.color = color;
    }

    public String getRegisterNumber() {
        return registerNumber;
    }

    public void setRegisterNumber(String registerNumber) {
        this.registerNumber = registerNumber;
    }

    public int getYear() {
        return year;
    }

    public void setYear(int year) {
        this.year = year;
    }

    public int getPrice() {
        return price;
    }

    public void setPrice(int price) {
        this.price = price;
    }
}
```

## 어노테이션 설명

### @Entity
- 클래스가 JPA 엔티티임을 나타냅니다. 데이터베이스의 `Car` 테이블에 매핑됩니다.

### @Id
- 엔티티의 기본 키 필드를 나타냅니다.

### @GeneratedValue(strategy=GenerationType.AUTO)
- 기본 키 값의 생성을 자동으로 처리합니다. 데이터베이스 벤더에 따라 자동으로 키 생성 전략을 선택합니다.

### @Column(name="`year`")
- 엔티티 필드와 데이터베이스 열을 매핑합니다. 열 이름이 `year`로 설정됩니다. 백틱(`) 문자를 사용하여 예약어를 피합니다.

### @ManyToOne(fetch = FetchType.LAZY)
- `Car` 엔티티와 `Owner` 엔티티 간의 다대일 관계를 정의합니다. 지연 로딩을 사용하여 필요할 때만 연관된 `Owner` 엔티티를 로드합니다.

### @JoinColumn(name = "owner")
- 외래 키 열을 매핑합니다. 이 열은 `owner`라는 이름을 가집니다.

## 생성자

### 기본 생성자
- 기본 생성자는 매개변수가 없습니다. JPA는 엔티티를 로드할 때 기본 생성자를 사용합니다.

### 매개변수가 있는 생성자
- 이 생성자는 모든 필드를 초기화합니다. 새로운 `Car` 객체를 생성할 때 사용됩니다.

## 필드 및 접근자 메서드

### 필드
- `id`: 기본 키 필드입니다.
- `brand`, `model`, `color`, `registerNumber`: 자동차의 속성을 나타내는 필드입니다.
- `year`: 자동차의 제작 연도를 나타내는 필드입니다.
- `price`: 자동차의 가격을 나타내는 필드입니다.
- `owner`: 자동차의 소유자를 나타내는 필드입니다. `Owner` 엔티티와 다대일 관계를 가집니다.

### 접근자 메서드 (Getter and Setter)
- 각 필드에 대한 Getter와 Setter 메서드를 통해 필드의 값을 읽고 쓸 수 있습니다.
- 예를 들어, `getBrand` 메서드는 `brand` 필드의 값을 반환하고, `setBrand` 메서드는 `brand` 필드의 값을 설정합니다.

## 결론
이 클래스는 JPA를 사용하여 데이터베이스와 상호작용하는 엔티티를 정의합니다. 이를 통해 `Car` 객체는 데이터베이스의 `Car` 테이블과 매핑되어 ORM(Object-Relational Mapping)을 가능하게 합니다. 이를 통해 데이터베이스 연산을 객체 지향적으로 처리할 수 있습니다.


