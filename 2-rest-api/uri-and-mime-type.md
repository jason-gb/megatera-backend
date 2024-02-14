# URI & MIME type

### 학습 키워드

* URI & URL & URN
  * URI : 리소스(자원)를 식별하는 고유 문자열 시퀀스
  * URL : 리소스의 위치를 나타냄
  * URN : 리소스의 고유 이름을 사용

### [URI](https://developer.mozilla.org/ko/docs/Web/HTTP/Basics\_of\_HTTP/Identifying\_resources\_on\_the\_Web) (Uniform Resource Identifier)

리소스를 식별하는 방법.

식별할 때는 식별자(Identifier = ID)를 활용.

URI은 크게 둘로 나뉨:

1. URL(Uniform Resource Locator) → 리소스의 위치. 위치 변경에 취약함.(서울에 살던 사람이 부산에 잠깐 갔을때는 서울에 있는 사람을 찾을 수 없음.)
2. URN(Uniform Resource Name) → 리소스의 “유니크”한 이름. 사실상 쓰이지 않음.

URI라고 쓰는 건 대부분 URL을 의미함. URN 쓰는 걸 거의 본 적이 없음. 따라서 URI와 URL을 크게 구별하지 않고 동의어에 가깝게 사용함.

### [MIME Type](https://developer.mozilla.org/ko/docs/Web/HTTP/Basics\_of\_HTTP/MIME\_types) (Content Type, Media Type)

Content의 종류를 표현. `<type>/<subtype>`의 형태로 쓴다. HTTP Headers에 `Content-Type` 속성으로 전달함. [IANA](https://www.iana.org/assignments/media-types/media-types.xhtml)에 등록된 목록을 참고하자.

1. `text/plain` ⇒ E-mail에서 자주 사용.
2. `text/html` ⇒ 일반적인 웹 문서. HTML 문서.
3. `text/css`
4. `text/javascript`
5. `application/xml` ⇒ 범용. 자기서술적이기 상대적으로 어렵다.
6. `application/atom+xml`
7. `application/json` ⇒ 범용. 자기서술적이기 굉장히 어렵다.
8. `application/dns+json`
