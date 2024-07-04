#카메라 #사진 #캘린더  #사진다루기 

#### 권한
- 카메라
- 갤러리

> iOS 14 기점으로 나뉜 사진 다루기

iOS 14 이전
	- ImagePicker Controller
		1. 촬영
		2. 갤러리
		3. 갤러리 사진 저장

```swift
// ✅UIImagePickerController: 촬영/ 갤러리
    // ➡️단순히 갤러리를 보여주고 가져오는 부분은 권한 필요 ❌
    // ➡️➡️➡️언제 찍었냐 어디서 찍었냐 렌즈가 뭐냐 -> 권한 필요 🅾️
    // ➡️➡️➡️이미지를 갤러리에 저장하고 싶을 대도 권한 필요 🅾️

@objc func addButtonClicked() {
        print(#function)
        // - 사진
        let picker = UIImagePickerController()
        picker.delegate = self
        picker.allowsEditing = true
        picker.sourceType = .camera //🧡
        present(picker, animated: true)
    }
```
- iOS 14 이후
	- PHPickerController
		- 갤러리, 여러장
