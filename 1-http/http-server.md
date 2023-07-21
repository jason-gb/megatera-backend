# HTTP server

### HTTP 서버

#### 1️⃣ Listen

다른 곳에 접속하는 게 아니라 포트 번호만 정하면 된다. 만약 80 포트를 사용 중이라면 8080 등 다른 포트 번호를 쓰면 된다.

```java
int port = 8080;
```

Java에서는 ServerSocket이라는 별도의 클래스를 사용한다(기존 사용하던 Socket을 사용하지 않음. Socket을 상속한 게 아니라, 완전히 구별된다는 점에 주의).

```java
ServerSocket listener = new ServerSocket(port);
```

클라이언트의 접속을 기다린다. 클라이언트가 접속하면 통신용 소켓을 따로 만들어서 돌려준다.

```java
Socket socket = listener.accept();
```

I/O에서 이렇게 기다리는 걸 Blocking이라고 한다. 파일 읽기, 쓰기 등도 모두 Blocking 동작이지만, TCP 통신에서는 네트워크 상태 같은 요인에 의해 크게 지연될 수 있고, accept처럼 상대방의 요청이 없으면 영원히 기다리는 일이 벌어질 수 있다. 멀티스레드나 비동기, 이벤트 기반 처리 등이 필요한 이유다.

#### 2️⃣ Request

서버의 입장에서는 요청을 받는다. 클라이언트가 주는 것이고.

따라서 먼저 읽어야 한다.

코드는 위에서 다룬 것과 100% 동일하다.

#### 3️⃣ Response

클라이언트의 요청과 마찬가지로, 응답 메시지를 만들어서 전송하면 된다.

String message 보낼때 HTTP/1.1 200 ok 에서 띄우기를 더 하거나 하면 인식을 못해서 저렇게 요청이 온 그대로 반환해줘야 적용이 된다.

```
HTTP/1.1 200 OK
(빈 줄)
Hello, world!
```

Java 코드

```java
String message = """
	HTTP/1.1 200 OK
	
	Hello, world!
	""";
```

또는

```java
String message = "" +
	"HTTP/1.1 200 OK\\n" +
	"\\n" +
	"Hello, world!\\n";
```

⚠️ 마지막 줄에 Newline(\n)을 넣는 걸 잊지 말자.

제대로 하려면 Content-Type과 Content-Length를 더해주는 게 좋다.

```java
String body = "Hello, world!";
byte[] bytes = body.getBytes();
String message = "" +
	"HTTP/1.1 200 OK\\n" +
	"Content-Type: text/html; charset=UTF-8\\n" +
	"Content-Length: " + bytes.length + "\\n" +
	"\\n" +
	body;
```

⚠️ Content-Length로 정확한 크기를 알 수 있기 때문에 마지막 줄에 Newline(\n)을 넣지 않아도 된다.

전송 코드는 클라이언트와 100% 동일하다.

#### 4️⃣ Close

마찬가지로 클라이언트와 100% 동일하다.
