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