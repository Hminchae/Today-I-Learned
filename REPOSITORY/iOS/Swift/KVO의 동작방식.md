# 1. iOS에서 KVO란 무엇입니까? 
#### KVO 이란?

- 객체의 프로퍼티의 변경사항을 다른 객체에 알리기 위해 사용하는 코코아 터치 프로그래밍 패턴
- Model과 View와 같이 논리적으로 분리된 파트간의 변경사항을 전달하는데 유용하다.
- `NSObject`를 상속한 클래스에서만 `KVO` 를 사용 할 수 있다.

#### KVO 사용 방법

- Observing이 필요한 객체에게 `NSObject`를 상속 받도록 한다.
- Observing 하려는 `Property`에 `@objc` 속성과, `dynamic` 키워드를 부여한다.
- key Path를 사용하여 `observe(_:options:changeHandler:)`를 호출하여 Observing을 수행한다.

```swift
class Person: NSObject {
    
    let name: String
    @objc dynamic var age: Int
    @objc dynamic var car: String = "BMW"
    
    init(name: String, age: Int, car: String) {
        self.name = name
        self.age = age
        self.car = car
    }
    
}

var jenny: Person = Person(name: "jenny", age: 20, car: "아반떼")

jenny.observe(\.car, options: [.old, .new, .initial, .prior]) { (object, change) in
    print("\(object.name)의 차가 \(change.oldValue) 에서 \(change.newValue)로 바꿨다. ")
}

jenny.observe(\.age, options: [.old, .new]) { (object, change) in
    print("\(object.name) 나이가 \(change.oldValue) 에서 \(change.newValue) 로 변경 되었다. ")
}



jenny.age = 24
jenny.age = 30

jenny.car = "K3"


```

#### KVO Options

- **old** : 변경 전 값이 반환된다.
- **new** : 변경 후 값이 반환된다.
- **initial** : 초기화값에 대한 값을 반환된다.
- **prior** : 변경 전,후 상태 모두 파악하여 반환된다.

#### KVO 장점

- 두 객체간의 동기화, Model과 View  같이 분리된 파트간의 변경사항을 전달 가능하게 한다.
- 프로퍼티의 값 번경 전(`old Value`), 변경 후(`new Value`) 를 관찰 할 수 있다.

#### KVO 단점

- Objective-C 런타임에 의존적이며 `dynamic` 키워드로 인해 dynamic Dispatch로 활성화 하게 된다.
- `NSObject`를 상속한 `class` 에서만 사용이 가능하다.

# 2. iOS의 KVC란 무엇입니까?
# 3.  iOS에서 KVO와 KVC의 차이점은 무엇입니까?






#### 📝 참고 사이트

- [Using Key-Value Observing in Swift](https://developer.apple.com/documentation/swift/using-key-value-observing-in-swift)
- [zeddios](https://zeddios.tistory.com/1220)
- [[iOS - swift] KVO(Key-Value Observing)](https://ios-development.tistory.com/366)


