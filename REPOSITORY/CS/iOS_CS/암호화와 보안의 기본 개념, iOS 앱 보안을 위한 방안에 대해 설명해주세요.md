#보안 #iOS #앱보안

### 🔐 대칭키 암호화와 비대칭키 암호화의 차이

#### 1. 대칭키(Symmetric key) 암호화
> 대칭키(Symmetric key)방식은 암호문을 생성(암호화)할 때 사용하는 키와, 암호문으로부터 평문을 복원(복호화)할 때 사용하는 키가 동일한 암호 시스템으로 일반적으로 알고 있는 암호 시스템

- 하나의 키로 암호화와 복호화를 수행하므로 대칭키(Symmetric key) 또는 비밀키(Secret Key)방식의 암호화라고 함
- 대칭키의 종류
	- Block cipher 
		- 데이터를 블록 단위로 처리 <- 일반적으로 대칭키 암호화라고 하면 이 방식을 뜻함
		- 정해진 길이, 또는 가변 길이의 암/복호화 키를 사용
		- 주요 알고리즘 
			- DES(Data Encryption Standard : 예전 유닉스의 패스워드 파일을 암호화하는데 사용했지만, 오래전에 뚫려서 이제는 절대 사용하면 안 되는..
			- AES
				- 현재 미국의 표준 암호 알고리즘, 128, 192, 256 비트의 키를 사용할 수 있음
				- 많은 보안 프로토콜에서 사용하고 있음 ex) SSL/TLS, SSH, VPN 둥
				- 블록 크기가 크고 라운드 수가 많아서 안전성이 높지만 공격자가 암호문을 획득하고 암호화에 사용된 키를 노출시키는 경우, 암호문을 해독할 수 있어 안전한 키관리가 필수임 + 데이터의 무결성과 인증에 대해 별도 보안 메커니즘 필요
			- SEED : 국내에서 개발, 128비트 키 사용
			- ARIA : 국내에서 개발
			- IDEA : 유럽에서 개발한 알고리즘
	- Stream cipher
		- 이진화된 평문 스트림과 이진 키스트림의 배타적 논리합(XOR) 연산으로 암호문을 생성
		- 주요 알고리즘
			- RC4
			- A5/1, A5/2, A5/3
- 장점
>  Windows의 BitLocker와 OS X의 FileVault 같이 디스크 전체를 암호화할 대도 대칭키 방식(AES)를 쓴다..!

   - 공개키 방식에 비하여 구현이 용이
   - CPU/메모리 적게 사용
   - 빠른 암/복호화 속도
단점
- 하나의 키만 사용하므로 상대방과 대칭키 기반으로 암호화 통신을 할 경우 상대방도 사전에 같은 키를 가지고 있어야 함 -> 암호화 통신을 위한 키 전달과 관리가 어려움..! 
	- 대칭키를 보내는 중간에 유출될 우려..
	- 암호화 통신을 도감청 당할 수도..
	- 여러 상대방과 통신할 경우 각각의 대칭키를 관리하기(생성, 전달, 유출 시 폐기)가 어렵구..
	- 상대방과 같은 키를 사용할 경우 키가 노출되면 모든 채널과 새로 키를 전달해야하는 치명적 단점..
#### 2. 비대칭키(Asymmetric Key) 암호화
> 비대칭키 암호화는 다른 말로 `공개키 암호 알고리즘`이라고 알려져 있음. 이는 하나의 키가 아닌 암호화에 쓰이는 키 값과 복호화에 쓰이는 키 값이 다른 암호 시스템

