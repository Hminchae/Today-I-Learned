### 1. CoW(Copy-on-Write)
CoW가 뭘까요? Swift를 포함한 모든 프로그래밍에서 쓰이는 기술 중 하나임
컴퓨터 프로그래밍에서 복사 동작을 할 때, 실제 원본이나 복사본이 수정되기 전까지는 복사를 하지 않고 원본 리소스를 공유함. 원본이나 복사본에서 수정이 일어날 경우, 그 때 복사하는 작업을 함!

Swift 에선 Collection Type(`Array`, `Dictionary`, `Set`)과 String Type을 복사해서 사용할 때 일어난다.

예를들어, `var array1: [String] = ["명현", "동호", "소혜", "팡햄"]` 같은 배열이 있고, `var array2: [Int] = array1` 이런식으로 대입하게 되면 배열은 구조체 형식이기 때문에 값 복사가 일어난다. 이렇게 되면 `array2` 는 새로운 메모리를 할당해서 `["명현", "동호", "소혜", "팡햄"]`를 들고 있을거라 생각하는게 학계의 정설임.

하지만 CoW 를 쓰면 ?? 바로 복사하지 않음

`array2` 가 `array1`을 참조하고 있는 형태가 됨. 이러다가 원본인 `array1`이나 복사본 `array2` 둘 중 하나를 수정하게 된다면! 이 때 비로소 진짜 복사 과정이 일어나 `array2`의 값이 메모리에 할당되게 됨

![[스크린샷 2024-04-29 오후 10.48.19.png]]

이런식으로! 메모리 주소가 같은곳을 보고 있다가 새로운 값을 쓰게 되었을 때 비로소 메모리가 할당 되는 걸 볼 수 있음

### 2. 사용 용도
수정을 하지 않고 그냥 복사만 해서 가지고 있을 때, 메모리를 많이 차지하지 않고 더 효율적으로 사용할 수 있음. **실제 수정이 이뤄질 때 복사를 하고 그 전엔 참조를 통해 불필요한 복사를 줄이자!** 이게 바로 CoW의 장점이자 사용이유라 함

Swift에서, Value Type의 복사는 `깊은 복사 방식`을 사용하는데 Collection Type 같은 경우는 Value Type 이지만, heap 영역에 생성되어 매번 깊은 복사 방식을 사용하면 높은 메모리 오버헤드를 발생시킬 수 있다함. 이를 방지하기 위하여 Collection Type 의 경우 복사한 데이터의 수정이 발생하지 않는다면, `얕은 복사`와 같이 heap영역에 생성된 데이터의 주소값만 공유하고 있다가, 값이 변경이 발생했을 때 깊은 복사를 사용하는 방식을 채택하여 메모리를 효율적으로 관리할 수 있다함 ~ 

- 깊은 복사?
	Swift에서 Value Type 복사 시 사용하는 방법, 데이터 자체를 복사하여 독립적인 메모리 공간을 차지하게 하여 복사본을 수정하여도 원본에는 영향이 가지 않음.
- 얕은 복사?
	Swift에서 Reference Type 복사 시 사용하는 방법, 가리키고 있는 인스턴스의 주소값만 공유하여 같은 인스턴스를 가리키게 하는 방식, 복사본 수정 시 원본 데이터에도 영향이 간다.
### 3. 배열 외 다른 타입들에서는?
![[스크린샷 2024-04-29 오후 11.29.51.png]]
	공식문서에 따르면 표준 라이브러리의 모든 가변 크기 Collection이, Copy-on-Write 방식을 사용한다고 명시되어 있음. 정말 그럴까 각각 실험해보겠음
#### 1) Dictionary, Set
![[스크린샷 2024-04-29 오후 11.48.17.png]]
	엥 왜이럼? .. 주소가 변경이 일어나기도 전에 다른걸 확인할 수 있었음. 역시 마음대로 되는게 없다 ~ 공식문서에서 CoW가 구현되어 있다는 것을 명시해 놓았기 때문에 많이 이상함.. 저 문자열을 저장하기에 8바이트는 부족하다는 점을 고려하고, 배열과는 다르게 한 번 Wrapping이 되어있다는 점 때문에 다른 주소값을 저장하는게 아닐까 추측을 해본다는데 이 얘기가 뭔 얘긴지 난 모르겠다.
