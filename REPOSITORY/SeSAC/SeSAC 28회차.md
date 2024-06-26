#강의노트 #네트워크 

#### 네트워크 결과를 `잘`  핸들링 하는법
##### 실패의 경우도 DispatchGroup 에 넘긴다.

![[스크린샷 2024-06-26 오전 9.39.51.png]]![[스크린샷 2024-06-26 오전 9.45.01.png]]
##### 실패의 경우도 튜플타입으로 DispatchGroup 에 넘긴다.
![[스크린샷 2024-06-26 오전 9.57.36.png]]

#### 동기 비동기의 이해
- QoS : 


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