### 함수와 변수

- 클래스 내에서
	- 함수 -> 메서드
	- 변수 -> 프로퍼티

> 탬플릿처럼 사용할 네비게이션 타이틀 코드!

```swift
let menu = UIBarButtonItem(
            image: UIImage(systemName: "heart.fill"),
            style: .plain,
            target: self,
            action: #selector(starButtonClicked))
```

### 얼럿과 액션시트

#### 얼럿
> 중간에 뜸

빨간색 - distructive
파란색 - default
Cancel 스타일 - 볼드
![[스크린샷 2024-05-22 오전 3.40.27.png]]
액션시트
> 아래에서 올라옴

시트안에 뷰 구성도 가능

```swift
@objc func profileButtonClicked() {
        print(#function) // -> 함수의 이름이 출력되게 됨
        
        // 1. 얼럿 만들기
        let alert = UIAlertController(
            title: nil,
            message: nil,
            preferredStyle: .actionSheet)
        
        // 2. 아이템 만들기
        let open = UIAlertAction(
            title: "열기",
            style: .default) // handler 같은 경우는 누워있는데, 얘는 써도 되고 안 써도 되어서 그렇다
        let delete = UIAlertAction(
            title: "삭제",
            style: .destructive)
        let cancel = UIAlertAction(
            title: "취소",
            style: .cancel) // 스타일 .cancel 두번쓰면 오류난다
        
        // 3. 위치 지정.. 이지만 취소의 경우 아래로 내려감
        alert.addAction(cancel)
        alert.addAction(delete)
        alert.addAction(open)
        
        // 4. present
        present(alert, animated: true)
    }
```
![[스크린샷 2024-05-22 오전 3.42.28.png]]
- 타이틀과 message에 nil 할당
![[스크린샷 2024-05-22 오전 3.43.00.png]]

#### 그 외
- UIActivityViewController
- UIMenuController
- UIDocumentPickerViewController
- UIFontPickerViewController
- UIColorPickerViewController(iOS14)