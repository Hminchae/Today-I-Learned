
#### defer Statement

- `defer Statement` 는 함수 안에 작성 되는 `non-escaping closure`이며 함수 작성된 위치와 상관없이 함수가 종료되기 직전에 실행 되는 구문
- `defer` 구문은 후 처리 방식을 할 때 사용되며 함수 scpoe 범위 내에서 가장 마지막에 실행이 된다.
- `defer` 구문을 중첩으로 사용 할 수 있으며 `LIFO` 형식으로 가장 마지막에 있는 `defer` 가 먼저 실행되고 가장 처음에 있는 `defer` 가 마지막에 실행됨
- `defer` 구문 내부에는 `break`, `return`, `throw` 등과 같이 구문을 빠져나갈 수 있는 코드 또는 오류를 던지는 코드를 작성하면 오류를 발생됨


```swift
func sayNumber() {
    defer {
        print("print check : 1")
    }
    print("print check : 2")
}

// print check : 2
// print check : 1

func sayCheckNumber() {
    defer {
        for i in 0..<5 {
            print("for loop check : \(i)")
        }
    }
    print("print check : 5")
}

// print check : 5
// for loop check : 0
// for loop check : 1
// for loop check : 2
// for loop check : 3
// for loop check : 4


func sayNestedNumber() {
    defer {
        print("print check : 1")
    }
    
    defer {
        print("print check : 2")
    }
    
    defer {
        print("print check : 3")
    }
    print("print check : 4")
}


// print check : 4
// print check : 3
// print check : 2
// print check : 1
```

#### defer가 호출되는 순서

- 함수 내에 한 개 있을 때
    - 함수의 가장 마지막에 실행된다.

```swift
func test() {
    print("First print")
    
    defer { print("!!defer!!")}
    
    print("Second print")
}
test()

/* 결과
First print
Second print
!!defer!
*/
```

- 함수 내에 defer가 여러 개 있을 때
    - 끝에 있는 defer 부터 실행된다(LIFO)

```swift
func test2() {
    defer { print("1st defer - first") }
    defer { print("2nd defer") }
    defer { print("3rd defer - last") }
}
test2()

/* 결과
3rd defer - last
2nd defer
1st defer - first
*/
```

- defer가 중첩되어 있을 때
    - 가장 바깥 쪽에 있는 defer가 가장 먼저 실행된다.

```swift
func test3() {
    defer {
        defer {
            defer {
                print("1st defer - inner")
            }
            print("2nd defer")
        }
        print("3rd defer - outer")
    }
}
test3()

/* 결과
3rd defer - outer
2nd defer
1st defer - inner
*/
```

#### defer가 호출되지 않는 경우

- defer 를 읽기 전에 함수가 종료될 때

```swift
func test4() {
    print("1st print")
    return
    
    defer { print("defer~~") }
    
    print("2nd print")
}
test4()

/* 결과
1st print
*/
```

- throw를 이용해서 오류를 던질 경우
- guard문을 사용하여 중간에 함수를 종료하는 경우
- 함수의 리턴값이 Never(비반환함수)인 경우

#### defer를 사용하는 경우

- 함수가 종료하기 직전에 정리해야할 변수나, 상수를 처리해야할 용도로 사용한다.
- `defer` 는 `NSLock` 클래스를 통해 멀티 스레딩 환경에서 `Thread-Safe` 하게 작업을 할 수 있도록 도와주며 `deadlock` 을 방지 할 수 있기 때문에 함수 종료 직전에 DB 등을 닫아주는 용도로 사용하면 보장을 받을 수 있다.
