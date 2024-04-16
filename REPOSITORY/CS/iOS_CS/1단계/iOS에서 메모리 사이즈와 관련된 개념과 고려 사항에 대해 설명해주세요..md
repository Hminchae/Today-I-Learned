#iOS #메모리

### iOS 디바이스의 메모리 제약과 앱 메모리 제한에 대해 설명해주세요.

앱에서 메모리가 필요하면, 시스템에서 메모리 페이지를 준다. 이 페이지에는 여러 객체들이 저장되고 큰 용량의 객체는 여러 페이지에 걸쳐서 존재할 수 있음. 한 페이지는 16KB정도이며 각 페이지에는 write한 적이 있는지에 따라 Clean 또는 Dirty 메모리로 나뉨

한 앱의 전체 메모리 사이즈는 다음 그림처럼 계산할 수 있음
![memory-footprint](https://seizze.github.io/assets/img/2019-12-20-iOS-%EB%A9%94%EB%AA%A8%EB%A6%AC-%EB%9C%AF%EC%96%B4%EB%B3%B4%EA%B8%B0,-%EB%A9%94%EB%AA%A8%EB%A6%AC-%EC%9D%B4%EC%8A%88-%EB%94%94%EB%B2%84%EA%B9%85%ED%95%98%EA%B8%B0,-%EB%A9%94%EB%AA%A8%EB%A6%AC-%EB%A6%AD-%EC%B0%BE%EA%B8%B0/memory-footprint.png)

일반적인 앱의 메모리는 다음과 같은 세 부분으로 나누어짐. ![app-memory](https://seizze.github.io/assets/img/2019-12-20-iOS-%EB%A9%94%EB%AA%A8%EB%A6%AC-%EB%9C%AF%EC%96%B4%EB%B3%B4%EA%B8%B0,-%EB%A9%94%EB%AA%A8%EB%A6%AC-%EC%9D%B4%EC%8A%88-%EB%94%94%EB%B2%84%EA%B9%85%ED%95%98%EA%B8%B0,-%EB%A9%94%EB%AA%A8%EB%A6%AC-%EB%A6%AD-%EC%B0%BE%EA%B8%B0/app-memory.png)
- Clean 메모리는 이미지, 프레임워크 데이터 등을 포함
- Dirty 메모리는 객체 등 앱에서 수정한 데이터들과 프레임워크 dirty 메모리를 포함
- Compressed 메모리는 압축된 메모리를 의미, 일정 기간 동안 특정 메모리 영역에 접근하지 않으면, 시스템이 해당 메모리 페이지들을 압축하고, 다시 접근할 때 압축 해제함 -> iOS 에서는 Memory compressor를 이용하여 이런 압축 또는 압축해제 작업들을 수행

>메모리 워드(word) 크기와 데이터 정렬(alignment)이 메모리 액세스 성능에 미치는 영향에 대해 설명해주세요.


> 포인터 크기(32비트, 64비트)에 따른 메모리 사용량 차이와 고려 사항에 대해 설명해주세요.


> iOS 앱에서 대용량 데이터를 다룰 때 메모리 사이즈를 고려한 최적화 방안에 대해 설명해주세요.