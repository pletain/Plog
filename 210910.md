# HTTP 메세지
### HTTP 메세지 구조
- start line - 시작라인
- header - 헤더 
- empty line - 공백 라인(CRLF)
- message body

### HTTP 시작라인 
#### start-line = request-line / status-line
##### request-line (요청메세지)
  - request-line = method SP(공백) request-target SP HTTP-version CRLF(엔터)
  - HTTP 메서드(GET), 요청대상(/search?q=hello&hl=ko), HTTP Version
  <br />
* HTTP 메서드
  - 종류: GET, POST, PUT, DELETE...
  - 서버가 수행해야 할 동작 지정
    - GET: 리소스 조회
    - POST: 요청 내역 처리
  <br />
* 요청 대상
  - absolute-path[?query] (절대경로[?쿼리])
  - 절대경로= "/"로 시작하는 경로
  <br />
* HTTP 버전

##### status-line (응답 메세지)
- status-line =  HTTP-version SP(공백) status-code SP reason-phrase CRLF(엔터)
- HTTP 상태 코드: 요청 성공, 실패를 나타냄
  - 200: 성공
  - 400: 클라이언트 요청 오류
  - 500: 서버 내부 오류
- 이유 문구
  - 사람이 이해할 수 있는 잛은 상태 코드 설명 글

### HTTP 헤더
- header-field = field-name":" OWS field-value OWS (OWS: 띄어쓰기 허용)
- field-name은 대소문자 구분 없음
- ex) Host: www.google.com, Content-Type: text/html;charset=UTF-8 
- 용도
  - HTTP 전송에 필요한 모든 부가정보
  - ex) 메세지 바디의 내용, 크기, 압축, 인증, 요청 클라이언트(브라우저) 정보, 서버 애플리케이션 정보, 캐시 관리 정보...
  - 표준 헤더가 너무 많다.
  - 필요시 임의 헤더 추가 가능
    - helloworld: hi 


### HTTP 메세지 바디
- 용도 
  - 실제 전송할 데이터
  - HTML 문서, 이미지, 영상, JSON 등등 byte로 표현할 수 있는 모든 데이터 전송 가능

