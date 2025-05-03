## IAM
> Identity and Access Management

기업 환경에서는 
- 인증/인가 된 사람과 디바이스만 필요할 때 애플리케이션에 접속하여야 한다. 
- 사용자 관리, 로그인, 액세스 권한 할당과 제거 프로세스를 감독할 수 있어야 한다. 

일반적인 IAM 사용자 구분
- 직원, 외주, 고객, 파트너

## Keycloak 설치
```
docker run -p 8080:8080 \  
 -e KC_BOOTSTRAP_ADMIN_USERNAME=admin \  
 -e KC_BOOTSTRAP_ADMIN_PASSWORD=admin \  
 [quay.io/keycloak/keycloak:26.1.4](http://quay.io/keycloak/keycloak:26.1.4) \  
 start-dev**
```

## Realm 생성

![[Pasted image 20250408005958.png]]

## User 생성 

![[Pasted image 20250408010436.png]]

새로만든 realm 에서 User 메뉴를 선택하여 사용자를 추가한다.
account console 에 접속(http://localhost:8080/realms/myrealm/account) realm 명/account 경로
![[Pasted image 20250408011047.png]]
![[Pasted image 20250408011412.png]]
접속 기기 정보 기능도 제공함

