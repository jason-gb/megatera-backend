# Spring Web MVC

### 학습 키워드

* [Spring](https://docs.spring.io/spring-framework/docs/current/reference/html/overview.html#overview)(링크된 문서에서 핵심을 캐치할 것, 괴롭지만 한 번은 해내야 함)
* Spring Boot
* Spring initializer
  * 링크 : https://start.spring.io/
* Web Server와 Web Application Server(WAS)
  * Tomcat
*   Model-View-Controller(MVC) 아키텍처 패턴

    1 . View -> 표현

    2 . Contriller -> 입력&#x20;

    3 . Model -> 그 외의 모든 것
* 관심사의 분리(Seperation of Concern) - MVC가 추구하는 것
* Spring MVC
* Java Annotation
* Spring Annotation
  * @RestController
    * @Controller
    * @ResponseBody
  * @GetMapping
    * @RequestMapping

**Controller**

```java
@RestController 
public class WelcomeController { 
@GetMapping("/") public String home() { 
return "Hello, world!"; 
} }
```

Annotation이 보이면 전부 들어가서 뭔지 확인하는 습관 !