#### 2) String 
String의 경우엔 15글자를 초과할 때와 이하인 경우가 저장 동작이 다르다 함
- 15글자 이하의 경우
	![[스크린샷 2024-04-29 오후 11.58.35.png]]
		다른 주소에 저장되는걸 볼 수 있음
- 15글자 초과의 경우 : Heap 영역 저장 -> CoW 를 쓰는게 맞..음..!
	![[스크린샷 2024-04-30 오전 12.06.02.png]]
		근데 나는 다른 주소를 가지는걸로 나오는데..?
#### 3) Struct
구조체를 한번 확인해보겠음
![[스크린샷 2024-04-29 오후 11.39.33.png]]
	흠 그렇군, 수정이 되기전에 이미 다른 메모리주소를 가지는걸 볼 수 있다. 

그렇다면 사용자 정의 구조체에 CoW를 구현하고 싶으면 어떻게 하면 될까?
```swift
class Ref<T> {
    var val: T
    init(_ v: T) { val = v }
}

struct Box<T> {
    var ref: Ref<T>
    init(_ x: T) { ref = Ref(x) }
    
    var value: T {
        get { return ref.val }
        set {
            // 유일하게 참조되는지 확인
            if (!isKnownUniquelyReferenced(&ref)) {
                ref = Ref(newValue)
                return
            }
            ref.val = newValue
        }
    }
}
```
이렇게 struct 내부에 class 인스턴스를 저장 프로퍼티로 소유하고, 그 인스턴스 내부에 프로퍼티로 원본 데이터를 저장함. 그리고 getter에서는 참조의 데이터를 그대로 반환하지만, setter에서 유일하게 참조되고 있는지를 확인하고! 아니라면 새로운 참조 인스턴스를 생성해서 반환하도록 구현하면 된다.
### 3. 작업시간은 어떨까

그렇다면 실제 복사가 일어나는 첫 수정 작업의 코드가 CoW 때문에 실행시간이 더 걸릴 것 이라는 예측으로 코드를 실행해 봤음.. 
![[스크린샷 2024-04-29 오후 11.04.52.png]]

엥 근데 왜이럼? 분명 소들좌의 블로그에선 첫번째 수정 작업 때 작업시간이 더 걸린단말임..혹시 몰라서 작업 시간을 측정하는 다른 방법도 사용해봤지만

![[스크린샷 2024-04-29 오후 11.10.47.png]]
어엄,,, 시도마다 다른 결과가 나옴. 너무 작은 데이터라서 이런 결과가 나왔을 수 도 있고,, 이 경우는 다른분들의 생각이 궁금하네요. 

### 4. 한 걸음 더..
이대로 끝내기는 아쉬워서 운영체제의 내용을 가지고 왔어요..

#### OS에서 Copy On Write(메모리를 절약하기 위한 방법)
원래 OS에서 많이 쓰인 표현이라 함. 부모 프로세스가 자식 프로세스를 fork할 때, 기본적으로 부모 프로세스의 address space를 자식 프로세스의 address space로 copy해서 완전히 동일함. 이 때 process를 create해서 자식 process의 address space 공간이 만들어지고, 그 공간에 부모 process의 address space를 memory copy로 전부 카피하는 것은 아주 큰 Overhead가 발생함

실제로 어떻게 발생하는지 이해하기 위해서는 OS에서 사용하는 `Virtual Memory`, `Page Table`, `Page` 에 대한 개념을 어느정도 숙지하여야 함. `Virtual Memory` 는 저번에 내가 다뤘기 때문에ㅎㅎ간단하게 정리하겠음

