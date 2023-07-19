# HTTP Client

### TCP/IP 통신

> [인터넷\_프로토콜\_스위트](https://ko.wikipedia.org/wiki/%EC%9D%B8%ED%84%B0%EB%84%B7\_%ED%94%84%EB%A1%9C%ED%86%A0%EC%BD%9C\_%EC%8A%A4%EC%9C%84%ED%8A%B8)

> [전송\_계층](https://ko.wikipedia.org/wiki/%EC%A0%84%EC%86%A1\_%EA%B3%84%EC%B8%B5)

#### TCP와 UDP

전송 계층의 대표적인 프로토콜

* TCP: 연결이 필요함. 전달 및 순서 보장. (전화)
* UDP: 연결하지 않고 데이터를 보냄. 전달 및 순서를 보장하지 않음. (편지)

#### Socket

* [Berkeley\_sockets](https://en.wikipedia.org/wiki/Berkeley\_sockets)
* [네트워크\_소켓](https://ko.wikipedia.org/wiki/%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC\_%EC%86%8C%EC%BC%93)

Socket과 Socket API를 구분해야 헷갈리지 않는다.

Socket은 기본적으로 파일과 유사하게 다룰 수 있다(유닉스에서는 파일 디스크립터의 일종).

Java에서는 키보드 입력, 화면 출력, 파일 입출력 등과 마찬가지로 Stream(Java 8에서 도입된 Stream API가 아님에 주의!)으로 다룰 수 있다.

#### TCP 통신 순서

1. 서버는 접속 요청을 받기 위한 소켓을 연다. → Listen
2. 클라이언트는 소켓을 만들고, 서버에 접속을 요청한다. → Connect
3. 서버는 접속 요청을 받아서 클라이언트와 통신할 소켓을 따로 만든다. → Accept
4. 소켓을 통해 서로 데이터를 주고 받는다. → Send & Receive ⇒ 반복!
5. 통신을 마치면 소켓을 닫는다. → Close ⇒ 상대방은 Receive로 인지할 수 있다.
