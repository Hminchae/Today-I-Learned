#UIToolBar #Observable #값전달 #Animation #MethodDispatch 

![[스크린샷 2024-07-15 오전 9.46.31.png]]
![[스크린샷 2024-07-15 오전 9.47.12.png]]![[스크린샷 2024-07-15 오전 9.57.54.png]]


### 바로 실행되는 문제를 어떻게 해결할까
- Observable 클래스에 bind 매서드 안에 closure(value)를 포함한다면 인스턴스가 초기화되면서 화면이 바로 전환되는 문제가 있음
- 해결하기 위해서 Observable 안에 즉시실행/실행X bind 매서드를 두거나
- bind 매서드 안에 첫실행이냐를 받아오는 bool 값을 받거나
- 화면전환을 시켜주는 vc 의  output 값을 지켜보고 있는 코드에 data 가 nil 이면 early exit 하는 guard 문을 넣어주는 방법이 있음

## Animation

![[스크린샷 2024-07-15 오전 11.14.48.png]]
- Scale 키우기
- Rotate
- Translate 등 
#### Options
> 배열 형태 O 
> `UIView.animate(withDuration: 5, delay: 1, options: [.curveEaseInOut, .repeat ])`
![[스크린샷 2024-07-15 오전 11.23.26.png]]

```swift
    func animationImageView() {
        UIView.animate(withDuration: 5, delay: 1, options: .allowUserInteraction) { // ⬅️ delay : 애니메이션 언제 시작할지 딜레이를 줄 수 있음, 💡 options : 다양한 설정
            self.signUpLabel.alpha = 1 // ⬅️ 시간에 비례해서 점점 진해진다.
        }
    }
```

## Method Dispatch
> 최적화 함수 실행이 컴파일, 런타임에 정해지는지에 대한 차이
> 