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

![[스크린샷 2024-06-25 오전 10.59.52.png]]
> 정적 프레임워크?
> snapkit 같은 경우 계속 import 를 안 해줘도 계속계속 사용이 가능하다!
> 어떤 방법이 좋을지? 어떻게 구성되어있는건지 ?

```swift
import UIKit.UILabel
import UIKit.UISearchBar // -> 어차피 이렇게 써도 UIKit 전체가 import 되는 것 과 동일함
```

> 인스턴스 생성 클로저와 viewDidLoad 중 뭐가 먼저 실행될까?? ⬇️

```swift
// 뷰컨트롤러 인스턴스 생성 전에 클로저가 먼저 실행이 된다.
    var resultLabel = {
        let view = UILabel()
        view.textAlignment = .center
        view.numberOfLines = 0
        view.text = "검색 결과가 없습니다."
        print("이이잉 ?")
        return view
    }()
```
 ![[스크린샷 2024-06-25 오전 11.16.36.png]]
#### 뷰를 만들어 VC를 정리하기

> 뷰를 만들어 쓰면 vc가 깔끔해지지만...
> 🚨🚨
> delegate를 View에서 채택하고 사용해도 상관없지만, 버튼 클릭 등 뭔가 화면 전환이 이루어지는 상황이나 토스트뷰 등 transition 이 일어나는 일들은 View 가 일을 못해줘요..😵

```swift
class SearchViewController: BaseViewController {
    
    let mainView = SearchView()
    
    //⬇️viewDidLoad보다 먼저 실행됨
    //loadView: 뷰컨트롤러의 루트뷰를 생성해주는 기능
    //super.loadView()절대 호출하지 말아야 함 ❌
    override func loadView() {
        print(#function)
        view = mainView
    }
    
    override func viewDidLoad() {
        super.viewDidLoad()
        print(#function)

    }
}
```

#### GCD

---
### 정리

---
### 복습할 것



