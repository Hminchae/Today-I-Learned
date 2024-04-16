#iOS #메모리

### 메모리 기초
> 메모리와 관련하여 기초적인 용어를 먼저 정리하고 넘어가보겠음

1. virtual memory
	- 운영체제에서의 가상메모리
	- 하드웨어 RAM을 물리적 메모리라고 한다면, 이 물리적 메모리가 부족해서 디스크 공간도 같이 사용하는 방법임
		-  ![[Pasted image 20240416232321.png]]
		- process가 계산을 하다가 메모리에서 데이터를 찾는데, 이 때 virtual memory 라는 것을 두고 virtual memory 에서는 RAM과 disk 공간을 바라봄
		- virtual memory 부분을 적절한 단위로 나누게 되는데, 이것을 Page 라고 함
		
		- ![](https://blog.kakaocdn.net/dn/cxQGRV/btsCG1Op2Lo/0XnmEcdNlKynSHooneNfZK/img.png)
		- page out: 물리메모리에 page에 대응하는 데이터가 없어서, 물리메모리에 있는 어느 한 page와 disk에 있는 page랑 swap 해야하는데, 이 때 물리메모리에서 사용하지 않은 공간을 내준다는 의미로 page out이라 함
		- page in : 위에서 page out 되면서 반대로 디스크 입장에서는 swap 될 때 보내는 page를 의미
2. dirty memory 와 clean memory
	- clean memory
		- page out 될 수 있는 공간
		- 아직 물리 메모리에서 사용되지 않아서 디스크로 언제든지 보낼 수 있어 여유공간을 의미함
	- dirty memory
		- page out 될 수 없는 이미 수정된 데이터 영역
	ex) 배열을 선언하고 특정 인덱스에 값을 할당하면, 그 인덱스 영역은 이미 사용했으므로 **page out**이 불가능한 영역
	![](https://blog.kakaocdn.net/dn/bUEdr4/btsCzSZetlK/r4rMGh2RiAXUtX2EzgYACk/img.png)
3. compressed memory
	- 가상 메모리를 사용하면 결국 디스크까지 가느라 I/O 작업으로 인하여 속도가 저하될 수 있어, WWDC 2013에서 디스크까지 굳이 가지 않고 RAM을 먼저 최적화 하는 방식인 compressed memory를 발표했음
	- 메모리의 압축을 위해 WKdm 알고리즘을 사용
		- WKdm 알고리즘 : 32 bit data 14개로 이루어진 디렉토리와 결과를 쓸 메모리 공간만 있으면 대상의 크기에 상관없이 압축을 수행함
	- swap 기준은 LRU 사용
		- LRU 알고리즘: 사용된지 가장 오래된 페이지를 교체대상으로 교체
	- 압축률은 50퍼센트 이상이며 하나의 페이지를 압축하는데 백만분의 수 초가 수요됨
	- 더 알아보고 싶으면 [여기]([https://www.apple.com/media/us/osx/2013/docs/OSX_Mavericks_Core_Technology_Overview.pdf](https://www.apple.com/media/us/osx/2013/docs/OSX_Mavericks_Core_Technology_Overview.pdf)) 참고
4. swapped memory
	- 물리 메모리가 가득 찬 상태에서 더 많은 공간이 필요한 경우, 디스크 공간을 이용하여 부족한 메모리를 대체할 수 있는 공간
5. resident memory(resident size)
	- RAM에 올라온 데이터들, 즉 실제 사용되어지는 데이터들을 의미
#### 들어가기 앞서..Xcode로 메모리 누수 확인하기
메모리에 대한 주제를 정리하기 전에 가볍게 프로젝트 파도의 메모리에 대해서 조사해보고자 했음
iOS 프로젝트의 메모리 누수는 다음과 같은 시퀀스로 조사를 해보면 된다고 함. 나는 일단 문제 발견만 해보기로ㅎㅎ
1. ==**문제 발견**: instruments-memory leak 으로 메모리 릭이 발생하는 구간 확인==
2. ==**문제가 발생한 곳 찾기**: instruments, memory graph 디버깅==
3. ==**Xcode 로 메모리 릭이 발생한 이벤트 2차 검증**: View memory graph hierarchy 의 Backtrace 에서 문제의 함수를 클릭하면 코드를 볼 수 있다.==
4. ==**문제의 함수를 break point 로 디버깅하여 정확한 문제 진단**==
5. ==**문제 해결**==
6. ==**해결되었는지 확인:** instruments-memory leak 으로 다시 테스트==

![[스크린샷 2024-04-16 오후 10.56.31.png]]
Xcode의 instruments -> leak 에서 메모리 누수가 발생하는 구간을 확인하고자 했다.  모든 시나리오를 확인하지는 않고, 게시물 -> 프로필 -> 게시물을 타고타고 들어가면서 확인했고 스크린샷에 보이는 것처럼 메모리 누수가 발생했다는 ❌마크를 확인했다.
### iOS 디바이스의 메모리 제약과 앱 메모리 제한에 대해 설명해주세요.
### 메모리 워드(word) 크기와 데이터 정렬(alignment)이 메모리 액세스 성능에 미치는 영향에 대해 설명해주세요.


### 포인터 크기(32비트, 64비트)에 따른 메모리 사용량 차이와 고려 사항에 대해 설명해주세요.


### iOS 앱에서 대용량 데이터를 다룰 때 메모리 사이즈를 고려한 최적화 방안에 대해 설명해주세요.




### 참고
- [아]