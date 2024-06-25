#강의노트  #개념 #일급객체 #클로저 #싱글턴
### Swift 함수 = 1급 객체
1. 변수 또는 상수에 함수를 담을 수 있음 
2. 인자로 함수를 전달할 수 있음
3. 반환값(Return Value)로 함수를 전달할 수 있음

⬇️⬇️⬇️⬇️⬇️⬇️
1. 변수 또는 상수에 `클로저`를 담을 수 있음
2. 인자로 `클로저`를 전달할 수 있음
3. 반환값(Return Value)로 `클로저`를를 전달할 수 있음

![[스크린샷 2024-06-24 오전 11.17.12.png]]
> 🤔 뭐가 문제??
> 지금 핸들러는 depth 가 한 단계 더 들어가있는 상태! 
> 함수가 끝나도 계속 실행할 수 있어야 하기 때문에!

![[스크린샷 2024-06-24 오전 11.25.35.png]]
- `self` 를 쓰면서 나 탈출해서도 계속 이 작업을 마쳐줘! 정도로 이해하면 됨
![[스크린샷 2024-06-24 오전 11.30.00.png]]

```swift
class ViewController: UIViewController {

    override func viewDidLoad() {
        super.viewDidLoad()
        view.backgroundColor = .white
        // showAlert(title: "테스트", message: "테스트함다")
        // viewDidLoad() 에서 Alert X
        
    }
    
    override func viewDidAppear(_ animated: Bool) {
        super.viewDidAppear(animated)
        showAlert(title: "테스트", message: "저장저장?", ok: "저장") {
            print("저장되었슈")
        }
        
        showAlert2(title: "테스트", message: "저장저장?", ok: "저장") { _ in
            print("저장 2222")
        }
        
        // {_ in 의 기능이 밖으로 나옴!
    }
}
```


---
#### 오늘 정리할 것
- [ ] 뷰의 생명주기
- [ ] 일급 객체 함수
- [x] 과제 : recap => alert
- [x] 과제 : recap network => try
- [ ] 과제 : tmdb 도..
	- [ ] 추천 api =>