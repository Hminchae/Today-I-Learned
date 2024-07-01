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

### 접근제어자

#### 컴파일 최적화
![[스크린샷 2024-07-01 오전 11.21.10.png]]
> 해당 클래스에서만 사용하는 파일.. 클래스 안에 종속적이게 만들어 컴파일 최적화

#### 최적화 수준
1. 모드
	1. Debug
	2. Release
![[스크린샷 2024-07-01 오전 11.49.49.png]]