# HTTP Client

### TCP/IP 통신

tcp/ip 위에 http가 형성됨

> [인터넷\_프로토콜\_스위트](https://ko.wikipedia.org/wiki/%EC%9D%B8%ED%84%B0%EB%84%B7\_%ED%94%84%EB%A1%9C%ED%86%A0%EC%BD%9C\_%EC%8A%A4%EC%9C%84%ED%8A%B8)  그 중 tcp , ip가 제일 많이 사용됨

> [전송\_계층](https://ko.wikipedia.org/wiki/%EC%A0%84%EC%86%A1\_%EA%B3%84%EC%B8%B5) tcp , udp가 제일 유명함

#### TCP와 UDP

전송 계층의 대표적인 프로토콜

* TCP: 연결이 필요함. 전달 및 순서 보장. (전화)
* UDP: 연결하지 않고 데이터를 보냄. 전달 및 순서를 보장하지 않음. (편지)

#### Socket

* [Berkeley\_sockets](https://en.wikipedia.org/wiki/Berkeley\_sockets)
* [네트워크\_소켓](https://ko.wikipedia.org/wiki/%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC\_%EC%86%8C%EC%BC%93)

Socket과 Socket API를 구분해야 헷갈리지 않는다. (비트코인은 프로토콜 이지만 그 안에서 사용되는 화폐도 비트코인이다.)

socket 은 엔드포인트 , 서버와 클라이언트의 종착점이다. 둘이 연결되어서 어떻게 통신하는지를 프로그래밍하는게 socket api 를 사용하는 것.

Socket은 기본적으로 파일과 유사하게 다룰 수 있다(유닉스에서는 파일 디스크립터의 일종).

Java에서는 키보드 입력, 화면 출력, 파일 입출력 등과 마찬가지로 Stream(Java 8에서 도입된 Stream API가 아님에 주의!)으로 다룰 수 있다. (input output 등을 쓰는 Stream)

#### TCP 통신 순서

1. 서버는 접속 요청을 받기 위한 소켓을 연다. → Listen
2. 클라이언트는 소켓을 만들고, 서버에 접속을 요청한다. → Connect
3. 서버는 접속 요청을 받아서 클라이언트와 통신할 소켓을 따로 만든다. → Accept
4. 소켓을 통해 서로 데이터를 주고 받는다. → Send & Receive ⇒ 반복!
5. 통신을 마치면 소켓을 닫는다. → Close(양쪽 누구든 close할 수 있다) ⇒ 상대방은 Receive로 인지할 수 있다.

### HTTP 클라이언트

#### 1️⃣ Connect

호스트는 IP 주소 또는 도메인 이름을 사용할 수 있다. 도메인의 경우 DNS를 활용하기 때문에 제대로 하려면 복잡해질 수 있지만, 알아서 처리해 준다.

```java
String host = "example.com";
```

HTTP의 기본 포트 번호는 80.

```java
int port = 80;
```

IP 주소와 포트 번호만 알면, 서버에 접속할 수 있다.

```java
Socket socket = new Socket(host, port);
```

객체 생성이지만 여기서 바로 서버에 접속 요청한다. 실패하면 ConnectException 예외 발생.

#### 2️⃣ Request

요청 메시지를 만들고, TCP로 전송하면 된다.

```
GET <http://example.com/> HTTP/1.1
(빈 줄)
```

또는

```
GET / HTTP/1.1
Host: example.com
(빈 줄)
```

후자의 형태를 더 많이 쓴다.

⚠️ 마지막에 빈 줄을 넣는 걸 잊으면 안 된다.

Java 코드

```java
String message = """
	GET / HTTP/1.1
	Host: example.com

	""";
```

또는

```java
String message = "" +
	"GET / HTTP/1.1\\n" +
	"Host: example.com\\n" +
	"\\n";
```

소켓에서 Output Stream을 얻어서 쓸 수 있다.

* OutputStream : 바이트 기반 출력 스트림의 최상위 추상클래스. 모든 바이트 기반 출력 스트림 클래스는 이 클래스를 상속 받아 기능을 재정의 함.

```java
OutputStream outputStream = socket.getOutputStream();
outputStream.write(message.getBytes());
```

문자열을 직접 전송하고 싶다면 Writer를 쓴다(추천).

```java
OutputStreamWriter writer = new OutputStreamWriter(socket.getOutputStream());

writer.write(message);
writer.flush();
```

⚠️ 내부적으로 버퍼가 있기 때문에 flush를 잊지 않아야 한다.

\- flush() : FileWriter 내부 버퍼의 내용을 파일에 writer함. flush()를 호출하지 않는다면 내용이 버퍼에만 남고 파일에는 쓰이지 않는 상황이 나올 수 있음.

\- close() : FileWriter는 스트림을 이용하여 파일의 내용을 읽음. 이때 close()를 호출하여 스트림을 닫으면 그 스트림을 다시 이용하여 파일에 쓰는 것이 불가능.

#### 3️⃣ Response

소켓에서 Input Stream을 얻어서 쓸 수 있다.

* InputStream : 바이트 기반 입력 스트림의 최상위 추상클래스 (모든 바이트 기반 입력 스트림은 이 클래스를 상속받음.) 파일 데이터를 읽거나 네트워크 소켓을 통해 데이터를 읽거나 키보드에서 입력한 데이터를 읽을 때 사용.

```java
InputStream inputStream = socket.getInputStream();
```

Byte 배열을 준비하고, 여기로 데이터를 읽어온다. 응답 데이터가 우리가 준비한 배열보다 클 수도 있는데, 이 경우엔 반복해서 여러 번 읽는 작업이 필요하다. 이 경우엔 우리가 준비한 배열이 Chunk(한번에 처리하는 단위)가 된다. 단순하게 하기 위해 여기서는 한번만 읽는다.

```java
byte[] bytes = new byte[1_000_000];
int size = inputStream.read(bytes);
```

실제 데이터 크기만큼 Byte 배열을 자르고, 문자열로 변환해 출력한다.

```java
byte[] data = Arrays.copyOf(bytes, size);
String text = new String(data);

System.out.println(text);
```

요청과 마찬가지로 Reader를 쓰면 훨씬 편하다(추천).

```java
InputStreamReader reader = new InputStreamReader(socket.getInputStream());

CharBuffer charBuffer = CharBuffer.allocate(1_000_000);

reader.read(charBuffer);

charBuffer.flip();

System.out.println(charBuffer.toString());
```

⚠️ CharBuffer에서 읽기 전에 flip을 잊지 않아야 한다.

#### 4️⃣ Close

더이상 할 게 없으니 이제 close하면 된다.

```java
socket.close();
```

Socket은 Closeable이기 때문에 try-with-resources를 써도 된다.

```java
try (Socket socket = new Socket(host, port)) {
	// Request
	// Response
}
```

