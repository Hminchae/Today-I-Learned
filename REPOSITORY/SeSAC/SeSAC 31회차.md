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
- realm : 모바일 최적화 
