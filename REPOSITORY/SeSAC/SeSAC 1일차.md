아웃라인뷰

뷰 -> 버튼이 뷰의 컨트롤 기능을 상속받음
텍스트필드 -> 클릭되는(컨트롤)

Launch Screen -> 로직 X
splash -> 

### 앱의 생명주기
#### AppDelegate.swift의 관리
> 앱이 꺼지냐 켜지냐만 관리
- Not Running : 앱이 시작되기 전 상태
- Foreground
	- Active : 앱이 화면에서 실행중인 상태
	- Inactive : 앱이 화면에서 실행 중이나 어떤 신호도 받지 않는 상태 ex) 전화, 알람
- Background : 앱이 화면에 보이지 않지만 코드를 실행하고 있는 상태
- Suspend : 앱이 곧 종료될 상태

#### SceneDelegate.swift
iOS 13 부터 : 다크모드, iPad OS 등장, SwiftUI 등장
> 앱

#AppThining 

### App Thinning
애플리케이션이 디바이스에 설치될 때, 앱스토어와 운영체제가 디바이스의 특덧ㅇ에 맞게 설치되도록 하는 기술
#### Slicing

Asset

- Any Appearance : ? light 모드
- Dark

> 컬러 이름을 의미 단위로 하자 -> 시멘틱하다 

기본 컬러셋에서 system 이 붙어있는 컬러들은 다크모드가 대응되어 있는 컬러일 수 있음