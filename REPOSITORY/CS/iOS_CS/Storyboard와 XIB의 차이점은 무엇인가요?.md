## Storyboard와 XIB
### XIB(XML Interface Builder)
- iOS 앱에서 사용자 인터페이스를 디자인학 구성하기위한 통합 개발 환경.
- XIB를 사용하여 개발자는 스토리보드 같은 인터페이스 디자인 및 개발을 수행할 수 있음
- XIB는 XML 기반의 파일 형식으로 `NIB 파일`로 컴파일되어 iOS 디바이스에서 로드 됨
### NIB(Next interface Builder)
- 인터페이스 디자인을 위한 시각적인 요소들과 그들의 역할을 정의한 객체들을 포함하는 바이너리 파일
- 이 파일들은 `앱 번들의 리소스 디렉토리`에 저장되어 실행 시점에 로드되어 화면에 표시됨


| 분류     | XIB             | Storyboard        | SwiftUI           |
| ------ | --------------- | ----------------- | ----------------- |
| 파일 확장자 | .xib            | .storyboard       | .swift            |
| 호환성    | iOS 2.0+        | iOS 5.0+          | iOS 13+           |
| 레이아웃   | 개별 파일           | 개별 파일             | 코드 기반             |
| 인터페이스  | 드래그 앤 드롭        | 드래그 앤 드롭          | 선언적               |
| 미리보기   | 사용 불가           | Xcode 11+에서 사용 강능 | Xcode 11+에서 사용 가능 |
| 재사용성   | 여러 뷰에서 재사용 가능   | 여러 뷰에서 재사용 가능     | 여러 뷰에서 재사용 가능     |
| 러닝커브   | 쉽게 배울 수 있음      | 중간 정도의 학습 곡선      | 높은 학습 곡선          |
| 성능     | storyboard보다 빠름 | XIB보다 느림          | 둘보다 빠름            |
사용자 관점에서 흐름도는 xib -> UIView -> UIViewController 순으로 전달이 되어 UIViewController -> UIView -> xib로 반환 받음

1. 사용자는 xib 파일을 통해 화면이 보여짐  
2. 사용자는 특정 행동을 위해 xib 파일을 선택하면 매핑된 UIView로 이벤트 처리가 수행됨 
3. 이벤트 처리가 완료된 뒤 UIViewController에서 이벤트를 수신하여 데이터 처리 혹은 화면 간의 전환을 수행함
## Storyboard에서 세그(Segue)를 사용하는 이유는 무엇인가요?


### 
## Storyboard 참조(Storyboard Reference)의 장점은 무엇인가요?

## 참고
- [XIB 이해 하기 : 이론, 파일 생성, 페이지 이동 방법](https://adjh54.tistory.com/164)