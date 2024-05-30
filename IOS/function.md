

```markdown
# Today I Learned

## Swift: Functions

### 1. 함수 정의와 호출

#### 함수 정의
- Swift에서 함수는 `func` 키워드를 사용하여 정의합니다.
- 함수는 이름, 매개변수 목록, 반환 타입, 그리고 코드 블록으로 구성됩니다.

```swift
func greet(person: String) -> String {
    let greeting = "Hello, \(person)!"
    return greeting
}
```

#### 함수 호출
- 함수를 호출할 때는 함수 이름과 매개변수를 사용합니다.

```swift
let greetingMessage = greet(person: "John")
print(greetingMessage)  // "Hello, John!"
```

### 2. 매개변수와 반환값

#### 매개변수
- 함수는 매개변수를 가질 수 있으며, 매개변수는 함수 내부에서 상수로 취급됩니다.
- 매개변수에는 기본값을 설정할 수 있습니다.

```swift
func greet(person: String, from hometown: String = "Unknown") -> String {
    return "Hello, \(person)! Glad you could visit from \(hometown)."
}
```

#### 반환값
- 함수는 반환 타입을 가질 수 있으며, `->` 키워드를 사용하여 반환 타입을 명시합니다.
- 반환값이 없는 함수는 `Void`를 반환하거나, 반환 타입을 생략할 수 있습니다.

```swift
func sayHelloWorld() -> String {
    return "Hello, world!"
}

func printHelloWorld() {
    print("Hello, world!")
}
```

### 3. 다양한 함수 기능

#### 다중 반환값
- Swift 함수는 튜플을 사용하여 여러 값을 반환할 수 있습니다.

```swift
func minMax(array: [Int]) -> (min: Int, max: Int)? {
    guard let minValue = array.min(), let maxValue = array.max() else {
        return nil
    }
    return (minValue, maxValue)
}

if let bounds = minMax(array: [8, -6, 2, 109, 3, 71]) {
    print("min is \(bounds.min) and max is \(bounds.max)")
}
```

#### 인자 레이블과 아규먼트 레이블
- 함수의 매개변수는 인자 레이블(argument label)과 파라미터 이름(parameter name)을 가질 수 있습니다.

```swift
func greet(person: String, from hometown: String) -> String {
    return "Hello, \(person)! Glad you could visit from \(hometown)."
}

print(greet(person: "Bill", from: "Cupertino"))
```

#### 가변 매개변수
- 함수는 가변 매개변수를 가질 수 있으며, 가변 매개변수는 함수 호출 시 여러 값을 받을 수 있습니다.

```swift
func arithmeticMean(_ numbers: Double...) -> Double {
    var total: Double = 0
    for number in numbers {
        total += number
    }
    return total / Double(numbers.count)
}

print(arithmeticMean(1, 2, 3, 4, 5))  // 3.0
print(arithmeticMean(3, 8.25, 18.75))  // 10.0
```

### 4. 중첩 함수
- 함수는 다른 함수의 내부에 정의될 수 있으며, 이를 중첩 함수라고 합니다.

```swift
func chooseStepFunction(backward: Bool) -> (Int) -> Int {
    func stepForward(_ input: Int) -> Int { return input + 1 }
    func stepBackward(_ input: Int) -> Int { return input - 1 }
    return backward ? stepBackward : stepForward
}

var currentValue = 3
let moveNearerToZero = chooseStepFunction(backward: currentValue > 0)
// moveNearerToZero는 이제 stepBackward() 함수를 가리킵니다.

print("Counting to zero:")
while currentValue != 0 {
    print("\(currentValue)... ")
    currentValue = moveNearerToZero(currentValue)
}
print("zero!")
```

이제 모든 내용이 코드 블록 안에 포함되어 있습니다. 이 마크다운 파일을 그대로 복사하여 사용하시면 됩니다.
```
