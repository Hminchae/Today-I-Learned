#SeSAC #강의노트 #iOS 

### 복습

- Asset 에서 사진이 1배수 하나만 차있으면 어떻게 될까? -> 그 하나로 비어있는 배수를 채우게 됨
- JPG PNG <-권장! jPEG  대 SVG
	- JPG PNG <-권장! jPEG : 비트맵
	- SVG : 벡터 이미지 
		- SVG 일 때 Preserve Vector Data <- 이 체크박스가 비어있으면 벡터로 다뤄지지 않음
		- PDF와 비슷
	- 1배수, 2배수 관리가 필요 없는 경우엔 그룹에 직접 추가하여도 됨
- Xcode -> Build Phases
	- Copy Bundle Resource 에 내가 추가한 이미지와 에셋이 추가됨. 
	- 만약 파일 추가할 때 target 추가 하지 않으면 나중에 여기에 다시 와서 추가해주어야 하기 때문에 귀찮아짐
	- 만약 지울 때!
		- Move to Trash
		- Remove Reference : Xcode 상에서만 사라지고..파일엔 아직 살아있어서 추후 문제가 생길 수 있음

- Entry Pointer 가 잘못지정되어 있으면 타이틀이 사라짐

### Navigation Cotroller
1. drill down : 
2. 수직적 연결

Segue

TBC -> TabBar -> TabBarItem -> 


화면 + 기능

- Scene : 뷰객체 + 제스처 + 뷰컨트롤러 => 스토리보드를 통해
- Logic : 어떻게 하면 될까?
	- => Swift 파일 
- 이 두개를 연결함 ! 이 두가의 이름은 같게 설정함

Class 와 스토리보드를 연결할 때 `Inherut Module From Target` 가 체크되어 있어야 함


@IBOutlet <- @는 Swift attribute 임 Interfae Builder -> 아울렛 변수

```swift
// 뷰컨트롤러의 생명주기
// viewDidLoad: 화면이 사용자의 눈에 보이기 직전에 실행되는 기능
// 그림자, 모서리 둥글기 등 스토리보드에서 할 수 없는 UI를 작성하는 편
override func viewDidLoad() {
        super.viewDidLoad() // ex 만약 모서리가 둥근 이미지가 다음 페이지에 있는데 사용자가 테두리가 둥근 상태를 보게 되면 상당히 이상함! 그래서 보기전에 만들어주어야 함
                                            
    }
```

### 

![[스크린샷 2024-05-16 오후 12.12.51.png]]


CG -> 코어 그래픽


this is not key value coding-compliant for te key movieTitleLabel =>

!! 아울렛이나 액션 연결이 끊겼을 때 해결 방법은 꼭 알고 넘어가기



UIButton 과 Any
- Touch Up Inside = 눌렀다가 떼는 동작


```swift
@IBAction func textFieldReturnTapped(_ sender: UITextField) {
        print("나 여기~~")
    }
```

textField 는 액션이 있는데 SearchBar 엔 왜 액션이 없지? => `Control` 을 상ㅇ속받은 textField라서!!!!

SearhBar 는 왜 컨트롤이 없을까?? => 

#### Outlet & Action
#### 속성, 조금씩!! "많이"
