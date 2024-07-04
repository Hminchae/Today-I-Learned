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

#### 마이그레이션

#### Transaction
> 작업 수행의 논리적 단위 For 데이터 정확성

- ACID
	- Atomicity
		- All OR Nothing : Transaction의 작업이 부분적으로 실행되거나 중단되지 않는 것을 보장
	- Consistency
		- Transaction이 성공적으로 완료되면 일관적인 DB상태를 유지하는 것
		- 정해진 규칙에 의해서만 수정이 가능한 특성
	- Isolation
	- Durability
		- 한번 수행된 Transaction은 영원히 적용되는 특징

#### Realm 특징 정리
- NoSQL
- 객체 중심 데이터베이스 -> ORM 필요하지 않고 직관적
- iOS - Android 간 DB 공유 가능
- 코드로 작업할 수 있음 -> 중간 쿼리 X
- 메인 스레드에서 읽기/ 쓰기 가능 -> 다중 쓰레드에서의 Realm 객체 관리가 어려움(쓰레드별 객체 관리 필요함)
- 객체를 직접 디스크에 유지함 
	- -> 서드파티 스토리지 엔진을 사용하지 않음
	- -> 디스크에서 데이터를 읽거나 쓸 때 데이터를 상호 변환하지 않아도 됨
- SQLite와 CoreData보다 작업 속도가 빠름
- 다양한 쿼리를 지원하지 않음
- iOS 8 이상부터 사용 가능
### 이번주를 정리하며 .. 
1. URLSessionDelegate
2. final, wmo
3. Realm
#### 주말 과제
- [ ] 리마인더....
- [ ] DB써서 데이터 쌓기 .........