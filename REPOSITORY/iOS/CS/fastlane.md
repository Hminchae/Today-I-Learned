fastlane은 앱의 베타배포와 릴리즈를 자동화 시켜주는 프로그램이다.

일반적으로 배포를 할때엔 Xcode -> Archive -> Xcode Upload -> AppStoreConnect Metadata 정보 업데이트 등 여러가지 절차가 필요한데, fastlane 을 이용하면 단 한 줄로 배포가 가능하다.

### 설치
다양한 방법으로 설치가 가능하지만 가장 선호되는 방법은 Bundler을 통한 방법이다.
Bundler와 Gemfile을 이용하여 fastlane 의존성 관리를 해준다.

유니버셜 링크 : 사용자가 url 을 클릭하면 즉시 앱으로 서비스가 연결되는 기능