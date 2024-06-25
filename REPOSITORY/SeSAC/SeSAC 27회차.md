#강의노트 #BaseVC #BaseView #DispatchGroup #TV/CV #Network

### 강의내용
#### 1. BaseVC 쓰는법
UIVC -> BaseVC -> TargetVC

![[스크린샷 2024-06-25 오전 10.00.08.png]]

|                                      |                                      |
| ------------------------------------ | ------------------------------------ |
| ![[스크린샷 2024-06-25 오전 10.04.17.png]] | ![[스크린샷 2024-06-25 오전 10.05.49.png]] |
```swift
override func configureView() {
        super.configureView() <- 🚨 이거 호출하지 않으면 BaseVC의 configureView가 호출 X
        print("VC", #function)
    }
```

> super.configureView() <- 🚨 이거 호출하지 않으면 BaseVC의 configureView가 호출 X

```swift
 @available(*, unavailable) <- 
    required init?(coder: NSCoder) {
        fatalError("init(coder:) has not been implemented")
    }
```

>  @available(*, unavailable) ?? 

UIVC -> BaseVC -> BaseToastVC, BaseAlertVC 등등..이 가능 

#### 2. ? 쓰는법

---
### 정리

---
### 복습할 것

