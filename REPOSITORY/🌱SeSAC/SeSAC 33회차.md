#카메라 #사진 #캘린더  #사진다루기 #이미지저장 #Realm데이터묶기 

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

```swift
extension AddViewController: PHPickerViewControllerDelegate {
    
    func picker(_ picker: PHPickerViewController, didFinishPicking results: [PHPickerResult]) {
        
        dismiss(animated: true)
        print("1",Thread.isMainThread)
        if let itemProvider = results.first?.itemProvider,
           itemProvider.canLoadObject(ofClass: UIImage.self) {
            itemProvider.loadObject(ofClass: UIImage.self) {
                image, error in
                print("2",Thread.isMainThread)
                DispatchQueue.main.async {
                    self.photoImageView.image = image as? UIImage //➡️ 글로벌 스레드로 보냈기 때문에..
                }
            }
        }
    }
}
```

![[스크린샷 2024-07-04 오전 11.00.53.png]]

#### 사진 저장
1. 갤러리 링크(String)
	- > 삭제가 된다면...??
	- > 앨범을 바꾼다면..?
	- => 여러가지 에러가 날 가능성이 있기때문에 권장되는 방식은 아님
2. defaul.realm 
	- png -> data
	- 1010011010 -> Image -> 010101010 -> Image 비효율적..
3. 이미지 자체를 저장
	- file manager 이용
	- iphone/app.document/jack.png
		1. 도큐먼트 위치 + 2. 경로
		2. => 저장

> 레코드를 지워도 3번방식 시, 파일에 남아있다...  지워주어야 함


![[스크린샷 2024-07-04 오후 12.22.14.png]]
![[스크린샷 2024-07-04 오후 12.25.44.png]]
> 파일을 안 지우고 realm 을 먼저 지웠을때 생기는 오류!!!!!
> id 가 없어져서 .. data.id 가 조회되지 않음


#### 그러면 🚨이렇게 하면/??? 

> ![[스크린샷 2024-07-04 오후 12.26.32.png]]

=> ⬇️ 맨 밑에 있는 레코드는 삭제하면 앱이 터지고, 다른애들은 터지진 않지만 파일에서 삭제 되지 않음
 
![[스크린샷 2024-07-04 오후 12.30.01.png]]

=> ⬆️또한 인덱스가 꼬여 원하는 타겟 이미지가 삭제되지 않을 수 가 있음 ㅠㅠ

### 코드 개선

![[스크린샷 2024-07-04 오후 2.17.53.png]]

