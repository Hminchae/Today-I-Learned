
 CLLocation+Mapkit
 Class/Struct
 Typecasting



####  ✅ Do-Try Catch / Error Handling

```swift
    @objc func checkButtonClicked() { //
        print("우오ㅏ우와아아")
        
        guard let text = userTextField.text else { return }
        
        if validateUserInput(text: text) {
            print("서버통신 허용")
        } else {
            print("서버통신 x")
        }
    }
    
    
    // 1️⃣ 빈값 여부
    // 2️⃣ 숫자 여부
    // 3️⃣ 날짜 형식
    func validateUserInput(text: String) -> Bool {
        guard !text.isEmpty else {
            print("빈값")
            
            return false
        }
        guard Int(text) != nil else {
            print("숫자가 아닙니다...")
            return false
        }
        
        guard checkDateFormat(text: text) else {
            print("날짜 형태가 잘못되었음")
            return false
        }
        return true
    }
    
    func checkDateFormat(text: String) -> Bool {
        let format = DateFormatter()
        format.dateFormat = "yyyyMMdd"
        
        return format.date(from: text) == nil ? false : true
    }
```

> 유효성 검사, 에러 핸들링 ? 

##### 노란 경고
![[스크린샷 2024-06-18 오전 11.00.18.png]]

> **@discardableResult** 를 작성하여 경고를 피할수도 있음

![[스크린샷 2024-06-18 오전 11.02.26.png]]

####  ✅ Decodable
- [JsonValidation](https://jsonlint.com/)
> 사이트에서 json 구조의 유효성을 판단 가능

>keyNotFound(CodingKeys(stringValue: "product", intValue: nil), Swift.DecodingError.Context(codingPath: [], debugDescription: "No value associated with key CodingKeys(stringValue: \"product\", intValue: nil) (\"product\").", underlyingError: nil))

=> 


#### Struct 와 Class
코드, 데이터, 힙, 스택(값)

