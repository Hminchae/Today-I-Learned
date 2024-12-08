## 개념
### 게임 엔진?
 비디오 게임의 개발에 기반이 되는 구성 요소들을 가진 필수 구성 요소들인 그래픽 엔진, 물리 엔진, 오디오 엔진, UI 시스템, 게임 플레이 프레임워크 등이 잘 융합된 상태의 소스코드와, 그 기능들을 사용 가능한 툴을 겸비한 게임 개발 소프트웨어

### SpriteKit
- 2013년 wwdc에서 발표된 맥 생태계 전용 2D 게임 개발용 API
- Cocos2d와 유사한 구조를 가짐
- iOS에 최적화, Metal API를 지원하며 빠른 속도
- iOS의 라이브러리를 자유롭게 가져다 쓸 수 있음
- 고수준 언어인 Swift로 코딩 가능
- 간단한 2D게임을 빠르게 개발
- Apple 생태계 밖에서는 사용 불가

### SpriteKit의 구조
- 뷰컨트롤러 위에서 미리 준비되어 있는 씬을 바꿈으로써 화면을 전환
- 모든 노드는 SKNode의 하위 클래스
- SKLabelNode, SKSpriteNode, SKShapeNode, SKEmitterNode, SKEffectNode, SKCropNode...
- ,,,,ㅠㅡㅠ ㅡㅜ 