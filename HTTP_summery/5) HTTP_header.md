### HTTP 헤더 개요
* header-field = field-name ":" OWS field-value OWS (OWS: 띄어쓰기 허용)
* field-name은 대소문자 구분 X

#### 용도
* HTTP 전송에 필요한 모든 부가정보
* ex) 메시지 바디의 내용, 메시지 바디의 크기, 압축, 인증, 요청 클라이언트, 서버 정보, 캐시 관리 정보 ...
* 표준 헤더가 너무 많음
* 필요시 임의의 헤더 추가 가능
  * helloworld: hihi 

#### RFC2616(과거)
* 헤더 분류
  + General 헤더: 메시지 전체에 적용되는 정보
  + Request 헤더: 요청 정보 
  + Response 헤더: 응답 정보
  + Entity 헤더: 엔티티 바디 정보

#### HTTP BODY (message body - RFC2616(과거))
* 메시지 본문(message body)은 엔티티 본문(entity body)을 전달하는데 사용
* 엔티티 본문은 요청이나 응답에서 전달할 실제 데이터
* 엔티티 헤더는 엔티티 본문의 데이터를 해석할 수 있는 정보 제공
  + 데이터 유형(html, json), 데이터 길이, 압축 정보 등등 

#### RFC723x 변화
* 엔티티(Entity) -> 표현(Representation)
* Representation -> representation Metadata + Representation Data
* 표현 = 표현 메타데이터 + 표현 데이터

#### HTTP BODY (message body - RFC7230(최신))
* 메시지 본문(message body)을 통해 표현 데이터 전달
* 메시지 본문 = 페이로드(payload)
* **표현**은 요청이나 응답에서 전달할 실제 데이터
* **표현 헤더는 표현 데이터**를 해석할 수 있는 정보 제공
  + 데이터 유형(html, json), 데이터 길이, 압축 정보 등등
* 참고: 표현 헤더는 표현 메타데이터와 페이로드 메시지를 구분해야 하지만 
<hr />

### 표현
* Content-Type: 표현 데이터의 형식
* Content-Encoding: 표현 데이터의 압축 방식
* Content-Language: 표현 데이터의 자연 언어
* Content-Length: 표현 데이터의 길이
* 표현 헤더는 전송, 응답 둘다 사용 

#### Content-Type
###### 표현 데이터의 형식 설명
* 미디어 타입, 문자 인코딩
* ex)
 + text/html; charset=utf-8
 + application/json
 + image/png 

#### Content-Encoding
###### 표현 데이터 인코딩
* 표현 데이터 인코딩
* 표현 데이터를 압축하기 위해 사용
* 데이터를 전달하는 곳에서 압축 후 인코딩 헤더 추가
* 데이터를 읽는 ㅉ목에서 인코딩 헤더의 정보로 압축 해제
* ex)
 + gzip
 + deflate
 + identity 

#### Content-Language
###### 표현 데이터의 자연 언어
* 표현 데이터의 자연 언어
* ex)
 + ko
 + en
 + en-US

#### Content-Length
###### 표현 데이터의 길이
* 바이트 단위
* Transfer-Encoding(전송 코딩)을 사용하면 Content-Length를 사용하면 안됨
<hr />

### 협상(콘텐츠 네고시에이션)
###### 클라이언트가 선호하는 표현 요청
* Accept: 클라이언트가 선호하는 미디어 타입 전달
* Accept-Charset: 클라이언트가 선호하는 문자 인코딩
* Accept-Encoding: 클라이언트가 선호하는 압축 인코딩
* Accept-Language: 클라이언트가 선호하는 자연 언어
* 협상 헤더는 요청 시에만 사용

#### 협상과 우선 순위
###### Quality Values(q)
* Quality Values(q) 값 사용
* 0~1, 클수록 높은 우선 순위
* 생략하면 1
* Accept-Language: ko-KR,ko;q=0.9,en-US;q=0.8,en;q=0.7
 + 1. ko-KR;q=1 (q생략)
 + 2. ko;q=0.9
 + 3. en-US;q=0.8
 + 4. en:q=0.7
<br />

* 구체적인 것이 우선한다.
* Accept: text/&#42; , text/plain, text/plain;format=flowed, &#42;/&#42;
 1. text/plain;format=flowed
 2. text/plain
 3. text/&#42;
 4. &#42;/&#42;

