#git #강의노트 #bit #CS 
- GB != GIB
- 비트와 바이트의 차이

- on/off 가 일어나는 연산이 1hz 

### Re: GIT
> istributed Viersion Control Systems

- Git 은 VCS의 일종
- CVCS vs DVCS
	- CVCS
		- Delta방식
	- DBCS : git
		- 코드를 분산적으로 관리
		- 스냅샷 + 델타 방식
- Git 의 장점
	- 코드를 분산
	- 네트워크 X
	- 깃의 용량 관리는 최근 것은 스냅샷 기반으로 관리하고 오래된 것은 델타로 관리함

> 델타 방식 : 파일의 변화만 체크하여 차이점 인식해서 관리
> 스냅샷 : 특정 시점의 파일과 디렉토리 상태를 그대로 사진찍듯 관리 

#### Git Add
Untracked ->ADD -> Tracked

- 커밋 메세지는 항상 친절하게 자세히!
	- 그렇다고 일기는 ㄴ
- 커밋 당ㄴ위에 항상 신경쓰려고 노력해야 함 
	- 작업하다 중간에 저장 차원에서 커밋 x
	- 항상 정상 동작을 보장하는 시점에 커밋 O

![[스크린샷 2024-05-17 오후 12.33.51.png]]
#### Tip.commit
- --amend : 전의 커밋에 덮어 쓰는 기능 
	- 주의 ) 깃허브에 올린 내용에 대해서는 amend 를 안 하도록 주의

#### Git Branch
#### HEAD
- Detached HEAD : 브랜치가 아닌 특정 커밋을 가르키는 경우

#### Reset 과 Revert
- Reset : 특정 과거 시점으로 돌아가기
	- 돌아간 시점 이래로 완전히 새롭게 시작
- Revert : 특정 과거 시점으로 되돌리기
	- 히스토리를 되돌리는 방식
#### Merge
- Merge
	- Fast-forward merge : 브랜치에서 분기한 이후, 기존 브랜치에 변경 사항이 없는 경우 진행되는 머지
	- 구조적으로 confilct 가 나지 않음
- 3Way merge
	- 3 way : 


### 과제

#### 면접 질문
- 깃은 무결성, 신뢰성 -> 깃 아이디에 대한 설명
-----
- 거터 영역?
- M : modified


---
### 과제 - 넷플릭스

> 버튼이 말을 안 들었던 이유

plain < iOS15+ >>>
default < legacy
즉 default 스타일을 다루는 버튼 코드와 plain 스타일을 다루는 버튼 코드가 다름 

> 이미지가 색을 잃었던 이유
- Image Rendering <ode: template vs original
```swift
Button.setImage(image: UIImage(named: "어쩌구")?.withRenderingMode(.alwaysOriginal))
```

> 이미지에 색 채우기

`tintColor` = 이미지에 색을 **채움**
예를들어 textField 의 틴트 컬러는 커서의 색상을 바꿀 수 있음

> 왜 기본은 다 파란색인가요?

Interface Builder Document 에서 속성 Global Tint 를 변경하면 기본 적용되는 파랑색을 변경할 수 있음 

> 렌더링 모드로 매번 따로 지정하지 않고도 항상 적용하고 싶다면?

Asset 에서 Render As Original Image 로 설정하면 됨

> Argument 에 설정한게 sender 로 왜 와여? 