- `양방향 암호화`로, 복호화가 가능한 암호 알고리즘
- 공개키 암호는 대칭키 암호의 키 전달에 있어서 취약점을 해결하기위한 노력의 결과로 탄생
- 방식
	- 한 쌍의 키가 존재, 하나는 누구나 가질 수 있는 공개키이며 공개키 암호화 방식은 암호학적으로 연관된 두개의 키를 만들어서 하나는 자기가 안전하게 보관하고 다른 하나는 상대방에게 공개함
	- `개인키로 암호화 한 정보`는 그 쌍이 되는 공개키로만 복호화가 가능
	- `공개키로 암호화 한 정보`는 그 쌍이 되는 개인키로만 복호화가 가능
	>  💡 만약 개인이 비밀통신을 할 경우 비대칭키 암호화보다 대칭키 암호를 사용할 수 있지만, 다수가 통신을 할 때에는 키의 개수가 급증하게 되어 큰 어려움이 따름. 이런 문제를 극복하기 위하여 나타난 것이 공개키 암호화이고 공개키 암호화는 다른 유저와 키를 공유하지 않더라도 암호를 통한 안전한 통신을 할 수 있음이 큰 장점임
	

- 비대칭키의 종류 
	- RSA(Rivest, Shamir and Adleman) 
		- 로널드 리베스트(Ronald Rivest)와 아디 샤미르(Adi Shamir), 레너드 애들먼(Leonard Adleman) 등 3명의 수학자에 의해 개발된 알고리즘
		- 대표적인 공개키 알고리즘, 공개키 암호 시스템으로 암호화와 인증에 사용되며 오늘날 사용되는 공개키 암호 방식의 가장 일반적인 공개 알고리즘
		- 암호화 뿐만 아니라 전자서명이 가능한 최초의 알고리즘 !!
		- 방식
			- 두개의 키 사용, 키 라는 것은 메시지를 열고 잠그는 상수(constant), 숫자를 의미
			- 소인수 분해의 난해함에 기반함. 공개키만을 가지고는 개인키를 짐작할 수 없도록 디자인 됨
			- 두개의 큰 소수들의 곱과, 추가 연산을 통해 하나는 공개키를 구성, 또 하나는 개인키를 구성 함. 한 번 이 키들이 만들어지면, 원래의 소수는 더 이상 중요하지 않고 버릴 수 있음. 이 RSA 시스템을 사용하면, 개인키는 절대로 인터넷을 통해 보내지지 않음
			- ![[Pasted image 20240421200354.png]]
			-  ex ) 김명현이라는 사람에게 최동호라는 사람이 메시지를 보내고자 할 때는 최동호는 김명현의 열린 자물쇠를 들고 와 최동호의 메시지를 봉인(공개키 암호화 과정), 그 다음에 김명현한테 전해주면 ~ 자물쇠의 열쇠(개인키)를 가지고 있는 김명현이 그 메시지를 열어보는(개인키 복호화 과정)식. 중간에 이 메시지를  가로챈 팡햄은 그 열쇠를 받지 못해서 메시지를 못봄 ㅠㅠ
	- EIGamal : 이산 대수 문제의 어려움에 기반을 둔 최초의 공개키 암호 알고리즘
	- ECC(Elliptic Curve Cryptosystem) : 타원곡선? 의 수학적 원리를 이용한 차세대 공개키 암호 방법으로 주목받고 있음
	- DSA(SEED) : 전자상거래, 금융, 무선통신 등에서 전송되는 개인 정보와 같은 중요한 정보를 보호하기 위하여 1999년 2월 한국인터넷진흥원과 한국의 암호 전문가들이 순수 한국 기술로 개발한 128비트 블록 암호

#### 3. 그래서 드디어 차이점 정리..!

