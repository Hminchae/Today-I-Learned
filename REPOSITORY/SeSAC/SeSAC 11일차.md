> 개인적인 궁금함
> super. 는 왜 호출하는건지?

- super.viewDidLoad()를 호출하는 것은 무엇보다도 좋은 습관이라고 생각합니다.
- iOS에서 일반적인 것은 슈퍼클래스가 해야 할 설정 (속성 초기화, 배치 등)을 완료한 후 모든 하위 클래스 설정을 수행하는 것입니다. 변경을 시작하기 전에 슈퍼클래스가 모든 설정을 처리할 수 있는 기회를 주지 않으면 이상한 버그와 동작이 발생할 수 있습니다.
- 우리는 클래스 초기화와 평행선을 그릴 수 있습니다. "지정된 이니셜라이저는 상속된 속성에 값을 할당하기 전에 슈퍼클래스 이니셜라이저까지 위임해야 합니다." 우리는 모든 슈퍼클래스 속성에 값이 있는지 확인하고 하위 클래스에서 상속을 통해 안전하게 사용할 수 있다는 사실을 기반으로 이 작업을 수행합니다.
- 경험 법칙:  
    - 초기화/설정할 때 상위 클래스의 구현을 먼저 실행하십시오.  
    - 해체/정리할 때 상위 클래스의 구현을 마지막에 실행하십시오.  
    - viewDidLoad()가 일종의 초기화라고 가정하면 수퍼클래스에서 올바르게 설정하기 위해 먼저 super.viewDidLoad()를 호출해야 합니다.
- UIViewController 기본 클래스에서 viewDidLoad() 구현을 확인하면 비어 있음을 알 수 있습니다. 따라서 자식 클래스에서 super.viewDidLoad()를 호출하는 유일한 이유는 좋은 코딩 스타일 때문일 것입니다 :-) 따라해 봅시다!

> 네비게이션을 두번 임베드 하면 네비게이션 바 영역이 두개가 생김

RTL (Right to Left)

메모리 : 임시적으로 사용하는 공간


### 프로퍼티
- 저장 프로퍼티
  ```swift
struct Media {
    let title = "극한 직업" // 저장 프로퍼티
    var runtime = 123
    lazy var video = Video() // 나 초기화 필요할 때만 해주면 안되나? -> lazy, 저장 프로퍼티
    
    init() {
        print("Media init")
    }
}

```
-  지연 저장 프로퍼티
	 - 인스턴스가 생성되었더라도, lazy 가 선언되어 있다면 이 프로퍼티는 사용 시점에 초기화가 된다.
	 - 즉 인스턴스 생성 시점과 무관
	 - 즉 사용하지 않으면 초기화 되지 않는다.
	 - 즉 메모리 공간을 차지하지 않는다
	 - lazy 는 var 와 함께 사용한다.

- 연산 프로퍼티

- 인스턴스 프로퍼티
- 타입 프로퍼티


	`코드`  `데이터` `힙` `스택`
`힙` : 참조
`스택` : 값
 --> `인스턴스`
45일 ? 

뷰 컨트롤러의 생명주기

 static 키워드가 붙은 타입 프로퍼티는 데이터 영역에 저장이 됨
 static let team = "SeSAC" // 타입 프로퍼티 -> 앱을 종료하기 전까지 계속 사용하는 공간"
-> 여기저기 생성해서 부르는 것 보다는 낫다는 판단 .lazy 하게 동작함

| 1번                                                                 | 2번                                                                 | 3번                                                                 |
| ------------------------------------------------------------------ | ------------------------------------------------------------------ | ------------------------------------------------------------------ |
| ![[simulator_screenshot_64C95588-ECC6-44CB-961A-E520917CD6D0.png]] | ![[simulator_screenshot_70951948-1B1F-439B-8E37-1EFC9DB441CB.png]] | ![[simulator_screenshot_7558CEBC-13A9-4140-ABAC-22A3BB9F7619.png]] |


#### 1번의 경우
```swift
profileImageView.backgroundColor = .gray
profileImageView.layer.cornerRadius = profileImageView.frame.width / 2
profileImageView.contentMode = .scaleAspectFill
        
reviewImageView.backgroundColor = .gray
reviewImageView.layer.cornerRadius = reviewImageView.frame.width / 2 // 이 친구는 왜 원이 아님?
reviewImageView.contentMode = .scaleAspectFill
```

> 이유 : XIB 가 화면에 보여지는 과정에서 생기는 문제임.
> 1. XIB 비율 -> 2. 해상도 사이즈 판단 -> 3. 정원
> 오토레이아웃을 잡았을 때 너비와 높이를 지정하였기 때문에 왼쪽 원은 정확하게 나옴
> 하지만 오른쪽의 경우 가변 크기 이기 때문에,,!


#### 3번으로 해결!
```swift
override func layoutSubviews() {
        super.layoutSubviews()
    profileImageView.layer.cornerRadius = profileImageView.frame.width / 2
    reviewImageView.layer.cornerRadius = reviewImageView.frame.width / 2 
    }
```

여기 이렇게 이 메서드 안에서 레이아웃을 그리ㄱ ㅔ되면 원으로 잘 나온다. 비율로 화면 비를 잡았을 때 이 메서드를 활용하면 좋다. 뷰가 그려진 이후에도 레이아웃이 그려져야 하는 `뷰의 드로잉 사이클` <- 을 이해하여야 함!


| 1번                                                                 | 2번                                                                 | 3번                                                                 |
| ------------------------------------------------------------------ | ------------------------------------------------------------------ | ------------------------------------------------------------------ |
| ![[simulator_screenshot_90CCCFB5-4200-41C5-AA2A-BE154091DE0F.png]] | ![[simulator_screenshot_97509C0B-4778-4E0D-9800-DD3F9B7A8123.png]] | ![[simulator_screenshot_D6C67A0E-8B81-4022-8D61-AE6911D286C0.png]] |
> 스크롤을 하다보면 광고가 아닌 경우에도 백그라운드에 색이 칠해지는 것을 알 수 있음
>  
#### 1번

```swift
>  if data.ad {
            backgroundColor = .yellow
        } 
```

#### 2번
```swift
if data.ad {
            backgroundColor = .yellow
        } else {
            backgroundColor = .magenta
        }
```
하지만 ㅁ모든 셀의 경우에 대응을 해주면 정상적으로 동작한다.
#### 3번
```swift
override func prepareForReuse() {
        super.prepareForReuse()
        backgroundColor = .white
        reviewImageView.image = nil
    }
```



#### 과제 내용
- ExpandableCell : 확장 가능한 셀
	- label numberOflines = 1
	- 레이아웃 설정(상화좌우)
	- 테이블 셀 높이 : automatic dimension
		- `tableView.rowHeight = UITableView.automaticDimension`

1. TVC -> 2. XIB + UIVC + TV -> 3. 프로퍼티 -> 4.저장 | 연산 | 

4. 
- PrepareForReuse
- layoutSubView
- aware
