키워드: #AnyObject #강의노트  #새싹  #protocol
#### ReuseProtocol
- UIKit 에서만 사용하고 싶고, 클래스 에서만 쓰고 싶다면? -> AnyObject를 사용한다.
- ![[스크린샷 2024-06-03 오전 9.42.23.png]]
###### Any 와 AnyObject

| Any?                                | AnyObject                           |
| ----------------------------------- | ----------------------------------- |
| ![[스크린샷 2024-06-03 오전 9.45.30.png]] | ![[스크린샷 2024-06-03 오전 9.46.20.png]] |
###### 타입으로서의 프로토콜(Protocol as Type)

| 프토로콜 미채택                             | 프로토콜 채택                              |
| ------------------------------------ | ------------------------------------ |
| ![[스크린샷 2024-06-03 오전 10.01.02.png]] | ![[스크린샷 2024-06-03 오전 10.01.33.png]] |


```swift
class Jack: Mentor { }
class Hue: Mentor { }

struct Bran: Mentor { }
struct Den: Mentor { }

protocol Mentor { }

class ViewController: UIViewController {
    
    @IBOutlet weak var tableView: UITableView!
    
    var sample: Mentor = Jack()
    
    override func viewDidLoad() {
        super.viewDidLoad()
        
        sample = Den()
        
        configureTableView()
    }
    
    // self: 클래스의 인스턴스
    // delegate, datasource 프로퍼티는 프로토콜 자리...
    // 타입으로서의 프로토콜(Protocol as Type)
    func configureTableView() {
        tableView.delegate = self
        tableView.dataSource = self
        let xib = UINib(nibName: BasicTableViewCell.identifier, bundle: nil)
        tableView.register(xib, forCellReuseIdentifier: BasicTableViewCell.identifier)
        
        tableView.rowHeight = 80
        tableView.separatorColor = .red
    }
}
```

###### 열거형과 화면 값 전달
> "휴먼 에러 방지" :  컴파일 타임에서 오류 처리가 가능함
> case로 선택지를 만들지만..
> rawValue 설정도 가능
> 멤버와 값의 분리 : rawValue

```swift
enum ViewType: String {
    case add = "추가하기"
    case edit = "편집하기"
}
```

```swift
switch type {
        case .add :
            navigationItem.title = ViewType.add.rawValue
            topTextField.placeholder = "등록할 이름을 입력해주세요"
        case .edit :
            navigationItem.title = ViewType.edit.rawValue
            topTextField.placeholder =  "수정할 이름을 입력해주세요"
        }
```