|      | 대칭키 암호화 방식                                                                           | 비대칭키 암호화 방식                                                                                                                       |
| ---- | ------------------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------- |
| 개념   | - 암호화(비밀키) = 복호화(비밀키)<br>- 대칭구조                                                      | - 암호화(공개키)와 복호화(개인키)가 다르며 ,<br>이들 중 복호화키만 비밀로 간직<br>- 비대칭 구조                                                                      |
| 특징   | - 대량의 Data 암호화 유리                                                                    | - 전자서명, 공인인증서 등 다양한 이용                                                                                                            |
| 장점   | - 연산 속도 빠르고 구현 용이<br>- 일반적으로 같은 양의 데이터를 암호화하기 위한 연산이 공개키 암호보다 현저히 빠름<br>- 쉽게 기밀성을 제공 | - 키 분배/키 관리가 용이<br>- 사용자의 증가에 따라 관리할 키의 개수가 상대적으로 적음<br>- 키 변화의 빈도가 적음(공개키의 복호화키는 길고 복잡하기 때문)<br>- 기밀성, 무결성을 지원하고 특히 부인 방지 기능을 제공 |
| 단점   | - 키 관리가 어려움<br>- 무결성 지원이 부분적으로만 가능하고, 부인방지 기능을 제공하지 않음                               | - 키의 길이가 길고 연산 속도가 느림                                                                                                             |
| 알고리즘 | SEED, HIGHT, ARIA, LEA, DES, AES, RC4 등                                              | RSA, Diffie- Hellman, ECC, digital signature                                                                                      |

#### 4. 서명 
> 메시지를 보낸 소혜가 자신의 개인키로 서명해서 메시지 보낸 사람이 소혜 본인임을 입증하는 것

```
메시지 송신자(A)가 메시지 수신자(B)한테 메시지를 전송하려고 한다.  
A는 메시지를 A의 개인키로 암호화한 메시지를 만든다. (서명)  
A는 메시지를 B의 공개키로 암호화한다.  
B한테 암호화한 메시지와 서명문을 같이 전달한다.  
B는 B의 개인키로 암호화한 메시지를 복호화한다.(암호화 메시지 -> 메시지)  
또, B는 A의 공개키로 서명문을 복호화한다. (서명 -> 메시지')  
메시지와 메시지'가 같다면, A가 메시지를 보내었다는 것이 보장된다.
```
#### 5. 덧붙여 iOS의 대칭키/비대칭키 활용 사례
> 애플은 암호화를 위해 CryptoKit 이라는 프레임워크 제공함

##### 1) iOS 에서의 RSA 암호화
> iOS 앱내에서 RSA 암호화 방식을 사용 하려면 두가지 방법이 있다.
> 방법에 대하여 자세한 설명은 [여기](https://zamcom.tistory.com/168) 블로그에 잘 설명 되어 있슴다..

 1. RSA 암호화를 지원하는 라이브러리 사용(OpenSSL)
     a ) OpenSSL 정적 라이브러리를 만들고
     b ) 라이브러리를  프로젝트에 추가하고 RSA_public_encrypt 함수를 이용하여 암호화
 2. 직접구현
##### 2) iOS에서 제공하는 암호화  프레임워크 'CryptoKit'
> 암호화 작업을 안전하고 효율적으로 수행할 수 있도록 도와주는 애플 프레임워크
> 이 내용에 대해서는 아래 해시함수를 다루고 더 설명 드리겠음
 
 - 암호학적 해싱(Cryptographic hashing)제공
 - 공개키 암호화 : 디지털 서명(Digital Signature)작업, 키 교환
 - 대칭키 암호화 : 메시지 인증 및 데이터 암호화 작업에 사용
 - ECC 알고리즘을 독점적으로 제공
 - CryptoKit는 **HMAC**, **AES**, **ChaChaPoly**, **P256**, **P384**, **P512** **Curve25519** 등의 암호화 방법을 제공
	 - Cryptographic Hash
		 - SHA215
		 - SHA384
		 - SHA512
	 - Message Authentication Code
		 - HMAC
	 - Cipher
		 - AES
		 - ChaChaPoly
	 - Public Key
		 - P256
		 - P384
		 - P512
		 - Curve25519
- 
  
```swift
let privateKey = Curve25519.Signing.PrivateKey() // 개인키 생성
let publicKey = privateKey.publicKey // 공개키 생성

let signature = try privateKey.signature(for: messageDigest) // 서명
publicKey.isValidSignature(signature, for: messageDigest) // 검증
```


