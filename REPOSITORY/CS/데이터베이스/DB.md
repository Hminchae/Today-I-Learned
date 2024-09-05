- Kafka : Disk 이용하지만 내부적으로 Sequential I/O 하기 때문에 다른 Disk 저장소보다 빠름 
- Redis : in-memory data store 이용해서 다른 DB보다 빠르다는 평가
- Connection Pool : DB는 요청 처리할 수 있는 커넥션 풀을 미리 준비해두고, 이 관리법에 따라 성능 차이 존재
- Disk vs Memory : DB 응답은 디스크 또는 메모리에 적재, 디스크는 Seek Time이 소요되기 때문에 Memory 보다 일반적으로 느림
- Sequential vs Random Access : 랜덤 탐색은 필요한 위치에 접근하는 동안 탐색 시간이 길고, 순차 탐색은 순서대로 탐색하기 때문에 랜덤보다 빠름
- DB 옵티마이저 : 인덱스를 이용할지, 풀스캔을 이용할지 어떤 방법이 빠른지를  계산하고 공유풀이라는 곳에 캐싱해둠

#### 분산 데이터베이스
- Scale-up -> 
#### CAP
- Consistency(일관성), Availability(가용성), Partition Tolerance(분할)
- 