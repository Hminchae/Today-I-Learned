#네비게이션바 #탭바 #appearance #ScrollView
### Appearance
=> 디자인 일괄 변경

```swift
 let navigationBarAppearance2 = UINavigationBarAppearance()
        navigationBarAppearance2.backgroundColor = .blue
        
        UINavigationBar.appearance().standardAppearance = navigationBarAppearance2
```

![[스크린샷 2024-07-11 오전 10.18.39.png]]
compact => 회전상태 조정

> 하나의 레이블 상태에서 여러 폰트(굵기, 색상)을 쓰고 싶다면? 

```swift
navigationBarAppearance.titleTextAttributes = [
            .foregroundColor: UIColor.white,
            .backgroundColor: UIColor.yellow
        ]
```

> 탭바의 속성을 변경하고 싶다면?

```swift
 let tabBarAppearance = UITabBarAppearance()
        tabBarAppearance.configureWithOpaqueBackground()
        tabBarAppearance.backgroundColor = .white
        
        tabBarAppearance.stackedLayoutAppearance.selected.iconColor = .blue
        tabBarAppearance.stackedLayoutAppearance.selected.titleTextAttributes = [.foregroundColor: UIColor.blue]
        
        tabBarAppearance.stackedLayoutAppearance.normal.iconColor = .blue
        tabBarAppearance.stackedLayoutAppearance.normal.titleTextAttributes = [.foregroundColor: UIColor.orange]
        
        UITabBar.appearance().standardAppearance = tabBarAppearance
```

### ScrollView
- 재사용 매커니즘 동작 X
- 

![[스크린샷 2024-07-11 오전 10.20.31.png]]
> 이거 어떻게 구현? 

1. Collection View
	 - 효율적
	 - 아쉬운점
		 - 로드하는데 시간이 좀 더 걸릴 수 있다.. 
2. ScrollView
	 - 가로스크롤 = 스크롤 영역크기
	 - 💡내부 크기를 알게끔 레이아웃을 구현해주어야 함