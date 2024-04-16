#iOS #메모리

### 들어가기 앞서..Xcode로 메모리 누수 확인하기
메모리에 대한 주제를 정리하기
1. **문제 발견**: instruments-memory leak 으로 메모리 릭이 발생하는 구간 확인
2. **문제가 발생한 곳 찾기**: instruments, memory graph 디버깅
3. **Xcode 로 메모리 릭이 발생한 이벤트 2차 검증**: View memory graph hierarchy 의 Backtrace 에서 문제의 함수를 클릭하면 코드를 볼 수 있다.
4. **문제의 함수를 break point 로 디버깅하여 정확한 문제 진단**
5. **문제 해결**
6. **해결되었는지 확인:** instruments-memory leak 으로 다시 테스트
### iOS 디바이스의 메모리 제약과 앱 메모리 제한에 대해 설명해주세요.

앱에서 메모리가 필요하면, 시스템에서 메모리 페이지를 준다. 이 페이지에는 여러 객체들이 저장되고 큰 용량의 객체는 여러 페이지에 걸쳐서 존재할 수 있음. 한 페이지는 16KB정도이며 각 페이지에는 write한 적이 있는지에 따라 Clean 또는 Dirty 메모리로 나뉨

한 앱의 전체 메모리 사이즈는 다음 그림처럼 계산할 수 있음
![memory-footprint](https://seizze.github.io/assets/img/2019-12-20-iOS-%EB%A9%94%EB%AA%A8%EB%A6%AC-%EB%9C%AF%EC%96%B4%EB%B3%B4%EA%B8%B0,-%EB%A9%94%EB%AA%A8%EB%A6%AC-%EC%9D%B4%EC%8A%88-%EB%94%94%EB%B2%84%EA%B9%85%ED%95%98%EA%B8%B0,-%EB%A9%94%EB%AA%A8%EB%A6%AC-%EB%A6%AD-%EC%B0%BE%EA%B8%B0/memory-footprint.png)

일반적인 앱의 메모리는 다음과 같은 세 부분으로 나누어짐. ![app-memory](https://seizze.github.io/assets/img/2019-12-20-iOS-%EB%A9%94%EB%AA%A8%EB%A6%AC-%EB%9C%AF%EC%96%B4%EB%B3%B4%EA%B8%B0,-%EB%A9%94%EB%AA%A8%EB%A6%AC-%EC%9D%B4%EC%8A%88-%EB%94%94%EB%B2%84%EA%B9%85%ED%95%98%EA%B8%B0,-%EB%A9%94%EB%AA%A8%EB%A6%AC-%EB%A6%AD-%EC%B0%BE%EA%B8%B0/app-memory.png)
- Clean 메모리는 이미지, 프레임워크 데이터 등을 포함
- Dirty 메모리는 객체 등 앱에서 수정한 데이터들과 프레임워크 dirty 메모리를 포함
- Compressed 메모리는 압축된 메모리를 의미, 일정 기간 동안 특정 메모리 영역에 접근하지 않으면, 시스템이 해당 메모리 페이지들을 압축하고, 다시 접근할 때 압축 해제함 -> iOS 에서는 Memory compressor를 이용하여 이런 압축 또는 압축해제 작업들을 수행

> 여기서, 앱이 할당 받을 수 있는 메모리 Footprint 에는 제한 한도가 존재, 이 한도치를 넘으면 EXC_RESOURCE_EXCEPTION 이 발생함

### 메모리 워드(word) 크기와 데이터 정렬(alignment)이 메모리 액세스 성능에 미치는 영향에 대해 설명해주세요.


### 포인터 크기(32비트, 64비트)에 따른 메모리 사용량 차이와 고려 사항에 대해 설명해주세요.


### iOS 앱에서 대용량 데이터를 다룰 때 메모리 사이즈를 고려한 최적화 방안에 대해 설명해주세요.