#Realm테이블여러개

### Realm 테이블을 합쳐보기
>Realm은 다른 RDBMS에서 사용하는 브릿지 테이블이나 조인을 사용하지 않고 Link, EmbeddedObject, LinkingObject를 통해 1:N, N:N 역 관계를 지원하고 있다.
#### To - Many Relationship
- 서로 다른 두개의 테이블을 연결시켜 일대 다 관계를 만들 수 있음
- 한 Depth 의 폴더를 더 만든다고 이해하면 될까..?
	- 회사에서 살 것
		- 공책
		- 파일
		- 맥북 
		- 등
	- 내가 살 것
		- 수박 
		- 참외
		- 등?
![[스크린샷 2024-07-08 오전 10.59.41.png]]
#### Inverse Relationship

![[스크린샷 2024-07-08 오전 11.32.39.png]]


알라모파이어 : 라우터패턴.. 에러 핸들링 상세화 ..


### 궁금한거
- [ ] @Persisted 가 뭘까?