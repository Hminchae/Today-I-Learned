**1. userInteractive**

- main thread에서 작업, 사용자 인터페이스(UI) 새로고침 또는 애니메이션 수행과 같이 사용자와 상호작용 하는 작업
- 작업이 신속하게 수행되지 않으면, UI가 중단된 상태로 표시될 수 있음
- 반응성(responsiveness)과 성능(performance)에 중점을 둡니다.
- Duration of work to be performed - 순식간에 끝난다.(Work is virtually instantaneous.)

**2. userInitiated**

- 사용자가 시작한 작업이며, 저장된 문서를 열거나, 사용자 인터페이스에서 무언가를 클릭할 때 작업을 수행하는 것과 같은 즉각적인 결과가 필요
- 사용자 상호작용을 계속하려면 작업이 필요합니다. (The work is required in order to continue user interaction) 반응성과 성능에 중점을 둡니다.
- Duration of work to be performed : 거의 순식간이며, 몇 초 또는 그 이하입니다.

**3. default**

- QoS의 priority level은 user-initiated와 utility사이에
- 이 QoS는 개발자가 작업을 분류하는데 사용하기 위한 것이 아님, QoS정보가 할당되지 않은 작업은 Default로 처리되며 GCD global queue는 이 level(default)에서 실행됩니다

**4. utility**

- 작업을 완료하는 데 약간의 시간이 걸릴 수 있으며, 데이터 다운로드 또는 import와 같은 **즉각적인 결과가 필요하지 않음**
- 유틸리티 작업에는 일반적으로 사용자가 볼 수 있는 progress bar가 있음, 반응성, 성능 및 에너지 효율성 간에 **균형을 유지하는 데 중점**

**5. background**

- 백그라운드에서 작동하며, indexing, 동기화 및 백업과 같이 **사용자가 볼 수 없는 작업**
- 에너지 효율성에 중점
- Duration of work to be performed : 작업은 분(minutes) 또는 시간(hour)과 같은 상당한 시간(significant time)이 걸림

**6. unspecified**

- 이는 QoS정보가 없음을 나타내며, 환경 QoS(environmental QoS)를 추론해야 한다는 단서를 시스템에 제공
- 쓰레드가 기존(legacy) API를 사용하는 경우, Unspecified QoS를 사용할 수 있으며, 이경우 쓰레드가 QoS를 벗어날 수 있음