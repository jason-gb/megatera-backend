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



