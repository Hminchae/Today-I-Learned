#### 유효성 검사

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
