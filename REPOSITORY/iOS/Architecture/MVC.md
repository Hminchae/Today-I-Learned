### 약자 의미
- MVC : Model View Controller
- SVO : Service Value Object
- APP : Application
- BIZ : Business
- DQM : Data Query Module
	- 데이터베이스에서 데이터를 조회하는 기능을 담당하는 모듈
- DEM : Data Elementary Module
- DAO : Data Access Object
	- 데이터 접근 객체 :  데이터베이스와의 상호작용을 추상화하여 데이터를 저장하고 불러오는 역할(데이터 추가, 수정, 삭제)
- DVO : Data Value Object
- SVO : Service Value Object
	- 서비스 값 객체, 서비스 레이어에서 사용되는 데이터 객체, 서비스와 관련한 데이터 및 로직을 포함함
- VO : Value Object
	- 값 객체, 주로 불변 데이터 값을 나타내는 객체, 시스템 내에서 데이터를 이동시키는데 사용됨
- CFG : Configuration
	- 설정파일(구성) : 소프트웨어 시스템의 설정 및 환경 정보를 포함함

![[Pasted image 20240903114334.png]]
### MVC 패턴이란

컴퓨터공학에서 소프트웨어 설계와 아키텍처를 위한 디자인 패턴 중 하나. 주로 UI(사용자 인터페이스)를 가진 응용 프로그램에 사용된다. 애플리케이션 개발과 유지보수를 쉽게 하기 위하여 데이터, 프레젠테이션, 프로세싱을 분리한 패턴이다. MVC는 모델, 뷰, 컨트롤러로 구성되는데, 각각은 다음과 같다.

#### Model(모델)
모델은 애플리케이션의 핵심 데이터와 비즈니스 로직을 나타낸다. 데이터 저장소와의 상호작용과 데이터 처리 및 유효성 검사같은 작업을 수행한다. 모델은 독립적으로 작동하고 뷰, 컨트롤러와 직접적으로 통신하지 않는다.
#### View(뷰)
사용자에게 보여지는 UI. 모델에서 데이터를 받아 사용자에게 표시하고, 사용자의 입력을 컨트롤러에게 전달한다. 뷰는 애플리케이션의 데이터 표시와 관련한 모든 작업을 처리함.
#### Controller(컨트롤러)
컨트롤러는 사용자 입력을 처리하고 애플리케이션의 흐름을 관리한다. 뷰에서 전달된 사용자 입력을 분석하고, 적절한 모델 기능을 호출하여 데이터를 조작하거나 업데이트 한다.

### 설계 원칙
##### 1. 각 구성 요소의 역할과 책임을 명확하게 구분한다.
모델, 뷰, 컨트롤러는 독립적으로 작동하고 각각의 역할에 집중하여야 함
##### 2. 구성 요소간의 결합도 최소화
결합도 최소화를 위하여 구성 요소간의 직접적인 참조를 피하고, 각 구성 요소는 다른 구성 요소와의 의존성을 최소화 하여야 함
##### 3. 코드의 재사용성과 확장성 고려
각 구성 요소는 독립적이고 재사용 가능한 모듈로 개발되어야 함. 공통 기능이나 코드를 재사용하기 쉬운 구조로 개발하여, 비슷한 요구사항이 있는 다른 프로젝트에서도 사용할 수 있도록 하여야 함

