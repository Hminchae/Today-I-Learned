#### 코드로 UI 구성하기
- 뷰 객체 프로퍼티 선언
- `ViewDidLoad`에서 `addsubView`
##### Autoresizing Mask 
> 동적인 레이아웃을 구성할 수 있도록 Apple 이 도입한 예전방식의 기능. 부모뷰가 커지거나 작아짐에 따라 서브뷰의 크기나 의치를 조정하는 방식을 결정하게 되는 레이아웃

##### system Color ? -> 해당 모드에 어울리는 색으로 바뀜


| 네비게이션 컨트롤러 있을 때 뷰의 시작점                                             | 모달                                                                 | `toItem:view.safeAreaLayoutGuide`                                  | `NSLayoutConstraint`                                               |
| ------------------------------------------------------------------ | ------------------------------------------------------------------ | ------------------------------------------------------------------ | ------------------------------------------------------------------ |
| ![[Simulator Screenshot - iPhone 15 - 2024-06-04 at 10.36.17.png]] | ![[simulator_screenshot_A08C4628-AD7A-4124-8EBC-CDCE26CDFCB0.png]] | ![[simulator_screenshot_A9470665-F5FD-450F-B947-C5B206879F93.png]] | ![[simulator_screenshot_CD9022F2-F494-4F33-8D76-B3D8939EFAD7.png]] |
#### 스냅킷
[스냅킷 독](https://snapkit.github.io/SnapKit/docs/)

##### 오류
![[스크린샷 2024-06-04 오후 12.18.35.png]]
> addSubview 가 레이아웃보다 먼저 호출이 되어야 함

```swift
            make.width.equalTo(300)
            make.height.equalTo(300)
            와
            make.width.height.equalTo(300)
            와
            make.size.equalTo(300)
            는 같은 역할을 함
```

```swift
make.top.equalTo(view.safeAreaLayoutGuide)          make.bottom.equalTo(view.safeAreaLayoutGuide)        make.trailing.equalTo(view.safeAreaLayoutGuide)
make.leading.equalTo(view.safeAreaLayoutGuide)

와

make.horizontalEdges.verticalEdges.equalTo(view.safeAreaLayoutGuide)

와

make.edges.equalTo(view.safeAreaLayoutGuide)

는 같다.
```

##### offset 과 Inset 


#### 함수부르기 

```swift
func setTextField() -> UITextField {
        let view = UITextField()
        view.placeholder = "제목을 입력해주세요."
        view.backgroundColor = .lightGray
        view.textAlignment = .center
        view.borderStyle = .none
        
        return view
    }
```

를 

```swift
 lazy var titleTextField = setTextField()

// ->

 lazy var titleTextField = {
        let view = UITextField()
        view.placeholder = "제목을 입력해주세요."
        view.backgroundColor = .lightGray
        view.textAlignment = .center
        view.borderStyle = .none
        return view
    }
    
// ->

let titleTextField = {
        let view = UITextField()
        view.placeholder = "제목을 입력해주세요."
        view.backgroundColor = .lightGray
        view.textAlignment = .center
        view.borderStyle = .none
        return view
    }

```

로 바꾸어 구성할 수 있음


#### 네트워크 통신
1. 요청이 있어야 응답을 한다.
	- 클라이어트 - 서버
2. GET POST PUT DELETE
	- Request
		- GET : 주세요
		- POST : 추가, 작성
		- PUT :  수정 요청
		- DELETE : 삭제 요청 
	- Response
3. 인증키
4. API
	- Application Programming Interface


`HTTPS`: 
`Quary String`:

5. XML 과 JSON
	- JSON Serialization