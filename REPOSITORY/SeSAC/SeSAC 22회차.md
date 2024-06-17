#폰트

#### 폰트

> 폰트 패밀리와 이름 아는법

```swift
for family in UIFont.familyNames {
            print(family)
            for name in UIFont.fontNames(forFamilyName: family) {
                print(">>> \(name)")
                
            }
        }
```

`logoLabel.font = UIFont(name: "Yeongdeok-Sea", size: 80)`
![[스크린샷 2024-06-17 오전 9.59.41.png]]

#### Notifications
- 권한 허용한 경우 iOS 알림 센터에 표시
- 앱 retention 에 기여
- Remote(Push)
	- 서버에서 알림 전달
	- 다른 시각 & 다양한 콘텐츠
	- ex) 광고, 채팅
- Local
	-  앱내에서 알림을 전달
	- 같은시각 & 비슷한 콘텐츠
	- ex) 일기, 디데이, 알림

| 1. 포그라운드에서도 오도록 설정 가능..                                            |                                                                    |
| ------------------------------------------------------------------ | ------------------------------------------------------------------ |
| ![[simulator_screenshot_2FF42EAD-070A-4354-830F-2E75228644B3.png]] | ![[simulator_screenshot_724BE22F-B76F-49CA-BEC2-1A3C992ED063.png]] |

##### 예시 코드
```swift
extension AppDelegate: UNUserNotificationCenterDelegate {
    
    // 포그라운드에서 알람을 받고 싶을 때(willPresent)
    // ex. 특정화면에서는 안 받고 싶어!
    // ex. 카카오톡.. Jack:Den
    // ex. 친구랑 1:1 채팅할 경우. 다른 단톡방이나 다른 갠톡방 푸시만 오는 것 처럼, 특정 화면/ 특정 조건에 대해서 포그라운드 알림을 받게 설정하는 것도 가능
    func userNotificationCenter(_ center: UNUserNotificationCenter, willPresent notification: UNNotification, withCompletionHandler completionHandler: @escaping (UNNotificationPresentationOptions) -> Void) {
        
        completionHandler([.banner, .badge, .list, .sound])
    }
}
```

```swift

    func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
        
        // ✏️ 알림권한 설정
        UNUserNotificationCenter.current().requestAuthorization(options: [.alert, .sound, .badge]) { success, error in
            print(success, error)
        }
        
        UNUserNotificationCenter.current().delegate = self
        return true
    }
```

##### 🚨 Notification 관련 정책
 - identifier: 고유값 / 64개까지만
 - TimeInterval: 60초 이상이어야 반복 가능
 - foreground 에서는 알림을 뜨지 않는 것이 default
 - Foreground 에서 알림을 받고 싶다면 별도 설정(delegate)필요
 - 알림센터에 보이고 있는지, 사용자에게 전달되었는지 알 수 없음
 - 단, 사용자가 알림을 `클릭`했을 때만 확인 가능(delegate)