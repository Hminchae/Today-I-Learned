#### 코드로 UI 구성하기
- 뷰 객체 프로퍼티 선언
- `ViewDidLoad`에서 `addsubView`
##### Autoresizing Mask 
> 동적인 레이아웃을 구성할 수 있도록 Apple 이 도입한 예전방식의 기능. 부모뷰가 커지거나 작아짐에 따라 서브뷰의 크기나 의치를 조정하는 방식을 결정하게 되는 레이아웃

##### system Color ? -> 해당 모드에 어울리는 색으로 바뀜

| 네비게이션 컨트롤러 있을 때 뷰의 시작점                                             | 모달                                                                 | `toItem:view.safeAreaLayoutGuide`                                  | `NSLayoutConstraint`                                               |
| ------------------------------------------------------------------ | ------------------------------------------------------------------ | ------------------------------------------------------------------ | ------------------------------------------------------------------ |
| ![[Simulator Screenshot - iPhone 15 - 2024-06-04 at 10.36.17.png]] | ![[simulator_screenshot_A08C4628-AD7A-4124-8EBC-CDCE26CDFCB0.png]] | ![[simulator_screenshot_A9470665-F5FD-450F-B947-C5B206879F93.png]] | ![[simulator_screenshot_CD9022F2-F494-4F33-8D76-B3D8939EFAD7.png]] |
#### 스냅킷
[스냅킷 독](https://snapkit.github.io/SnapKit/docs/)
