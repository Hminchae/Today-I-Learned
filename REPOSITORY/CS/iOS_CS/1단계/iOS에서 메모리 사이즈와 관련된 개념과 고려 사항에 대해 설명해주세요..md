#iOS #메모리

### 💡 메모리 기초
> 메모리와 관련하여 기초적인 용어와 개념을 먼저 정리하고 넘어가보겠음. 아래 내용은 WWDC18의 Memory Deep Dive 내용을 많이 포함하고 있음..

#### 메모리 용어
1. virtual memory
	- 운영체제에서의 가상메모리
	- 하드웨어 RAM을 물리적 메모리라고 한다면, 이 물리적 메모리가 부족해서 디스크 공간도 같이 사용하는 방법임
	- 즉, 메모리가 디스크의 공간을 사용하는데 마치 디스크 공간을 가상 메모리처럼 사용하는 것 (단, 캐싱및 **페이징**을 통해 자주쓰는 데이터를 파악하여 디스크에서 메모리로 올리며 이런 것들을 통해 그냥 디스크만 쓰는 것보다 빠른 것)
	- virtual memory = clean memory + dirty memory
		-  ![[Pasted image 20240416232321.png]]
		- process가 계산을 하다가 메모리에서 데이터를 찾는데, 이 때 virtual memory 라는 것을 두고 virtual memory 에서는 RAM과 disk 공간을 바라봄
		- virtual memory 부분을 적절한 단위로 나누게 되는데, 이것을 Page 라고 함
		- 이 분할된 공간에 접근하려면 분할된 공간의 주소가 Page Table이라는곳에 저장되고 RAM은 이 Page Table을 보고 디스크 공간에 접근
		
		- ![](https://blog.kakaocdn.net/dn/cxQGRV/btsCG1Op2Lo/0XnmEcdNlKynSHooneNfZK/img.png)
		- page out: 물리메모리에 page에 대응하는 데이터가 없어서, 물리메모리에 있는 어느 한 page와 disk에 있는 page랑 swap 해야하는데, 이 때 물리메모리에서 사용하지 않은 공간을 내준다는 의미로 page out이라 함
		- page in : 위에서 page out 되면서 반대로 디스크 입장에서는 swap 될 때 보내는 page를 의미
2. dirty memory 와 clean memory
	- clean memory : 값이 변경되지 않은 깨끗한 메모리
		- 새로운 데이터를 쓰기 위하여 사용
		- page out 될 수 있는 공간
		- 아직 물리 메모리에서 사용되지 않아서 디스크로 언제든지 보낼 수 있어 여유공간을 의미함
	- dirty memory : 값이 변경되어 더러운 메모리
		- page out 될 수 없는 이미 수정된 데이터 영역
		- 쓰기 작업이 발생했기 때문에 다시 읽을 필요가 있거나, 변경된 내용을 디스크에 반영해야 할 때 사용
		- 힙, 싱글톤 등 인스턴스들이 스택으로 채워진 메모리
	ex) 배열을 선언하고 특정 인덱스에 값을 할당하면, 그 인덱스 영역은 이미 사용했으므로 **page out**이 불가능한 영역
	![](https://blog.kakaocdn.net/dn/bUEdr4/btsCzSZetlK/r4rMGh2RiAXUtX2EzgYACk/img.png)
3. compressed memory
	- 가상 메모리를 사용하면 결국 디스크까지 가느라 I/O 작업으로 인하여 속도가 저하될 수 있어, WWDC 2013에서 디스크까지 굳이 가지 않고 RAM을 먼저 최적화 하는 방식인 compressed memory를 발표했음 -> **메모리 효율성**
	- 동작원리
		- 시스템의 메모리가 채워지기 시작하면, compressed memory는 메모리에서 가장 최근에 사용된 항목을 자동으로 압축하여 원래 크기의 반으로 압축함
		- 만약, 이 압축된 데이터들이 필요할 때 compressed memory가 즉시 압축 해제를 시도함
	- 효과
		- 가상메모리 사용 시, disk에서 swap 하는 비용을 최소화
		- 메모리 압축은 물리적 메모리의 사용을 최적화 하면서도 전력 소모를 최소화하게 됨
	- 압축률은 50퍼센트 이상이며 하나의 페이지를 압축하는데 백만분의 수 초가 수요됨
	- 더 알아보고 싶으면 [여기]([https://www.apple.com/media/us/osx/2013/docs/OSX_Mavericks_Core_Technology_Overview.pdf](https://www.apple.com/media/us/osx/2013/docs/OSX_Mavericks_Core_Technology_Overview.pdf)) 참고
5. swapped memory
	- 물리 메모리가 가득 찬 상태에서 더 많은 공간이 필요한 경우, 디스크 공간을 이용하여 부족한 메모리를 대체할 수 있는 공간
6. resident memory(resident size)
	- RAM에 올라온 데이터들, 즉 실제 사용되어지는 데이터들을 의미
#### iOS의 Memory Footprint
앱에서 메모리가 필요하면, 시스템에서 메모리 페이지를 줌(페이징). 이 페이지에는 여러 객체들이 저장되고, 큰 용량의 객체는 여러 페이지에 걸쳐 존재할 수 있다. 한 페이지는 16KB 정도이고, 각 페이지는 write 한 적이 있는지에 따라 앞서 살펴본 clean memory 와 dirty memory 로 나뉘게 됨

한 앱의 전체 메모리 사이즈는 이렇게 계산됨
- 앱의 메모리 사용량 = page 수 * 페이지 크기(16K)
- ![memory-footprint](https://seizze.github.io/assets/img/2019-12-20-iOS-%EB%A9%94%EB%AA%A8%EB%A6%AC-%EB%9C%AF%EC%96%B4%EB%B3%B4%EA%B8%B0,-%EB%A9%94%EB%AA%A8%EB%A6%AC-%EC%9D%B4%EC%8A%88-%EB%94%94%EB%B2%84%EA%B9%85%ED%95%98%EA%B8%B0,-%EB%A9%94%EB%AA%A8%EB%A6%AC-%EB%A6%AD-%EC%B0%BE%EA%B8%B0/memory-footprint.png)
- 일반적으로 앱의 메모리는 이렇게 세 부분으로 나누어짐
- ![app-memory](https://seizze.github.io/assets/img/2019-12-20-iOS-%EB%A9%94%EB%AA%A8%EB%A6%AC-%EB%9C%AF%EC%96%B4%EB%B3%B4%EA%B8%B0,-%EB%A9%94%EB%AA%A8%EB%A6%AC-%EC%9D%B4%EC%8A%88-%EB%94%94%EB%B2%84%EA%B9%85%ED%95%98%EA%B8%B0,-%EB%A9%94%EB%AA%A8%EB%A6%AC-%EB%A6%AD-%EC%B0%BE%EA%B8%B0/app-memory.png)
- 앱이 할당받을 수 있는 메모리 Footprint에는 제한 한도가 존재하고, 이 한도치를 넘어가면 `EXC_RESOURCE_EXCEPTION` 발생 -> 다음주제에서 계속
#### iOS의 메모리 관리
1. didReceiveMemoryWarning() 핸들링
	 ```swift
	 // AppDelegate.swift 
	 func applicationDidReceiveMemoryWarning(_ application: UIApplication) {
	  
	 }
	 ```
	- iOS7 이후 Compressed Memory를 사용하여 이전보다 더 많은 메모리를 사용할 수 있고, 메모리 해제가 복잡하게 되었는데 이 영향에 의하여 메모리 경고 처리가 필요함
	- 메모리 경고가 발생할 때 잠시 아무것도 캐싱하지 않거나, 일부 백그라운드 작업을 제한하는 작업을 권장
	- `cashe.removeAllObjects()`를 사용하여 캐싱을 제거하는게 가장 간편한 방법이라 함
2. 메모리 프로파일링 툴 사용
	1. Xcode memory graph debugger
		 - ![[스크린샷 2024-04-17 오전 12.39.35.png]]
		-  이 방법은 비추라함. WWDC2018에 따르면 Xcode에서 앱을 실행하면 더 많은 메모리를 소비하여 정확한 측정이 어렵다고..
	2. Instrument로 메모리 누수 확인하기
	   - ![[스크린샷 2024-04-16 오후 10.56.31.png]]
		`아래 같은 시퀀스로 메모리 누수를 확인하고 문제를 해결할 수 있다` 
		
		1. ==**문제 발견**: instruments-memory leak 으로 메모리 릭이 발생하는 구간 확인==
		2. ==**문제가 발생한 곳 찾기**: instruments, memory graph 디버깅==
		3. ==**Xcode 로 메모리 릭이 발생한 이벤트 2차 검증**: View memory graph hierarchy 의 Backtrace 에서 문제의 함수를 클릭하면 코드를 볼 수 있다.==
		4. ==**문제의 함수를 break point 로 디버깅하여 정확한 문제 진단**==
		5. ==**문제 해결**==
		6. ==**해결되었는지 확인:** instruments-memory leak 으로 다시 테스트==
	3. Command Line Tool 도 사용 가능하당..
		- ![vmmap-summary](https://seizze.github.io/assets/img/2019-12-20-iOS-%EB%A9%94%EB%AA%A8%EB%A6%AC-%EB%9C%AF%EC%96%B4%EB%B3%B4%EA%B8%B0,-%EB%A9%94%EB%AA%A8%EB%A6%AC-%EC%9D%B4%EC%8A%88-%EB%94%94%EB%B2%84%EA%B9%85%ED%95%98%EA%B8%B0,-%EB%A9%94%EB%AA%A8%EB%A6%AC-%EB%A6%AD-%EC%B0%BE%EA%B8%B0/vmmap-summary.png)
		- 이런식으로 가능하다는데 자세한건 [여기](https://seizze.github.io/2019/12/20/iOS-%EB%A9%94%EB%AA%A8%EB%A6%AC-%EB%9C%AF%EC%96%B4%EB%B3%B4%EA%B8%B0,-%EB%A9%94%EB%AA%A8%EB%A6%AC-%EC%9D%B4%EC%8A%88-%EB%94%94%EB%B2%84%EA%B9%85%ED%95%98%EA%B8%B0,-%EB%A9%94%EB%AA%A8%EB%A6%AC-%EB%A6%AD-%EC%B0%BE%EA%B8%B0.html)를 참고하자..
### 💡iOS 디바이스의 메모리 제약과 앱 메모리 제한에 대하여
> 만약 앱이 메모리를 너무 많이 사용한다면 iOS는 경고를 보낸다.. crash report 형태의 notifications를 받을 수 있는데 이 리포트는 앞서 적혀있던 `EXC_RESOURCE exception type`과 `MEMORY subtype` 등을 포함하는데 앱 메모리가 거의 한계에 이르렀다는 걸 알려준다. 근데 이건 메모리 사용 문제를 발견했다는거지 앱이 종료 되지는 않는다. 메모리 제한은 디바이스에 따라 다르고 앱이 이 제한을 초과하면 iOS가 앱을 완전 종료 시킨다. 

#### WWDC 피셜 메모리 제한에 관한..
![](https://miro.medium.com/v2/resize:fit:700/1*Pz-_3_vuNre3m9eGWkOMMg.png)
- 디바이스별로 메모리 한계치가 다르다..
- Extensions는 더 낮은 한계치를 가지고 있고
- 이 한계치들을 넘을때 `EXC_RESOURCE exception`이 에러로 나오게 됨
#### 디바이스별 메모리 제약
> 각 디바이스별로 앱에서 사용할 수 있는 최대 메모리를 [스택오버플로우](https://stackoverflow.com/questions/5887248/ios-app-maximum-memory-budget)에서 정리해 놓았길래 가져옴

![[스크린샷 2024-04-17 오전 1.32.10.png]]
- [여기]([https://github.com/Split82/iOSMemoryBudgetTest](https://github.com/Split82/iOSMemoryBudgetTest))에서 메모리 워닝과 크래쉬 한도를 찾을 수 있고 도움을 주는 소스를 확인할 수 있음
### 💡메모리 워드(word) 크기와 데이터 정렬(alignment)이 메모리 액세스 성능에 미치는 영향에 대해 설명해주세요.


### 💡포인터 크기(32비트, 64비트)에 따른 메모리 사용량 차이와 고려 사항에 대해 설명해주세요.


### 💡iOS 앱에서 대용량 데이터를 다룰 때 메모리 사이즈를 고려한 최적화 방안에 대해 설명해주세요.

이미 동호님과 창준님이 아래 이슈에서 정리해주셨기 때문에 넘어가겠습니다.

### 📝 참고
- 김종권님의 iOS 메모리 시리즈
	-  [iOS 메모리 기초개념](https://ios-development.tistory.com/1604)
	- [iOS 메모리 운영체제 기초](https://ios-development.tistory.com/1585)
	- [페이징, Compressed 메모리](https://ios-development.tistory.com/1587)
	- [Memory Footprint 프로파일링 방법](https://ios-development.tistory.com/1588)
- [앱에서 너무 많은 메모리를 사용하면 어떻게 될까?](https://woongsios.tistory.com/206)