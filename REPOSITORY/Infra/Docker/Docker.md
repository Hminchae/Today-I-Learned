#docker #컨테이너 

> 이식성 : 특정 프로그램을 다른 곳으로 쉽게 옮겨서 설치 및 실행할 수 있는 특성

### 💡IP/Port

규약으로 정해져있는 포트 번호가 몇개 있음
- 22번(SSH, Secure Shell Protocol): 원격 접속을 위한 포트 번호
	- EC3 인스턴스에 연결할 때 22번 포트를 사용함
- 80번(HTTP) : HTTP로 통신할 때 사용
- 443(HTTPS) : HTTPS 로 통신할 때 사용

### Docker 란? 
> 컨테이너를 사용하여 각각의 프로그램을 분리된 환경에서 실행 및 관리할 수 있는 툴

### Container 란?
> 	하나의 컴퓨터 환경 안에서 여러개의 `미니 컴퓨터 환경`을 구성할 수 있는 형태 : `미니 컴퓨터 환경` == `컨테이너` 

![[Pasted image 20250223234522.png]]

#### Container의 독립성
컨테이너는 독립적인 컴퓨터 환경이다. 구체적으로 아래의 항목들이 독립적으로 관리된다.
- 디스크(저장 공간) : 각 컨테이너마다 서로 각자의 저장 공간을 가지고 있다. 일반적으로 A 컨테이너 내부에서 B 컨테이너 내부에 있는 파일에 접근할 수 없다. 
- 네트워크(IP, Port) : 각 컨테이너마다 고유의 네트워크를 가지고 있음. 컨테이너는 각자의 IP주소를 가지고 있음


### Docker 명령어
- `docker pull 이미지명` : 이미지 다운  // latest 태그명을 가진 이미지를 다운 받는다.
	- `docker pull nginx:stable-alpine3.19-perl` : 특정 태그 정해서 이미지 다운 가능 
- `docker image ls` : 가지고 있는 이미지 리스트
- `docker image rm ~id~` : 특정 id의 이미지 삭제
- `docker image rm -f ~id~` : 중단된 상태의 컨테이너의 이미지를 강제 삭제
- `docker image rm $(docker images -q)` : 컨테이너 안 포함된 이미지 삭제
- `docker image rm -f $(docker images -q)` : 중단된 상태의 이미지 강제 삭제

![[Pasted image 20250225234949.png]]

💡이미지는 뭔데 ? :: 


