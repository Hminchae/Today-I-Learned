#폰트

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