### 🔐 해시 함수의 개념과 활용 사례
#### 1. 해시함수
> 해시함수(hash function)는 임의의 길이는 데이터 `message`를 고정 길이의 데이터 `hash value`, `hash code`, `digest`, `hash`로 매핑하는 함수임. 동일한 input에 대해서는 같은 결과를 도출한다!
##### 1) 암호화 해시 함수
- 해시함수의 일종, 해시값으로부터 원래의 입력값과의 관계를 찾기 어려운 성질을 가짐
	- 역상 저항성(pre-image resistance) : 해시값이 주어졌을 때, 해시값을 생성한 입력값을 찾는 것이 계산상 어려움. 제 1 역상 공격(주어진 해시값을 출력하는 입력값을 찾는 공격)에 대해 안전한 것을 말함
	- 제 2 역상 저항성(second pre-image resistance) : 해시값과 입력값이 주어졌을 때, 해시값을 생성하는 또 다른 입력값2를 찾는것이 계산상 어려움. 제 2 역상 공격(주어진 입력값과 같은 해시값을 출력하는 다른 입력값을 찾는 공격)에 대해 안전한 것을 말함
	- 충돌 저항성(collision resistance) : 같은 해시값을 생성하는 두 개의 입력값을 찾는 것이 계산상 어려워야 하며 해시충돌에 대해 안전해야 한다는 것을 말함  
	- 여기서 제 2 역상 저항성과 충돌 저항성의 차이점은, 제 2 역상 저항성에서는 공격자가 입력값 외 동일한 해시값을 생성하는 입력값2를 찾는 것이고, 충돌 저항성은 공격자가 동일한 해시값을 생성하는 입력값 두개를 자유롭게 선택할 수 있음
- *해시충돌이란? 해시 함수가 서로 다른 두개의 입력값에 대해 같은 출력값을 도출하는 상황. 무한한 입력값을 받아 유한한 출력값을 생성하는 경우, 비둘기집 원리에 의해 해시충돌은 항상 존재한다..!*
	- *비둘기집 원리*
		- *n + 1개의 물건을 n개의 상자에 넣을 때 어느 한 상자에는 두 개 이상의 물건이 들어 있다는 원리*
		- *5명의 사람을 서로 같은 팀이 되지 않도록 4개의 팀에 나누는 것은 불가능함*
	- *생일 문제*
		- *사람이 임의로 모였을 때 그 중에 생일이 같은 두명이 존재할 확률을 구하는 문제*
		- *1년은 365일이므로 366명이 모인다면 비둘기집의 원리에 따라 생일이 같은 두 명이 반드시 존재함*
		- *23명만 모여도 두 명이 생일이 같을 확률은 50%가 넘고, 57명이 모이면 99%를 넘어감*
##### 2) 순환 중복 검사(CRC, cyclic redundancy check)
 - 네트워크 등을 통하여 데이터를 전송할 때, 전송된 데이터에 오류가 있는지 확인하는 방식
	 - 데이터를 전송하기 전, 주어진 데이터에 대한 CRC 값을 계산하여 데이터에 붙여 전송함
	 - 받은 데이터의 값으로 CRC 값을 계산해 오류가 덧붙여 전송되었는지 확인
- 주어진 CRC값을 가지는 다른 데이터를 만들기 쉬움
=> 제 2 역상 저항성, 충돌 저항성을 가지지 않음 

#### 2. 해시 - 알고리즘
> 위 같은 해시함수에 사용되는 알고리즘으로는 MD(Message-Digest Algorithm)과 SHA(Secure Hash Algorithm)등이 있음. 각 알고리즘은 심각한 해시 충돌 문제 등으로 인해 해시 함수를 개선하며, 발표된 순서대로 MDn, SHA-n 식으로 넘버링됨

- 임의의 크기를 가진 데이터(Key)를 고정된 크기의 데이터(Value)로 변화시켜 저장하는 것
- 키에 대한 해시값을 사용하여 값을 저장하고 키-값 쌍의 갯수에 따라 동적으로 크기가 증가하는 associate array
- 해시값 자체를 index로 사용하기 때문에 평균 시간복잡도가 O(1)로 매우 빠름
- 대표적인 서비스
	- 해시기반 메시지 인증코드 (HMAC)
	- 무결성 검증을 통해 데이터 

