#화면전환 #storyboard 
## 수업 필기
#### 화면 전환
- Action Segue 종류
	- show, present modally 
	- show detail, present as popover : 아이패드에서 사용
![[스크린샷 2024-05-29 오후 7.33.37.png]]
💡 이것의 명칭은 Segue 또는 SegueWay

> 생각해볼 점 : 셀을 xib 로 만들었을 때 화면 전환을 어떻게 해야하지?
> 1. Segue 연결 어려움
> 2. 화면 다양성



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
#### 과제 
✅ 인기도시
	 - 세그먼트 컨트롤 사용
	 - 검색
		 - 공백 
		 - 입력방지
		 - `다낭` 검색시 하이라이팅
✅ 뷰 이동 구현하기

