#강의노트 #개념 #URLSession #HTTP 

>1. "요청" -> 응답
>2. Get, Post..
>3. 인증

##### HTTP <- 16회차 강의 자료
1. Request : 단방향 통신(줄거없냐 줄거없냐?)
2. Connectionless : 비연결성
3. stateless: 무상태성(식별X)
	- 토큰
	- 세션
	- 쿠키

클라이언트=>Application Programming Interface => 서버  

##### RestAPI <- 18회차 강의자료
네트워크를 통해서 핵심 콘텐츠와 기능을 활용할 수 있도록 제공되는 인터페이스, 아키텍쳐 스타일
자원을 중심으로 엔트포인트(URI)를 생성하고, HTTP메서드를 통해 동작을 수행

###### 6원칙
1. Uniform Interface(유니폼 인터페이스)
	- 자원(Resource)에 대한 식별이 가능하여야 함
	- HTTP 메서드를 통해 자원을 조작하여야 함
		- ex) .get을 통해 데이터를 가져오기 등
2. Stateless(무상태)
	- HTTP 특징
	- REST는 HTTP위에서 구현되기 때문에, REST 또한 무상태성을 가짐
	- 클라이언트의 상태가 서버에 저장되지 않고, 각 요청에 대한 응답을 전송 받는 것으로 요청 종료
3. Cacheable(캐시 가능)
	- REST는 HTTP 위에서 구현되기 때문에
	- 즉, 쉽게 이해할 수 있는 자체 표현 구조를 가져야 함 
4. Self-descriptiveness(자체 표현 구조)
	- REST API 메시지(Response/요청 URL/Endpoint 등)만 보고도, 어떤 의도로 구성되어 있는 지 직관적으로 파악할 수 있어야 함
	- 즉 쉽게 이해할 수 있는 자체 표현 구조를 가져야 함
5. Client-Server 구조
6. 계층형 구조

###### 특징
1. 웹의 장점을 최대한 활용한 아키텍쳐

##### 그래서 단점?
- Overfetching
	- 필요한 정보값보다 더 많은 정보값이 로딩될 수 있음
	- ex)네이버 영화 API에서 
- Underfetching 
	- 필요한 정보보다 부족한 정보 로딩으로 인해 추가 API 요청이 필요
- Endpoint
	- 서비스 규모가 커질수록 엔드포인트가 늘어나

16, 17, 18 -> 참고🧡

### URLSession
![[스크린샷 2024-06-27 오전 10.16.46.png]]![[스크린샷 2024-06-27 오후 2.15.50.png]]

> 메인에서 해주어야 할 일을 왜 background에서 해주고 있냐~~ 라는 오류
> URLsession 동작시 자동으로 global 에 할당을 해주게 됨.

VC 
	- UI/View
	- Network


### 메타 타입? 제네릭?

#### 👛 제네릭, 범용타입, < >
 - Type Parameter >> Placeholder 와 같은 역할
 - 타입이 뭔지 모르지만 특정 타입이라는 거는 알 수 있음
 - 호출 시 타입이 결정됨
 - Type Constraints - 프로토콜 제약, 클래스 제약

#### 메타타입
 print(type(of: String.self)) // 메타타입이 가지고 있는 값
	 고래밥 -> String/String.self -> String.Type

----
### 이번주 이것만은 꼭
- [ ] GCD + DispatchGroup
- [ ] Alamofire + Enum
- [ ] URLSession + Handler
- [ ] generic +_MetaType

**네트워크 통신은 꼭 정리를 해두기

### 과제
- [x] TMDB 마무리 (4 ~ 5) : API 횟수 많이 많이(로직마무리,  코드 마무리)
- [x] Recap -> URLSession