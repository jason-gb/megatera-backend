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