##### 1) MD(Message-Digest Algorithm)

- 1991년 Ronald Rivest에 의해 개발
- 전자 데이터의 디지털 지문이나 메시지 다이제스트를 생성하는 데 사용되는 암호화 해시 함수의 한 계열
	- *메시지 다이제스트 : 상대적으로 많은 양의 메시지 원문으로부터 일정 크기의 압축된 짧은 다이제스트를 생성하는 방식*
- 디지털  서명 프로토콜, 메시지 인증 코드 및 기타 응용 프로그램에 널리 사용됨
- 방식
	- 임의의 크기의 입력메시지를 가져와 일련의 수학적 연산을 적용하여 해시 또는 메시지 다이제스트로 알려진 고정 크기 출력을 생성함
	- 출력은 입력 메시지에 고유하며 입력 메시지를 변경하면 완전히 다른 해시가 됨
	- MD2, MD4, MD5 및 MD6를 포함한 여러 버전이 있고 각각 다양한 출력 크기와 보안 수준을 갖추고 있음
- 장점
	- 무결성 : 입력 메시지에 고유한 디지털 지문 또는 메시지 다이제스트를 제공하여 전자 데이터의 무결성을 보장
	- 속도 : 빠르고 효율적이여서 다양한 용도에 적합
	- 광범위한 사용 : 디지털 서명 프로토콜, 메시지 인증 코드 및 기타 보안 애플리케이션에 널리 사용
- 단점
	- 충돌 공격 : 다른 암호화 해시함수와 마찬가지로 MD는 두개의 서로 다른 입력 메시지가 동일한 해시를 생성할 수 있는 충돌공격에 취약함, 하지만 MD6와 같은 강력한 버전이 이 문제를 해결하기 위해 개발됨
	- 제한된 보안 : MD5는 더 이상 안전한 보안으로 간주되지 않아 IT 보안 애플리케이션에 사용하지 않음
##### 2) SHA(Secure Hash Algorithm)
- 해시함수를 이용해서 만든 해시 암호화 알고리즘의 모음
- 미국 국가보안국(NSA)에서 1993년 처음 설계했고 미국 국가 표준으로 지정됨
- 종류는 SHA-0 ~ SHA-3 다양하게 있는데 실제 많이 사용되고 있는 함수는 SHA-2
- digest의 길이에 따라 SHA-224, SHA-256 등등 나눌 수 있음
- TLS, SSL, PGP, SSH, IPSec 등 많은 보안 프로토콜에서 사용중
- 💡DES와 AES는 기밀성을 목적으로 사용하는 반면, SHA는 무결성을 보증. 비트코인이나 이더리움에서 사용되는 SHA 는 블록헤더, 전자서명, 공개키 등 위변조 방지를 위해서임 

#### 3. iOS에서의 활용 사례들

>Xcode 내에서 제공하는 함수를 이용하여 MD5 또는 SHA256 해시를 생성할 수 있음. 그리고 이제 Apple이 지원하는 CrytoKit을 사용하여 다양한 암호화가 가능해졌음. 사용자의 비밀번호를 저장하는 방법에 평문으로 저장하기 보다는 해시 값을 이용하여 저장하고, 파일의 해시 값을 비교하여 파일의 무결성을 검증하는 등으로 응용할 수 있음
##### 1) 대상 통으로 해시 생성
![[Pasted image 20240422193520.png]]
![[Pasted image 20240422193532.png]]
위 코드들은 CommonDigest.h 의 헤더파일의 일부이고 위 함수와 구조체를 이용하여 해시값을 구할 수 있음

CC_MD5함수를 이용하여 해시 값을 구할 수 있음
unsigned char *CC_MD5(const void *source, CC_LONG len, unsigned char *dest)

CC_MD5함수와 CC_SHA256함수는 unsigned char * 를 리턴하고 있으나, 일반적으로 아래 예시처럼 리턴 값을 사용하고 있지 않지만 리턴 값은 md파라미터를 통해 전달된 포인터를 반환함

