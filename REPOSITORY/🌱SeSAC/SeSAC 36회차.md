### 어제의 복습
```swift
    struct Input {
        // 처음에 로드
        var inputViewDidLoadTrigger: Observable<Void?> = Observable(nil)
        var inputAddButtonTapped: Observable<Void?> = Observable(nil)
        // 전체 삭제
        var inputRemoveButtonTapped: Observable<Void?> = Observable(nil)
    }
```

-> 프로퍼티가 너무 많아지면 struct 를 통해 묶을  수 도 있다. 