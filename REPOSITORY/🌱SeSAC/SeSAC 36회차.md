#네트워크통신과MVVM
### 어제의 복습
```swift
    struct Input {
        // 처음에 로드
        var inputViewDidLoadTrigger: Observable<Void?> = Observable(nil)
        var inputAddButtonTapped: Observable<Void?> = Observable(nil)
        // 전체 삭제
        var inputRemoveButtonTapped: Observable<Void?> = Observable(nil)
    }
```

-> 프로퍼티가 너무 많아지면 struct 를 통해 묶을  수 도 있다. 

### 뷰모델을 더 잘 써보기

```swift
viewModel.outputMarketData.bind { market in
            self.navigationItem.title = market.first?.korean_name
            self.searchBar.text = market.first?.english_name
            self.tableView.reloadData()
        }
```

##### ⬇️﹦위 코드는 뷰모델을 통해 아래처럼도 만들 수 있다. 
![[스크린샷 2024-07-10 오전 10.39.01.png]]

##### ⬇️﹦위 코드는 네트워크 로직을 싱글턴으로 분리하여 아래처럼도 만들 수 있다. 

![[스크린샷 2024-07-10 오전 11.01.58.png]]