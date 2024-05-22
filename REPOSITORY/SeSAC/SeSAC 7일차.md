
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