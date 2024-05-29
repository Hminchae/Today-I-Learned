#화면전환 #storyboard 
## 수업 필기
#### 화면 전환
- Action Segue 종류
	- show, present modally 
	- show detail, present as popover : 아이패드에서 사용
![[스크린샷 2024-05-29 오후 7.33.37.png]]
💡 이것의 명칭은 Segue 또는 SegueWay

> ✏️생각해볼 점 : 셀을 xib 로 만들었을 때 화면 전환을 어떻게 해야하지?
> 1. Segue 연결 어려움
> 2. 화면 다양성
> 3. 짝궁
> 	- present - dismiss
> 	- push - pop



##### 화면 전환의 필요성
- 제한된 스크린 크기
- 사용자 편의성 고려
- 적절한 정보 제공
##### 화면 전환 고려사항
- `네비게이션 콘텐츠`
	- 전환 방식
		- 상세 정보 : 오른쪽 
		- 기존과 다른 정보 : 아래 -> 위
	- 전환 효과
		- 페이지 전환효과 : 모달,  책넘김
		- 팝업 등
- `특성`
	- +/- 의 법칙

##### 개발 방법
> 📚 스토리보드와 코드베이스의 차이는 뭐예요?
- 인터페이스 빌더
	-  방향 짐작 가능
	- 코드 필요 x - 구현 쉬움
	- 세부적 대응 불가능
- 코드
	- 방향 짐작 어려움
	- 코드 필요 O - 콘텐츠 표현 용이
	- 세부적 대응 가능
##### Show vs Modal
- show : 네비게이션 컨트롤러를 가지고 있어야 함

```swift
@IBAction func presentModal(_ sender: UIButton) {
        // 1. 스토리보드 가져오기
        let sb = UIStoryboard(name: "Setting", bundle: nil) // 내가 만든 파일이면 모두 nil
        // 2. 스토리보드 내 내 전환하고자 하는 화면 가져오기
        // -> instantiate ~ : 인스턴스를 생성해주는 친구
        let vc = sb.instantiateViewController(withIdentifier: "BrownViewController") as! BrownViewController // 메모리에 올릴 준비 해라
        // 3. 화면 띄우기
        present(vc, animated: true)
    }
```

```swift
@IBAction func pushShow(_ sender: UIButton) {
        // 1. 스토리보드 가져오기
        let sb = UIStoryboard(name: "Setting", bundle: nil)
        // 2. 스토리보드 내 전환하고자 하는 화면 가져오기
        let vc = sb.instantiateViewController(withIdentifier: "BrownViewController") as! BrownViewController
        // 3. 화면 띄우기 : push Show 의 경우엔 네비게이션 컨트롤러 프로퍼티를 가져온다.
        // 컨트롤러 없으면 화면전환 X
        // 스토리보드에서 네비게이션 컨트롤러가 임베드 되어있지 않으면 push 안됨
        navigationController?.pushViewController(vc, animated: true)
    }
```

```swift
    @IBAction func presentFullScreen(_ sender: UIButton) {
        // 1. 스토리보드 가져오기
        let sb = UIStoryboard(name: "Setting", bundle: nil)
        // 2. 스토리보드 내 전환하고자 하는 화면 가져오기
        let vc = sb.instantiateViewController(withIdentifier: "BrownViewController") as! BrownViewController
        // 2-1. 화면 옵션
        // fullScreen은 dismiss를 직접 구현해주어야 함
        vc.modalPresentationStyle = .fullScreen // default 는 automatic
        // present 방식에서 화면을 띄울 때 애니메이션
        vc.modalTransitionStyle = .partialCurl // default는 .coverVertical
        // !! modalTransitionStyle은 옵션 종류에 따라 동작이 안 되거나 런타임 이슈가 발생할 수 있음
        // 3. 화면 띄우기
        present(vc, animated: true)
    }
```

```swift
@IBAction func presentNavigation(_ sender: UIButton) {
        // 1. 스토리보드 가져오기
        let sb = UIStoryboard(name: "Setting", bundle: nil)
        // 2. 스토리보드 내 전환하고자 하는 화면 가져오기
        let vc = sb.instantiateViewController(withIdentifier: "BrownViewController") as! BrownViewController
        // 2-1. 네비게이션 컨트롤러 임베드
        let nav = UINavigationController(rootViewController: vc)
        nav.modalPresentationStyle = .fullScreen
        nav.modalTransitionStyle = .flipHorizontal
        // 3. 화면 띄우기
        present(nav, animated: true)
    }
```

##### delegate 와 datasource 
`TableView.delegate = self` 

##### 💡 셀을 클릭했는데 동작을 안 한다면 ? 
-   print 로 확인
-  `delegate, datasource = self` 빠뜨리지 않았나..
- 연결이 안 되어 있거나..
- 테이블뷰나 셀이 클릭이 되는 상태인지 interaction/selection
	-  `tableView.isUserInteractionEnabled = false`
	- `tableView.allowsSelection = false` 이런애들 써 있거나..
-  클릭되는 컨트롤들이 위에 있는 상태인지
- 제스처 중첩 : 만약 셀 클릭 + 셀에 탭제스처, 테이블 뷰 탭제스처


/*
 프로토콜: 클래스/구조체/열거형
 - 상속 아님
 - 클래스 전체를 책임지지 않고, 특정 뷰나 기능에 대한 요소를 담당
 - 필수 요구사항은 모두 다 구현을 해주어야 함
 - 필수 요구사항(Requirement)은 모두 다 구현을 해주어야 함
    - Property Requirements
    - Method Requirements
    - Optional Requirements
 - 프로토콜은 구현은 안 함!
 */

#### 과제 
✅ 인기도시
	 - 세그먼트 컨트롤 사용
	 - 검색
		 - 공백 
		 - 입력방지
		 - `다낭` 검색시 하이라이팅
✅ 뷰 이동 구현하기