* 구제적인 것을 기준으로 미디어 타입을 맞춘다.
* Accept: text/&#42; ;q=0.3, text/html;1=0.7, text/html;level=1, text/html;level=2;q=0.4, &#42;/;q=0.5

<hr />

### 전송 방식
* Transfer-Encoding
* Range, Content-Range

#### 전송 방식 설명
* 단순 전송
* 압축 전송
* 분할 전송
* 범위 전송

<hr />

### 일반 정보
* From: 유저 에이전트의 이메일 정보
* Referer: 이전 웹 페이지 주소
* User-Agent: 유저 에이전트 애플리케이션 정보
* Server: 요청을 처리하는 오리진 서버의 소프트웨어 정보
* Date: 메시지가 생성된 날짜

#### From (유저 에이전트의 이메일 정보)
* 일반적으로 잘 사용되지 않음
* 검색 엔진 같은 곳에서, 주로 사용
* 요청에서 사용

#### Referer (이전 웹 페이지 주소)
* 현재 요청된 페이지의 이전 웹 페이지 주소
* A -> B로 이동하는 경우 B를 요청할 때 Referer: A를 포함해서 요청
* Referer를 사용해서 유입 경로 분석 가능
* 요청에서 사용
* 참고: referer는 단어 referrer의 오타

User-Agent
유저 에이전트 애플리케이션 정보

* user-agent: Mozilla/5.0 (Macintosh; Intel Mac OS x 10_15_7) AppleWebkit/537.36(KHTML, like Gecko) Chrome/86.0.4240.183 Safari/537.36
* 클라이언트의 애플리케이션 정보(웹 브라우저 정보, 등등)
* 통계 정보
* 어떤 종류의 브라우저에서 장애가 발생하는지 파악 가능
* 요청에서 사용

#### Server
요청을 처리하는 ORIGIN 서버의 소프트웨어 정보
* Server: Apache/2.2.22 (Debian)
* server: nginx
* 응답에서 사용 

#### Date (메시지가 발생한 날짜와 시간)
* Date: Tue, 15, NOV 1994 08:12:31 GMT
* 응답에서 사용

<hr />

### 특별한 정보
* Host: 요청한 호스트 정보(도메인)
* Location: 페이지 리다이렉션
* Allow: 허용 가능한 HTTP 메서드
* Retry-After: 유저 에이전트가 다음 요청을 하기까지 기다려야 하는 시간
#### Host 요청한 호스트 정보(도메인)
* 요청에서 사용
* 필수
* 하나의 서버가 여러 도메인을 처리해야 할 때
* 하나의 IP 주소에 여러 도메인이 적용되어 있을 때
#### Location 페이지 리다이렉션
* 웹 브라우저는 3xx 응답의 결과에 Location 헤더가 있으면, Location 위치로 자동 이동(리다이렉트)
* 응답코드 3xx에서 설명
* 201(Created): Location 값은 요청에 의해 생성된 리소스 URI
* 3xx(Redirection): Location 값은 요청을 자동으로 리디렉션하기 위한 대상 리소스를 가리킴
#### Allow 허용 가능한 HTTP 메서드
* 405(Method Not Allowd) 에서 응답에 포함해야함
* Allow: GET, HEAD, PUT
#### Retry-After 유저 에이전트가 다음 요청을 하기까지 기다려야 하는 시간
* 503(Service Unavailable): 서비스가 언제까지 불능인지 알려줄 수 있음
* Retry-After: Fri, 31 Dec 1999 23:59:59 GMT(날짜 표기)
* Retry-After: 120(초단위 표기)
<hr />

### 인증
* Authorization: 클라이언트 인증 정보를 서버에 전달
* WWW-Authenticate: 리소스 접근 시 필요한 인증 방법 정의

#### Authorization 클라이언트 인증 정보를 서버에 전달
* Authorization: Basic xxxxxxxxxxxxxxxxxxx

#### WWW-Authenticate 리소스 접근 시 필요한 인증 방법 정의
* 리소스 접근 시 필요한 인증 방법 정의
* 401 Unauthorized 응답과 함께 사용
* WWW-Authenticate: Newauth realm="apps", type=1, title="Login to \"apps\"", Basic realm="simple"





