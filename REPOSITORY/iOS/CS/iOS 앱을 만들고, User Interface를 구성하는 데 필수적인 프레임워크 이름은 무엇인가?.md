

## Cocoa Touch Framework

ios앱을 만드는데 필요한 여러 개발도구를 포함하는 최상위(가장 프로그래머와 가까운) 프레임워크

![image](https://github.com/Apple-CS-interview/iOS-CS-interview/assets/103357078/f4fb3017-3864-46af-832b-85d137e33fd0)

먼저 `코코아(Cocoa)`라는 단어는, `NSObject`를 상속받는 모든 클래스, 모든 객체를 가리킬 때 사용하는 단어다.

초기에 애플이 NeXT에서 이걸 샀을 때는 블루 박스라고 불리다가. 이제는 코코아라 불린다. [Objective-C](https://namu.wiki/w/Objective-C)에는 [C++](https://namu.wiki/w/C%2B%2B) 같은 네임스페이스가 따로 없기 때문에, 충돌을 피하기 위해 보통 클래스의 이름 앞에 Prefix를 붙인다. Foundation Kit 프레임워크 클래스들은 덕분에 이름앞에 죄다 NS([NeXTSTEP](https://namu.wiki/w/NeXTSTEP)에서 따와서 NS)를 붙여놓았다. NSString이라든지 NSArray라든지.

코코아라는 이름은 그당시 지금이상으로 핫했던 언어인 Java가 커피원산지에서 따온 이름이기 때문에, 애플 개발자는 어린아이도 할 수 있는 자바(Java for kids)라는 의미에서 코코아라고 이름지었다고 한다.

코코아 터치는 애플이 아이폰, 아이패드, 아이팟터치와 같은 제품의 소프트웨어 애플리케이션을 구축하기 위해 제공하는 사용자 인터페이스 **프레임워크**다. 주로 Object C 언어로 작성되었으며 Mac OS X에 기반을 두고 있다. 코코아 터치는 모델 뷰 컨트롤러 소프트웨어 아키텍처를 기반으로 개발되었다. 코코아 터치에서 이용할 수 있는 높은 수준의 응용 프로그램 프로그래밍 인터페이스는 애니메이션, 네트워킹, 그리고 코드 개발을 덜 하고 개발된 응용 프로그램에 기본 플랫폼의 모양과 동작을 추가하는 것을 돕는다.

참고로 비슷한 이름의 `코코아 프레임워크`는 `macOS` 개발 환경을 위한 프레임워크라고 한다. 그렇기 때문에, 아이폰, 아이패드 등의 터치기반의 iOS 개발환경에 `코코아 터치 프레임워크`라는 이름이 붙게된 것 같다.

import

**CoreData**

- [https://zeddios.tistory.com/989](https://zeddios.tistory.com/989) → _**나중에 읽기**_

**UIKit**

UIKit 프레임워크는 사용자의 인터페이스를 관리하고, 이벤트를 처리하는게 주 목적인 프레임워크다.

- UIViewController 같은애들을 쓰기 위해 필요
- _MacOS X의 UI를 담당하고 있는 AppKit_ 와 다른 점은 Mac OS X에서 사용하는 클래스와의 혼동을 막기 위해 ‘UI’로 시작하는 클래스 이름을 사용합니다.
- Mac OS X에서는 ‘NS’로 시작하는 클래스의 이름을 사용합니다. ( NS : NeXTSTEP )

**Foundation**

- 프로그램의 중심을 담당
- Application의 모든 object를 관리하는 기본적인 틀 제공
- 사실 가장 기본적인 `원시 데이터 타입`(String, Int, Double)부터가 `Foundation`에 포함되어있기 때문에, 프레임워크를 상속하지 않으면 아무것도 할 수 없다고 봐도 무방하다.
- 메모리 할당 혹은 반환하는 기본적인 규칙 정의
- 리스트나 딕셔너리와 같은 클래스들은 모두 ‘NS’로 시작

>  왜 Foundation이 아닌 UIKit만 import 해도 동작하는가??

![image](https://github.com/Apple-CS-interview/iOS-CS-interview/assets/103357078/048b1b6e-eb33-4e13-b411-50c9abd7864e)

UIKit은 가장 위인 Cocoa Touch 계층이고 그보다 두단계 Foundation은 Core Service 계층이다. 그렇기 때문에 UIkit이 Foundation 프레임워크를 상속했을 가능성이 높다.결과적으로 UIkit을 상속하는 것 만으로, Foundation도 함께 상속한 결과를 내는 것이다.그렇다고 해서, 모든 상위계층이 하위계층을 포함하고 있다거나, 같은계층끼리의 포함관계가 없는 것은 아니다. 예를들어 같은 계층의 GameKit은 UIkit을 상속하고있고, Foundation은 CoreFoundation을 상속하고 있다.

**Cocoa Touch 계층**

하위 계층의 프레임워크를 사용하여 애플리케이션을 직접 구현하는 프레임워크.UIKit, GameKit, MapKit

**Media 계층**

상위 계층인 코코아 터치 계층에 그래픽 관련 서비스나 멀티미디어 관련 서비스를 제공Core Graphics, Core Text, Core Audio, Core Animation, AVFoundation

**Core Service 계층**

문자열 처리, 데이터 집합 관리, 네트워크, 주소록 관리, 환경 설정 등 핵심적인 서비스들을 제공.또한 GPS, 나침반, 가속도 센서나 자이로스코프 센서와 같이 디바이스의 하드웨어 특성에 기반한 서비스도 제공.Foundation, Core Foundation, Core Location, Core Motion, Core Animation, Core Data

**Core OS 계층**

커널, 파일 시스템, 네트워크, 보안, 전원 관리, 디바이스 드라이버 등이 포함iOS가 운영 체제로서 기능을 하기 위한 핵심적인 영역