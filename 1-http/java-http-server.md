# Java HTTP Server

### Java HTTP Server

* [Module jdk.httpserver](https://docs.oracle.com/en/java/javase/17/docs/api/jdk.httpserver/module-summary.html)
* [Package com.sun.net.httpserver](https://www.notion.so/1-HTTP-7b084920331548a9a4ebd9b518a27f7f?pvs=21)
* [Non-blocking\_I/O\_(Java)](https://en.wikipedia.org/wiki/Non-blocking\_I/O\_\(Java\))

내부적으로 NIO를 사용하는 고수준 HTTP 서버 API.

#### 1️⃣ 서버 객체 준비

```java
InetSocketAddress address = new InetSocketAddress(8080);
int backlog = 0;

HttpServer httpServer = HttpServer.create(address, backlog);
```

* HttpServer class 사용시  404error가 떠야 하는데 나는 Connection reset by peer가 계속해서 떠서 이게 뭔가 확인 해봤더니 클라이언트가 요청을 보냈는데 연결이 끊겼다고 서버쪽에서 다시 요청을 보내라는 신호였다.\
  그래서 찾아보다가 (사실 못찾아서 물어봤음) 알고보니 HttpServer를 사용해야 하는데 HttpsServer를 내가 사용하는 바람에 나온 에러였다.
* http는 일반 텍스트로 전송하지만 https는 데이터가 암호화 되어서 전송되기 때문에 아직은 배우지 않았지만 아마 어떠한 key를 주고받아야 하는 부분 같다.

#### 2️⃣ URL(정확히는 path)에 핸들러 지정

tip. 인터페이스에 메서드가 하나 있는 것들은 람다 사용가능 아래 예시가 람다 사용하는 예시

```java
httpServer.createContext("/", (exchange) -> {
	// TODO
});
```

#### 3️⃣ Listen

```java
httpServer.start();
```

#### ➡️ Request

HTTP Method

```java
String method = exchange.getRequestMethod();
System.out.println(method);
```

HTTP path

```java
URI uri = exchange.getRequestURI();
String path = uri.getPath();
System.out.println(path);
```

Headers

```java
Headers headers = exchange.getRequestHeaders();
for (String key : headers.keySet()) {
	System.out.println(key + ": " + headers.get(key));
}
```

Body

```java
InputStream inputStream = exchange.getRequestBody();
String body = new String(inputStream.readAllBytes());
System.out.println(body);
```

#### ⬅️ Response

데이터를 Byte 배열로 준비.

```java
String body = "Hello, world!";
byte[] bytes = body.getBytes();
```

HTTP Status Code와 Content-Length 지정.

```java
exchange.sendResponseHeaders(200, bytes.length);
```

데이터 전송.

```java
OutputStream outputStream = exchange.getResponseBody();
outputStream.write(bytes);
outputStream.flush();
```



&#x20;너무 너저분 하다고 생각이 들었음 .

그 때 바로 아샬님께서 말씀해주시길 현업에서는 명확한 명칭을 가진 메소드화를 시켜야 한다고 하셔서 정말 기초적인 메소드화 진행

Request 1개 Response 1개씩 메소드화 진행&#x20;

Request 는 displayRequest라는 메소드 생성 후 상태찾는 형태의



