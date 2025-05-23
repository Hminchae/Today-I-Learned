#Database UI ➡️ Network ➡️ Database

> ✅ 복습
> final class, private 키워드 => 컴파일 최적화
> BaseVC(alert, configure) -> 재정의 가능성, 어떤 메서드가 실행될지는 컴파일 이후
> struct/enum : 컴파일 타임
> class : 런타임 결정 
> 💡런타임에 결정되던 것(Dynamic Dispatch)을 컴파일타임(Static Dispatch)으로 최대한 옮겨야 성능상 이점이 있음


### 데이터
데이터라는게 멀까..
#### Database
- 데이터를 저장한 파일들의 집합체
#### DataBase Management System
- 데이터베이스를 관리하기 위한 소프트웨어
#### RDBMS 
- Relational DataBase Management System

- 스키마 schema
- 테이블
- 레코드(Row)
	- 가로로 묶여있는 데이터
- 컬럼(Column = Attribute)

- PK
	- Primary key
	- 중복 X, 레코드를 식별하도록 하는 것.
	- ex ) 학번, 주민번호, 사번
- UK
	- Unique Key 
	- PK는 아니지만 값에대한 중복은 허용하지 않으며 null 은 가능한 값
- FK
	- Foreign Key 
	- 다른 테이블의 primary key

--- 
- 정규화 
---
> 금액 카테고리 메모내용 제목
> 컬럼 몇개? 테이블 몇개?


| 메모 ID(PK) | 제목  | 메모 내용   | 카테고리(FK) | 금액  | 등록날짜 |
| --------- | --- | ------- | -------- | --- | ---- |
|           |     | String? |          | Int |      |

| 카테고리 ID(PK) | 카테고리 이름 | 메모 수 | 총금액 |
| ----------- | ------- | ---- | --- |
|             |         |      |     |
#### Realm
- realm : 모바일 최적화 , 단순입출력🐆, 호환성 ⬆️
- CoreData : 기깔나는 통계, 차트, 그래프, 복잡한 연산을 사용하고 싶다면..선택

![[스크린샷 2024-07-02 오후 12.06.07.png]]

> Realm Studio 에서 위 테이블을 확인할 수 있다.

#### UserDefault vs Realm / DB
> 왜?

Realm은 가지고 오면서 정렬을 해줄 수 있음
![[스크린샷 2024-07-02 오후 12.27.17.png]]

!! 혹시 중간에 컬럼을 추가해주고 싶다면??
 ![[스크린샷 2024-07-02 오후 12.31.52.png]]![[스크린샷 2024-07-02 오후 12.32.09.png]]
> 🚨
> 시뮬에서 앱을 삭제하고 테이블을 초기화시킨다..

#### Transaction ?
> 왜 항상 try 구문 내에서 코드를 써야 하는건지..

#### PK
1. 중복 X
2. 고유
3. nil X
4. Index
	1. 여러개의 레코드중에서 번호로 목표 레코드를 찾을 수 있도록 하는 것
```swift
(indexed: true) <- 인덱스로 하는 것
💡 왜 모든 컬럼을 인덱스로 쓰지 않는건가? 인덱스를 위한 페이지 또한 늘어나면서 속도가 느려진다. 
```

#### Migration
> DB에만 있는 개념은 X
> 현재 운영하고 있는 환경 셋팅에서 다른 운영 환경으로 옮기는 작업
> 데이터베이스에서는 스키마 버전을 고나리하기 위해 수행