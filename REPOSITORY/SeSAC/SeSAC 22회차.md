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

