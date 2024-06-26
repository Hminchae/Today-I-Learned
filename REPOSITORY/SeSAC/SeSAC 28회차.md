#강의노트 #네트워크 #모델추상화

#### 네트워크 모델을 추상화 해보기
##### 실패의 경우도 DispatchGroup 에 넘긴다.

![[스크린샷 2024-06-26 오전 9.39.51.png]]![[스크린샷 2024-06-26 오전 9.45.01.png]]
##### 실패의 경우도 튜플타입으로 DispatchGroup 에 넘긴다.
![[스크린샷 2024-06-26 오전 9.57.36.png]]

#### 동기 비동기의 이해
- QoS : ??

```swift
// TrendVC - 트렌드 무비
    func trendMovieCallRequest(completionHandler: @escaping (Result<TrendMovie, Error>) -> Void) {
        let url = MediaAPI.trendURL(type: .movie).url
        let header: HTTPHeaders = [
            "Authorization": Constants.apiKey,
            "accept": "application/json"
        ]
        let para: Parameters = [
            "language" : "ko-KR",
            "time_window" : "week"
        ]
        AF.request(url, method: .get, parameters: para, headers: header).responseDecodable(of: TrendMovie.self) { response in
            switch response.result {
            case .success(let value):
                completionHandler(.success(value))
            case .failure(let error):
                completionHandler(.failure(error))
                
            }
        }
    }
    
    func trendTVCallRequest(completionHandler: @escaping (Result<TrendMovie, Error>) -> Void) {
        let url = MediaAPI.trendURL(type: .tv).url
        let header: HTTPHeaders = [
            "Authorization": Constants.apiKey,
            "accept": "application/json"
        ]
        let para: Parameters = [
            "language" : "ko-KR",
            "time_window" : "week"
        ]
        AF.request(url, method: .get, parameters: para, headers: header).responseDecodable(of: TrendMovie.self) { response in
            switch response.result {
            case .success(let value):
                completionHandler(.success(value))
            case .failure(let error):
                completionHandler(.failure(error))
                
            }
        }
    }
```


```swift
typealias trendingnHandler = ([TrendMovie]?, String?) -> Void
```

![[스크린샷 2024-06-26 오전 11.52.14.png]]


##### 현재의 한계 
- 네트워크 요청 모델: Router Pattern
- 아쉬운점 : ResponseDecodable 에 있는 Model.self 가 해결이 어려울 수 있음. 제네릭과 메타타입 개념으로 해결할 수 있음!

---
#### URLSession
1. request 
	1. header
	2. body
	3. auth
	4. parameter
2. response
	1. configuration : 환경 셋팅
		1. shared 세션
		2. default
		3. Ephemeral
		4. Background
	2. Task
		1. data
		2. upload
		3. download 
	3. Response
		1. completionHandler(closure)
		2. delegate

> 문서를 올리는데 진행률을 보면서 올리고 싶다 " 3,3,2"의 구조를 선택
> 문서를 올리는데 그러면서 딴 작업을 하고 싶다 "4,3,2"의 구조를 선택

`URLSession.shared.dataTask(with: **<#T##URLRequest#>**)`  : 진행률 보면서 시작
