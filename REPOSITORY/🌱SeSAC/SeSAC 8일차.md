
### Emotion Diary  꿀팁

> 큰곳에서 작은쪽으로..

> 유저디폴트 어케해요?

> 유저디폴트 여러번 쓰면 메모리 관리 측면에서 ..

-> 그런거 별로임, 왜냐면 배터리가 꺼졌을때 등등 상황에 대한 핸들링이 더 복잡해질 수도 있음. 그래서 그때 그때 유저디폴트에 반영하는게 더 최적임. 

그리고 앱이 종료될때 호출되는 라이프 사이클 함수를 이용한다면 백그라운드에 남아있을때  등등 에러를 핸들링하기 더 어려워짐

> 라이프사이클

viewDidLoad() -> 한번 호출이 되고 나서 탭바에서는 다시 안 뜸
1. 탭바가 두개 있을땐 viewDidLoad X 
2. disappear 가 호출 
3. `viewWillAppear` - `viewDidAppear` 는 한 세트 : 눈에 보일때마다 호출이 됨  


Present Popover : 아이패드용


### VC 화면전환과 라이프사이클
![[스크린샷 2024-05-23 오전 11.52.49.png]]
> 어떻게 전환이 되느냐에 따라 호출되는 메서드 또한 다르다
- Show
	- 만약 네비게이션 컨트롤러가 있으면 오른쪽에서 등장 `오른쪽 -> 왼쪽`
- 화면을 잡고 있으면 DidDisappear는 끝까지 호출되지 않음
		- Didappear도 마찬가지

	- 만약 네비게이션 컨트롤러가 없다면 `아래 -> 위`
- Modal 
	- 만약 네비게이션 컨트롤러가 있으면 `아래 -> 위`
	- 만약 네비게이션 컨트롤러가 없다면 `아래 -> 위`

> 화면전환과 뷰컨트롤러의 종류에 따라 생명주기가 달라지기 때문에 이걸 정리해두면 좋음
> 😇 작년 WW 에서 `viewIsAppearing` 이 새로 나옴!  -> `viewWillAppear` 와 `viewDidAppear` 사이 호출 

> 스토리보드 간의 결합 : `cmd` + `shift` + `L` -> 스토리보드 레퍼런스
### 테이블뷰

#### 테이블 뷰의 필요성
- 많은 뷰 객체
- 반복적인 디자인과 코드
- 어려운 스크롤 구현

> 반복적이고 많은 데이터를 간단하게 표현할 방법이 없을까? => 테이블 뷰 컨트롤러
![[스크린샷 2024-05-23 오후 2.22.31.png]]

테이블뷰 = `Section` + `Cell`
- TableView
	- content 제공방식
		- Dynamic Prototypes
			-  Cell 에 대한 콘텐츠가 다를 때 사용
			- 코드를 작성해야 눈에 보임 
		- Static Cell
			- 정해진 구조
	- View
		- Header
		- Footer
	- Style
		- Plain
		- Grouped
		- Inset Grouped : 동글동글
- Section
	- System
- Cell
	- System : 애플이 제공
		- Basic
		- 
	- Custom
	- 

![[스크린샷 2024-05-23 오후 3.11.05.png]]
-> 키보드 내림 처리 신경 쓸 필요 있음
![[스크린샷 2024-05-23 오후 3.32.23.png]]
-> Identifier 가 존재하는지 시스템이 확신하지 못해서

#### 기본 양식
```swift
// 1. 셀의 갯수(필수)
    // ex. 카카오톡 100명
    override func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
        return 100
    }
    
    // 2. 셀의 높이(약간 필수 권장...)
    override func tableView(_ tableView: UITableView, heightForRowAt indexPath: IndexPath) -> CGFloat {
        return 80
    }
    
    // 3. 셀의 디자인 및 데이터 처리
    // ex. 카카오톡 친구 이름. 프로필 사진. 상태 메시지 등
    override func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
        // 3-1. 어떤 셀을 쓸 지 결정
        let cell = tableView.dequeueReusableCell(withIdentifier: "thanky")!
        
        return cell
    }
```

> *** 중요!
> 앞으로 테이블뷰를 사용할 때 꼭 Dynamic Prototypes 이용! 

#### IndexPaths
> 특정 섹션의 특정 행에 대한 위치 정보
> 섹션과 행의 속성을 통해 엑세스 가능

왜 보이는 페이지에 있는 데이터만 불러오는 것 ? 필요한 만큼만 로드!! 

`dequeueReusableCell` => 재사용 메커니즘

```swift
 if indexPath.row == 0 {
            cell.textLabel?.text = list[indexPath.row]
            cell.textLabel?.textColor = .yellow
        } else if indexPath.row == 1 {
            cell.textLabel?.text = list[indexPath.row]
            cell.textLabel?.textColor = .red
        } else if indexPath.row == 2 {
            cell.textLabel?.text = list[indexPath.row]
            cell.textLabel?.textColor = .opaqueSeparator
        } else {
            cell.textLabel?.text = list[indexPath.row]
            cell.textLabel?.textColor = .blue
        }
```

이 코드를