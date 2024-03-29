# HTTP의 이해

**프로토콜 -> 규칙의 집합, 규약, 약속**

**애플리케이션 레이어 →** [**OSI 7 계층**](https://ko.wikipedia.org/wiki/OSI\_%EB%AA%A8%ED%98%95) **참고**

2, 3, 4, 7계층만 살펴보자.

1. 2계층 - 데이터 링크 계층 ⇒ MAC address
2. 3계층 - 네트워크 계층 ⇒ IP address
3. 4계층 - 전송 계층 → TCP, UDP ⇒ Port number
4. 7계층 - 응용 계층 → HTTP 등
   1. HTTPS를 위한 TLS 같은 보안 계층이 먼저 들어갈 수도 있다.

#### 클라이언트-서버 모델 + 메시지 교환

1. 서비스/리소스 → [URL](https://developer.mozilla.org/ko/docs/Web/HTTP/Basics\_of\_HTTP/Identifying\_resources\_on\_the\_Web)  : 명확히 어떤걸 요구하는지를 말해줌&#x20;
   1. scheme://host:port/path?query#fragment
2. 클라이언트 → 요청
3. 서버 → (처리) → 응답

#### 무상태

1. HTTP는 각각의 요청이 독립적 : 항상 알려줘야한다. 내가 누구인지
2. 즉, 클라이언트는 항상 자신이 누구인지 알려줘야 한다.
   1. 요청과 응답을 통해 계속 주고 받는 쿠키
   2. 데이터는 서버에서 관리하고 쿠키 등으로 key를 관리하는 세션\
      url뒤에 session\_000을 붙여서 주기도 했음
   3. 웹 브라우저의 기능 (localStorage 등) : 클라이언트가 독자적으로 관리

#### HTTP 메시지(트랜잭션)

결과적으로 이 http메세지를 잘 주고 받는것이 중요하다.

1. 기본적으로는 사람이 읽을 수 있는 형태를 지향함
2. 기본적인 구조는 요청과 응답 모두 동일 구조
   * Start line → 요청과 응답의 형태가 다름.
   * Headers
   * 빈 줄 < 중요함
   * Body(응답 에서는 body가 필요)
     1. 크기를 알기 어렵다. Headers의 Content-Length 항목 등을 활용한다.
     2. Start line, Headers는 텍스트지만 body는 아닐 수 있음. 바이너리 등 가능.
     3. 하나가 아니라 여럿일 수도 있다. 파일 업로드 등을 위해 쓰이는 multipart/form-data가 대표적.

#### [HTTP Method](https://developer.mozilla.org/ko/docs/Web/HTTP/Methods) (요청)

1. GET → Read (문서를 읽을때)
2. HEAD → GET without body (바디 없이 헤드만 읽고싶을때)
3. POST → Submit (멱등성X) ⇒ Collection Pattern에서 Create로 사용 \
   멱등성 : 같은 작업을 반복해도 달라지지 않음
4. PUT → Update (+Create) ⇒ Overwrite! ( 리소스를 전부 바꿔치기 해 줌 : 덮어쓰기 )
5. PATCH → Update (partial) (멱등성X) (부분적 업데이트 가능)
6. DELETE → Delete
7. OPTIONS → 지원 확인

#### [HTTP Status Code](https://developer.mozilla.org/ko/docs/Web/HTTP/Status) (응답)

1. 1xx → 정보 ⇒ 우리가 직접 쓰는 일은 드믐.
2. 2xx → 성공 ⇒ 200 OK, 201 Created(잘 만들어짐), 204 No Content(연결이 되었는데 내용이 없음)
3. 3xx → 리다이렉션 ⇒ 304 Not Modified가 특수한 형태로 자주 보임. (url 바꿔서 그냥 연결해줌)
4. 4xx → 클라이언트 쪽 문제 ⇒ 404 Not Found (요청을 잘못함)
5. 5xx → 서버 쪽 문제 ⇒ 500 Internal Server Error (일명 어쩌라고. 서버가 뭔가 잘못함)

**Status Code 요약**

1. 1xx : informational - 리퀘스트를 받아들여 처리중
2. 2xx : Success - 리퀘스트를 받아들여 정상적으로 처리
3. 3xx : Redirection - 리퀘스트를 완료하기 위해 추가 동작이 필요함
4. 4xx : Client error - 리퀘스트를 서버에서 이해 불가능
5. 5xx : Server error - 리퀘스트를 서버에서 처리 불가능
