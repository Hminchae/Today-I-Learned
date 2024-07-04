#네트워크 

##### 프로젝트 시작부터 Codebase로
`SceneDelegate`의 `willConnectTo`가 첫 진입점을 담당
`UIWindow` = 내가 보는 그 화면

#### 네트워크
- 클라 -> 서버 : Encoding
- 서버 -> 클라 : Decoding

##### self

##### 함수 순서
```swift
class MarketViewController: UIViewController {

    override func viewDidLoad() {
        super.viewDidLoad()

        print(#function, "1111")
        callRequest()
        print(#function, "2222")
    }
    
    func callRequest() {
        print(#function, "3333")
        print(#function, "4444")
    }
}
```

viewDidLoad() 1111
callRequest() 3333
callRequest() 4444
viewDidLoad() 2222


```swift
    override func awakeFromNib() {
        super.awakeFromNib()
        // Initialization code
    }
```

=> 이거 무슨 용도? 
: 변경되지 않는 셋업(초기화)


```swift

```

viewDidLoad() 1111
callRequest() 3333
callRequest() 4444
viewDidLoad() 2222
tableView(_:numberOfRowsInSection:) 0
tableView(_:numberOfRowsInSection:) 0
tableView(_:numberOfRowsInSection:) 0
tableView(_:numberOfRowsInSection:) 0
SUCCESS
tableView(_:numberOfRowsInSection:) 326


1. Req - Res
2. GET, POST, PUT, DELETE
3. 인증키 
	3.1. 헉 제한 ⬆️? -> 과금
4. 그래서 깃 이그노어 처리..
![[스크린샷 2024-06-05 오후 12.33.58.png]]