> 어제 복습
> - 테이블 뷰 필수 메서드
- 테이블 뷰
-  heightForRowAt -> 필수 X , 하지만 셀마다 다른 높이를 주고싶을때, indexPA

> 테이블 셀 재사용 때문에 설정한 값이 제대로 반영이 안 되는 경우가 있음 

-> 100퍼센트 모든 경우의 수 대응하도록 기억 

#### 오토레이아웃


**데이터랑 뷰랑 따로논다 -> 바뀌거난 달라지면 뷰에 실시간 반영**


> 데이터와 뷰는 따로 놀기 때문에, 데이터가 달라지면 뷰를 다시 갱신해주어야 한다.
> `tableView.reloadData`


* Constrain to margins : 애플이 권장하는 최소한의 

#### 타입캐스팅 
cell.ti


`reloadData` -> 모든 메서드를 호출하기 때문에 비효율적일 수 있음 

reload ~ 

```swift
tableView.reloadRows(at: [IndexPath(row: sender.tag,
                                            section: 0)],
                             with: .automatic)
``` 