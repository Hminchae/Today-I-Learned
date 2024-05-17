#git #강의노트 #bit #CS 
- GB != GIB
- 비트와 바이트의 차이

- on/off 가 일어나는 연산이 1hz 

### Re: GIT
> istributed Viersion Control Systems

- Git 은 VCS의 일종
- CVCS vs DVCS
	- CVCS
		- Delta방식
	- DBCS : git
		- 코드를 분산적으로 관리
		- 스냅샷 + 델타 방식
- Git 의 장점
	- 코드를 분산
	- 네트워크 X
	- 깃의 용량 관리는 최근 것은 스냅샷 기반으로 관리하고 오래된 것은 델타로 관리함

> 델타 방식 : 파일의 변화만 체크하여 차이점 인식해서 관리
> 스냅샷 : 특정 시점의 파일과 디렉토리 상태를 그대로 사진찍듯 관리 

#### Git Add
Untracked ->ADD -> Tracked