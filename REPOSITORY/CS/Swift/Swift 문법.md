#where 

```swift
 for i in 1...n where i % 2 == 0 {
        result += i
    }
```

- for 문에서 조건문을 추가할 때 where 사용할 수 있음

#filter #reduce

```swift
func solution(_ n: Int) -> Int { (0...n).filter { $0 % 2 == 0 }.reduce(0, +) }
```

#map #배열자르기

```swift
// numbers 라는 배열을 원하는 인덱스만큼 자르는 방법
func solution(_ numbers:[Int], _ num1:Int, _ num2:Int) -> [Int] {
    return (num1...num2).map{numbers[$0]}
}
```

#enumerated #map #배열자르기

```swift
// numbers 라는 배열을 원하는 인덱스만큼 자르는 방법
numbers.enumerated().filter {
        $0.offset >= num1 && $0.offset <= num2
    }.map {
        result.append($0.element)
    }
```

#배열자르기

```swift
Array(numbers[num1...num2]) 
```

