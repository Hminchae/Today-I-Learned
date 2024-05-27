> TableViewController 와 그냥 ViewController 에 SearchBar 와 TableView를 임베드 한 결과 : ViewController 의 SearchBar는 스코롤 시 안 없어진다!!


1. TableView : 기능이 많다
	1. Delegate - 함수
	2. Datasource - 함수
![[스크린샷 2024-05-27 오전 9.50.02.png]]![[스크린샷 2024-05-27 오전 9.50.30.png]]
> **그냥 뷰컨트롤러는 부하직원이 없다!**

![[스크린샷 2024-05-27 오전 9.53.43.png]]
tableViewController 의 기능을 사용하기 위해선 이 두 함수를 구현하는 것이 필수적이다..! override 가 붙어있지 않음을 확인할 수 있음![[simulator_screenshot_0BA9C89E-876A-47CE-BB9D-C96B1675550C.png]]
> 그런데 왜 아무것도 안 보일까?
> 	- 부하직원을 가지고는 왔지만 연결이 되어있지 않음
> 	- 테이블뷰가 없더라도 부하직원 가지고 올 수 있고..


### XML ? XIB? NIB?
![[스크린샷 2024-05-27 오전 10.38.34.png]]

### awakeFromNib
```swift
override func awakeFromNib() {
        super.awakeFromNib()
        configureLayout() // -> 호출 수 를 줄이게 함, 변경이 되지 않는 디자인들을 여기에 넣어 최적화 함
    }
```

| http 로 변경시                                                         | Xcode 오류 화면                          | 해결방법                                 |
| ------------------------------------------------------------------ | ------------------------------------ | ------------------------------------ |
| ![[simulator_screenshot_17A2460C-9B39-400C-A3CD-0019D0B7B775.png]] | ![[스크린샷 2024-05-27 오전 11.56.33.png]] | ![[스크린샷 2024-05-27 오후 12.01.31.png]] |
Apple 은 무조건 ATS..


### awakeForNib()

커스텀 뷰 클래스가 처음 만들어져서 초기화 되었는데, 크기나 위치 같은 속성이 완벽하지 않은 상태? 
UIView 에서 상속받은 커스텀 View 클래스를 만들고 

아카이브라는 것 ? : 객체들의 참조 관계를 따라 데이터를 저장하는 방식
언아카이브 : 아카이브한 데이터로부터 객체를 생성하는 과정?

### XIB 와 NIB
- XIB(XML Interface Builder) : 인터페이스 빌더에서 구성한 모든 정보는 .xib 파일로 저장. 이후 프로젝트 컴파일 시 바이너리파일인 .nib 파일이 되는 것임
- NIB(NeXT Interface Builder) : 뷰의 layout, display등의 요소들을 object graph 로 만들어서 직렬화 한 파일