- 첫 번째 인자 : 해싱 할 데이터의 포인터
- 두 번째 인자 : 해싱 할 데이터의 사이즈  
- 세 번째 인자 : 해싱 한 데이터를 저장 할 수 있는 포인터

```swift
#import <CommonCrypto/CommonDigest.h>

NSString *md5(NSString *str) {
	const char *cStr = [str UTF8String];
	unsigned char result[CC_MD5_Digest_LENGTH];
	CC_MD5(cStr, strlen(cStr), result);
	return [NSString stringWithFormat: @"%02X%02X%02X%02X%02X%02X%02X%02X%02X%02X%02X%02X",
	result[0], result[1],
	result[2], result[3],
	result[4], result[5],
	result[6], result[7],
	result[8], result[9], 
	result[10], result[11], 
	result[12], result[13], 
	result[14], result[15], 
	];						  
}
NSString *digest = md5(@"test");
NSLog(@"MD5 TEST %@", digest);

```

이 코드는 MD5 해싱소스 코드임. 여기서 MD5를 SHA256으로 치환하고, result의 배열인덱스를 0~ 31 까지 받아내면 SHA256소스가 된다.
##### 2) 버퍼를 이용하여 해시 생성
 예를 들어 크기가 큰 파일의 해시 값을 구한다고 가정할 때, 위의 방법을 이용하면 파일 전체를 메모리에 올려야 하기때문에 저사양 단말에서는 큰 부담을 가지게 될 수 있음! 따라서 파일의 일부를 버퍼를 이용하여 해시 값을 업데이트함으로써, 메모리사용량을 줄 일 수 있다고 함

``` swift
static int md5useUpdate(char* data, long len, char** outData)
{
    unsigned char hashBuf[BUF_LEN] = {0,};       //업데이트에 사용할 버퍼
    long curSize = 0;                            //현재 까지 읽은 데이터 사이즈
    long remainSize = len;                       //남아있는 데이터 사이즈
    //md5 컨텍스트 선언 및 초기화
    CC_MD5_CTX md5;
    CC_MD5_Init(&md5);
    //더 읽어야할 데이터가 남아있다면
    while(curSize < len) {
        if(remainSize < BUF_LEN){ //남은 사이즈가 버퍼보다 작을 경우, 남아있는 사이즈만큼만 메모리 복사 및 해시 업데이트
            memcpy(hashBuf, (char *)data, remainSize);
            CC_MD5_Update(&md5, hashBuf, (CC_LONG)remainSize);
        }
        else { //일반적인 경우 버퍼사이즈(1024)만큼 메모리 복사 및 해시 업데이트
            memcpy(hashBuf, (char *)data, BUF_LEN);
            CC_MD5_Update(&md5, hashBuf, (CC_LONG)BUF_LEN);
        }
        data += BUF_LEN;                //메모리 읽은 후 포인터 이동
        curSize += BUF_LEN;             //현재까지 읽은 사이즈 계산
        remainSize -= BUF_LEN;          //남아있는 사이즈 계산
    }
    unsigned char digest[CC_MD5_DIGEST_LENGTH] = {0,};
    CC_MD5_Final (digest, &md5);
    char *tmpOut = *outData;
    for(int i = 0; i < CC_MD5_DIGEST_LENGTH; i++)
    {
        sprintf(tmpOut, "%02x", digest[i]);
        tmpOut += 2;
    }
    return 0;
}
```
 정의한 함수 md5useUpdate는 해싱할 데이터와 사이즈, 해싱한 문자열을 기록할 데이터의 포인터를 입력받는다.
##### 3) CryptoKit을 사용한 암호화
> 위 두가지방법을 예전엔 주로 사용한 것 같으나.. 이젠 Apple에서 지원한다. 

