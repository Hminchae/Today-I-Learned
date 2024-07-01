#### 모듈 컴파일
- 단일 파일 컴파일의 경우, 모듈 내 파일들을 하나씩 컴파일 함
- 한계 : 파일내에 컴파일만 이루어짐
	- function inlining 이 안 됨
	- function specialization 이 안 됨
	-  ➡️ 결국 컴파일 시간이 길어짐

#### WMO
- 모듈 전체를 확인, 단일 파일 컴파일의 한계를 극복
- 장점 
	- function inlining 이 가능
	- function specialization 이 가능
	- 불필요한 referencing counting 제거
	- 적은 수의 기계 명령어 생성
- 장점2
	- non-public 함수에 대한 분석
	- 죽은 함수를 찾아냄
	- 컴파일 최적화 -> 컴파일 시간 단축
> WMO의 경우 컴파일 시간은 늘어날 수 있지만 실행속도는 빨라지는게 아닌가?

#### 컴파일 시간
- 컴파일 과정에는 파싱, 타입체킹, SIL, LLVM 백엔드 등이 포함된다.
	- 파싱, 타입체킹 : 엄청 빨리 끝나는 작업
	- SIL : 전체 컴파일 시간의 1/3 정도를 차지
	- LLB