#강의노트 #새싹 #함수

### 함수
#### - 함수 by 애플

= viewDidLoad 같이..
함수의 이름, 기능,  언제 실행 타이밍 미리 정의
#### - 함수 by 직접

= UDF : User Defined Function
함수의 이름, 기능, 실행 타이밍 직접 정의 해주어야 함 

@IBAction => 함수의 이름, 기능, 실행 타이밍 직접 정의 해주어

```swift
designLabelUI(oneLabel) // () <- 함수 호출 연산자
```

##### 매개변수(parameter)

```swift
func designLabelUI(_ labelName: UILabel, thisIsColorForLabelText textColor: UIColor) {
        labelName.text = "0"
        labelName.textColor = textColor
        labelName.font = .boldSystemFont(ofSize: 30)
        labelName.textAlignment = .center
    }
```

- `labelName` : 매개변수(parameter)
- `oneLabel`,`twoLabel` etc : 전달인자(Argument)
-  `thisIsColorForLabel` : 외부 매개변수(Argument Name)
-  `textColor` : 내부 매개변수(Parameter Name)
- `_ 외부매개변수` :  와일드카드 식별자

##### Alpha 와 Opacity
- Alpha : 하위뷰 까지 흐려짐
- Opacity
#### tap Gesture Recognizer 와 button 의 차이
- tap Gesture Recognizer
- UIPinch Gesture : 줌인 줌아웃
- UIRotationGesture : 회전
- UISwipeGesture
- UIPanGestureRecognizer : 막 휘두르기 (커스텀 영역과 가까움)
- UIScreenEdgePanRecognizer
- UILongPressGestureRecognizer 
- UIHoverGestureRecognizer : 마우스 올려두기

- User Interaction 을 받도록 하려면(버튼제외) : User Interaction Enabled 를 활성화 하여야 함
- 버튼과 달라서 Gesture는 하나씩

>뭐 안될때
>	- 연결관계
>	- 함수는 print를 해봐

##### Any ? 
Any를 사용하는 예 : 같은 액션을 다중 버튼 & 제스처가 담당할 때

### AutoLayout

> Tip
> 1. 하나씩 잡아본다
> 2. 한방향으로 잡는다(위 -> 아래, 아래 -> 위 )
> 3. clear Constraints
> 	1. 위 : 선택된거
> 	2. 아래 : 무조건 다 지워줌