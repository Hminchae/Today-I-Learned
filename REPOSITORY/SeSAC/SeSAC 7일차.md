
#### BreakPoint
#LLVM #LLDB


#### Opensource License 
> 어떻게 찾아요?

swift + github + calendar


> 어떻게 활용해요?

- 코코아팟 : 서포트 좋음 빌드 스피드 떨어짐
- 카르타고 : 빌드 스피드 좋으나 서포트 떨어짐 
- SPM : 애플 상승 서포트 떨어짐
- Manually : 수동 관리 
-> 의존성 관리 도구 

>시멘틱 버저닝 ?
>3.8.5 | 3은 메이저 8은 마이너  5는 patch


#### 클래스
- 멤버
	- 클래스안의 함수 : 메서드
	- 클래스 안의 변수 : 프로퍼티
```swift
import UIKit

var greeting = "Hello, playground"



var list = ["오밥", "선식당", "유미카츠"]
var list2 = ["456-789", "345-384", "3423-2987"]

list[0]
list2[0]


class Monster {
    var clothes: String // 인스턴스 프로퍼티
    var speed: Int
    var power: Int
    var exp : Int
    
    func a(power: Int) { // 인스턴스 메서드
        self.power = power
    }
    
    init(clothes: String, speed: Int, power: Int, exp: Int) {
        self.clothes = clothes
        self.speed = speed
        self.power = power
        self.exp = exp
    }
}

// 클래스를 메모리에 올리는 과정
// easy, normal, hard 이라는 인스턴스를 만드는 과정
let easy = Monster(clothes: "Orange", speed: 1, power: 1, exp: 1)
easy.speed
easy.exp
let normal = Monster(clothes: "Blue", speed: 10, power: 10, exp: 10)
normal.power
let hard = Monster(clothes: "gray", speed: 100, power: 100, exp: 100)





```

> 왜? struct 는 멤버와이즈 이니셜라이징을 지원하는데, class 는 왜 안 쓰는것인가? 
### 객체지향 프로그래밍_상속

> UIVC 에서 ViewDidLoad 는 항상 오버라이딩
> super.viewDidLoad **** 중요


오버라이딩이 뭔지, 초기화를 왜 해야하는지 


### Class 와 Struct
- Class
	- 상속가능
	- UIKit
- Struct
	- 상속불가능
	- SwiftUI, Swift


### Saving Data

- UserDefaults
	- 단일 데이터 값(경량) : 자동 록인 여부, 알림 수신 여부, 인앱 결제 엽 이메일, 닉네임, 성별 등 간단한 사용자 기본 설정 앱 테마, 앱 첫 실행, 팝업 다시 보지 않기 등
	- **단일 데이터 값, 자동 록인 여부, 알림 수신 여부, 닉네임 성별 등 간단한 사용자 기본 설정 앱 테마, 앱실행,**
	- iOS SandBox system

- DataBase




Emotion -> 횟수 + 리셋
BMI -> 키/몸무게
신조어검색기 -> 검색 내역 저장