1) `Virtual Memory`
	 cpu가 메모리에 접근할 때, 현재 수행하고 있는 코드와 그에 따른 필요한 데이터를 접근함.
	 결국 cpu 입장에서는 자신이 실행하여야할 instruction과 접근 해야할 데이터만 memory에 올라와 있다면 문제가 없음. 그래서 이론상으론 "모든 프로세스의 address space 메모리에 올라와있는 상태에서 프로그램이 실행되어야 함"라는 과정을 하고 있음

	 그러나 실질적으로 cpu가 접근하는 부분은 현재 실행하는 코드와 연관된 데이터로 한정됨.
	 따라서 cpu가 접근하는 부분만 있으면 되고, 그것이 실제로 문제가 없다면 동시에 실행할 수 있는 프로세스의 수가 증가함. 만약 메모리가 32GB이고 하나의 프로세스 용량이 16GB 라면? 두가지 프로그램 밖에 메모리에 올리지 못함, 하지만 실제로 사용하는 데이터들은 순간적으로 최대 1GB를 넘지 않는다면 32개의 프로세스를 올리는 것이 가능함!

	 때문에 메모리 활용성을 극적으로 높이기 위함이 바로 virtual memory 다~ 라고 이해하면 됨
2) `Page`, `Page Table`
	 process(프로그램이 동적인 상태에 있을 때의 의미)는 address space를 가지고, 이건 memory에 올라와 있음.  address space는 Page 단위로 쪼개지며 이것들은 비연속적인 구조를 지님. address space가 비연속적으로 이루어져있기 때문에 page Table이란 것을 가지고, 이를 통해서 mapping되어 있는 구조임. 결국 page Table은 page들을 가르키고 있고, page Table은 page은 logical Address로서 실제로 메모리에 없을 수 있는 것들도 포함함

	 page는 실제 physical memory에 존재하는 데이터들임
3) `Copy on Write in OS`
	 결국 Virtual memory 를 각자의 프로세스는 가지고 있으며, page Table은 page를 가르키고 있음. 
	 
	 fork시 자식 프로세스는 반드시 부모 프로세스를 그대로 copy 해야 할까? 부모 process와 동일한 address space를 자식 process가 사용할 수 있도록 page Table 을  동일하게 만들어줌! page Table이 copy되기 때문에 그렇게 하면 memory copy overhead가 엄청나게 줄어듬
	 
	 *copy가 이루어지는 상황* 
	
	 나중에 address space의 부모나 자식 둘 중 아무나 데이터를 write 했다면? 
	 자식 process가 exec 시스템 call 을 이용해서 address space를 바꾸려고 한다면 바꿔주어야 함. 또는 자식 프로세스가 부모하고 똑같은 일을 해서 address space를 갈아 엎을 필요가 없더라도 부모가 자신의 address space에 write하면 physical memory에 write하면 자식까지 영향을 미치게 됨. 누군가가 공유하고 있는 page에 write를 하면 그제서야 copy를 만들어서 그 copy본에 write를 하게 되기 때문에 "Copy on Write"라는 말이 붙게 되어 되었음

### 5. 결론
> 값 타입임에도 불구하고 컴파일 타임에 정확한 사이즈를 알기 어려운 가변 길이를 가진 Collection Type과 String Type은 Heap에 데이터를 저장하여 사용하기 때문에 매번 깊은 복사를 사용하기에는 높은 메모리 오버헤드가 발생할 수 있음
> 
> 따라서 Copy on Write를 통해 데이터의 변화가 발생하기 전까지는 얕은 복사처럼 동작하다 원본이나복사본의 변화가 생기면 깊은 복사를 수행하여 메모리를 효율적으로 사용할 수 있다~!
> 
> 공식문서에 명시되어 있지 않은 컬렉션 타입들도, CoW의 목적에 비춰볼때 구현되어 있다고 생각함이 타당한듯  + Struct는 기본적으로 COW 동작이 구현되어 있지 않아서, 필요하다면 커스텀하게 구현해 주어야 한다

### 🥕참고
- [Swift) COW (Copy-on-Write)](https://babbab2.tistory.com/18)
- [COW(Copy-on-Write)](https://forestjae.tistory.com/30)
- [Apple - Array](https://developer.apple.com/documentation/swift/array/)
- [COW(Copy On Write) - 메모리 절약 방법 - Structure 응용편, OS응용편](https://yudonlee.tistory.com/33)