1. **Normal Hashing**
Swift에서도 hashing을 제공하며, CryptoKit에서 제공하는 hashing 방법과 다른 메서드를 사용한다.
Swift는 Hashable 프로토콜을 제공하고, Set이나 Dictionary 타입의 데이터를 Hashing하고 싶다면 Hashable 프로토콜을 따라야 한다. String이나 Int는 Hashable 프로토콜을 따르고 있어서 문자열, 숫자 데이터는 바로 hashing이 가능함

```swift
/// 리터럴 값을 해싱하면 hash value이 나온다. /// haser로 만든 hash value는 계산할 때마다 다른 값이 나온다. 
func hashItem(item: String) -> Int { 
	var hasher = Hasher() 
	item.hash(into: &hasher) 
	return hasher.finalize() 
} 

let hashvalue = hashItem(item: "brown fox")
```
2. **1-2. Cyptrograhpic Hashing (SHA)**
CryptoKit이 제공하는 Cryptographic hashing은 [SHA-2(Secure Hash Algorithm 2)](https://en.wikipedia.org/wiki/SHA-2) 방식을 지원함 digest의 크기에 따라 3가지로 나뉜다. 예를 들어 SHA256의 digest는 256 비트를 가진다.

- **SHA256**
- **SHA384**
- **SHA512**

digest로 **데이터 무결성**을 확인할 수 있음

```swift
import CryptoKit /// 이미지 데이터를 받아온다. 
func getData(for item: String, of type: String) -> Data { 
	let filePath = Bundle.main.path(forResource: item, ofType: type)! 
	return FileManager.default.contents(atPath: filePath)! 
} 

let data = getData(for: "Baby", of: "png") 
UIImage(data: data) 

/// 256-bit의 digest를 만든다. 
let digest = SHA256.hash(data: data) 

// 송신자는 'data'와 'digest'를 수신자에게 보낸다.
// 수신자는 'data'를 cryptographic hashing한 값과 'digest'를 비교한다. 같다면 데이터는 무결한 상태이다. 
let receivedDataDigest = SHA256.hash(data: data) 
if digest == receivedDataDigest { 
	print("보낸 data == 받은 data") 
}
```

1. 데이터 송신자는 `data`와 `Cryptographic hashing`의 결과 값 `digest`와 같이 실어 보낸다.
2. 데이터 수신자는 `data`를 `Cryptographic hashing`한 값과 전달받은 `digest`를 **비교**한다. 값이 똑같으면 데이터에 손상 없고, 그렇지 않으면 손상이 있는 것

CrytoKit이 제공하는 암호화나 인증방식이 꽤나 다양하기 때문에 [여기](https://dadahae0320.tistory.com/47)에서 필요할 때 공부하는 걸 추천한다 ㅎㅎ 



### 참고
- [대칭키 암호화](https://lesstif.gitbook.io/web-service-hardening/encryption)
- [비대칭키 암호화](https://raonctf.com/essential/study/web/asymmetric_key)
- [추 후 참고](https://velog.io/@gs0351/%EB%8C%80%EC%B9%AD%ED%82%A4-vs-%EA%B3%B5%EA%B0%9C%ED%82%A4%EB%B9%84%EB%8C%80%EC%B9%AD%ED%82%A4)
- [대칭키와 비대칭키/공개키](https://velog.io/@octo__/%EB%8C%80%EC%B9%AD%ED%82%A4%EC%99%80-%EA%B3%B5%EA%B0%9C%ED%82%A4%EB%B9%84%EB%8C%80%EC%B9%AD%ED%82%A4)
- [CryptoKit을 사용한 암호화](https://phillip5094.tistory.com/21)
- [암호화 작업을 위한 Apple CryptoKit 알아보기](https://dadahae0320.tistory.com/47)
- [해시 함수 (Hash Function)](https://velog.io/@hadam/hash-function)
- [해시알고리즘, 해시 함수, SHA..](https://swingswing.tistory.com/169)
- [MD5해시 생성 / SHA256해시 생성](https://bachs.tistory.com/entry/iOS-MD5%ED%95%B4%EC%8B%9C-%EC%83%9D%EC%84%B1-SHA256%ED%95%B4%EC%8B%9C-%EC%83%9D%EC%84%B1)