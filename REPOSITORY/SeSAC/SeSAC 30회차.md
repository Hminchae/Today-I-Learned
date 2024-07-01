#UrlSession/UrlSessionDelegate 

## 이번주 계획
![[스크린샷 2024-07-01 오전 9.14.08.png]]

### 중요한 세가지
1. UI
2. Network
	- alamofire
	- UrlSession
	- http/socket
3. Database

### URLSession
1. Configuration
	- shared
	- default
2. Task
	- data
	- upload
	- download
3. Response
	- completion handler closure
	- Delegate 
		- shared 속성에선 X, default 속성으로 옮겨가야만 함
		- 여러번 상태를 받아올 수 있음


#### URLSession - Delegate
![[스크린샷 2024-07-01 오전 10.09.50.png]]![[스크린샷 2024-07-01 오전 10.11.37.png]]
> 위 초록박스 세가지는 어떤 순서로 호출이 될까??
> 	 1번 -> 서버에서 최초로 응답 받은 경우에 호출(ex. 상태코드) : 성공 or 실패에 대한 응답이기 때문에
> 	 2번 -> 서버에서 데이터를 받아올 때마다 반복적으로 호출됨
> 	 3번 -> 응답이 완료될 때 호출됨

### 컴파일 최적화
![[스크린샷 2024-07-01 오전 11.21.10.png]]
> 해당 클래스에서만 사용하는 파일.. 클래스 안에 종속적이게 만들어 컴파일 최적화

#### 최적화 수준

![[스크린샷 2024-07-01 오전 11.49.49.png]]![[스크린샷 2024-07-01 오전 11.58.24.png]]![[스크린샷 2024-07-01 오후 12.01.07.png]]
1. Debug : 최적화 수준 ⬇️
	1. Incremental : Swift 기본적으로 각 파일 개별적 컴파일
2. Release : 최적화 수준 ⬆️
	 - WMO : Whole Module Optimization
		 - 서로서로 연결고리를 만들어주어야 하기 때문에 컴파일 시간을 늘어날 수 있다.
		 - 예를 들어 어떤 파일에서 어떤 클래스를 호출하는지.. 등 연관관계를 파악하는 과정이 있음
		 - 하지만 `실행자체`는 빠르다.

> 그래서 컴파일 최적화, 어떻게 할 수 있을까 ?
> ➡️ 서로 파일/코드가 영향이 없게. 필요한 것들만 연결고리가 만들어지게 하여야 함!

- final : 클래스에 대한 상속 X
- 접근 제어 : Private -> 클래스 밖을 못 벗어남
- internal
	- Target 안에서 접근 가능
	- 기본으로는 internel 이 생략 되어 있다고 보면 된다. 
	
 => Method Dispatch (static Dispatch / Dynamic Dispatch)
 컴파일 시점에 함수실행이 확정이 될지, 런타임 시점에 함수실행이 확정이 될지에 관한 것
 -  컴파일 시점에 : Static = direct call
	 - struct
	 - enum
 -  런타임 시점에 : Dynamic
	 - class

> Dynamic 을 static 으로 바꾸어야 조금  더 최적화된 코드가 된다. 가능하면 컴파일단계에!!

BaseViewController의 단점
- func 들이 재정의가 되는것이기 때문에(override) Dynamic Dispatch 로 함수실행이 됨. 

### 오늘의 정리
- URLSession
	- configuration
	- default ...

- 최적화
	- debug, release
	-  위에 두개로 나뉘더라, 그 이유는 wmo 때문
	- final, private
	- Dynamic / static

#### 과제
- [ ] NASA
	- [ ] progress 바..
	- [ ] 다운로드중 버튼을 막는다던가
- [ ] Recap 과 TMDB
	- [ ] final 키워드 붙여보기
	- [ ] 제네릭 써보기..