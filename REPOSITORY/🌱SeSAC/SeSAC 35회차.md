#MVVM 

### MVC 패턴

![[스크린샷 2024-07-09 오후 9.42.20.png]]
- 모델과 뷰는 엄격하게 분리되어 있는 상태
- 모든건 VC가 담당

### MVVM 패턴
> 💡중요한건?
> 비즈니스 로직을 어떤 기준으로?


![[스크린샷 2024-07-09 오후 9.03.25.png]]

1 ~ 5를 뷰모델로 옮겨보자

#### 뷰모델 분리 전략
- VC 에서 UIKit 을 import 하지 않아도 문제가 생기지 않는 친구들을  데려가자
- 데이터의 가공하는 부분은 뷰모델로 빼보자
- ![[스크린샷 2024-07-09 오후 10.00.17.png]]
- 사용자가 클릭하는 모든 것 : input 으로


#### 
```swift
class Person {
    
    var closure = {
        print("이름 바뀜")
    }
    var name: String {
        didSet {
            closure() // <- 일급객체의 속성
        }
    }
    
    init(_ name: String) {
        self.name = name
    }
}
```
![[스크린샷 2024-07-09 오후 10.32.35.png]]


```swift

import Foundation

final class LoginViewModel {
    // 실시간으로 달라지는 데이터를 감지
    var inputId: String? {
        didSet {
            validation()
        }
    }
    var inputPassword: String? {
        didSet {
            validation()
        }
    }
    
    private(set) var outputValid = false
    private(set) var outputValidationText = ""
    
    private func validation() {
        guard let id = inputId, let pw = inputPassword else { return }
        
        if id.count >= 3 && pw.count > 5 {
            print("유효성 통과")
            outputValid = true
            outputValidationText = "통과"
        } else {
            print("유효성 검증 오류")
            outputValid = false
            outputValidationText = "이메일 3자, 비밀번호 5자 이상"
        }
     }
}
```



데이터의 가공은 뷰모델, 

>UserViewController

ViewDidLoad : input 