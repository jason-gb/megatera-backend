# REST API

### 학습 키워드

* API(Application Programming Interface)
* 정보은닉(Information Hiding)과 캡슐화(Encapsulation)
  * 그리고 이 둘의 차이(많이들 혼용하니까 잘 알아두세요)
* Architecture와 Architecture Style의 차이
* REST(7가지 제약 조건 위주로 정리)
  * 교재에 나온 `필딩 제약 조건`을 좀 더 풀어서 정리해보세요.
  * 아래 2가지 자료를 보시면 도움이 되실 겁니다.
  * [https://www.youtube.com/watch?v=RP\_f5dMoHFc](https://www.youtube.com/watch?v=RP\_f5dMoHFc)
  * [https://blog.npcode.com/2017/03/02/바쁜-개발자들을-위한-rest-논문-요약/](https://blog.npcode.com/2017/03/02/%EB%B0%94%EC%81%9C-%EA%B0%9C%EB%B0%9C%EC%9E%90%EB%93%A4%EC%9D%84-%EC%9C%84%ED%95%9C-rest-%EB%85%BC%EB%AC%B8-%EC%9A%94%EC%95%BD/)
  * [https://blog.npcode.com/2017/04/03/rest의-representation이란-무엇인가/](https://blog.npcode.com/2017/04/03/rest%EC%9D%98-representation%EC%9D%B4%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%B8%EA%B0%80/)



* 시스템을 여러 Tier/Layer로 구분. Tier는 물리적인 구분, Layer는 논리적인 구분.\
  사용자에 가까운 부분을 **Front-end**, 줄여서 F/E라고 부르고, 사용자에게서 먼 부분을 **Back-end**, 줄여서 B/E라고 부르고 거칠게 이야기하면, 서버는 백엔드, 클라이언트는 프론트엔드에 해당한다.

## - 우리가 만드는 것은 백엔드이지만 브라우저 자체를 만드는게 아니라 서  비스를 제공하는 한 부분적 요소를 만드는 것임

* API (application programming interface) 애플리케이션 프로그래밍 인터페이스\
  \- 구현에 관한것을 관여하기 보다는 커뮤니케이션\
  \- 인터페이스로 구성 되어있음

#### Interface

* Communication : 소통
* Specification : 드러내지 않음
* Information Hiding (Principle) : 정보 은닉
* Encapsulation (Technique) : 캡슐화
* Implementation : 분리됨, on & off

[REST](https://ko.wikipedia.org/wiki/REST) (Representational State Transfer)

* 다양한 방식의 버튼 작동방법이 존재하는데 그것을 규약한 방식

#### \[ 제약 조건 ]

1️⃣ **Starting with the Null Style**

2️⃣ **Client-Server**

3️⃣ **Stateless**

4️⃣ **Cache**

5️⃣ **Uniform Interface → 핵심!**

1. "REST 아키텍처 스타일을 다른 네트워크 기반 스타일과 구별하는 **중요한 특징**은 구성 요소 간의 **일관된 인터페이스**에 대한 강조입니다."
2. "**일반성** 소프트웨어 공학 원칙을 구성 요소 인터페이스에 적용함으로써 전체 시스템 아키텍처가 **간소화**되고 상호작용의 **가시성**이 향상됩니다."
3. "**구현체**는 제공하는 서비스와 **결합도**가 낮아져 **독립적인 발전 가능성**을 촉진합니다."
4. "그러나 **무엇이 손실될 수 있는지**, 일관된 인터페이스는 **효율성이 저하**되는데, 이는 정보가 **표준화된 형식**으로 전달되기 때문에 특정 애플리케이션의 요구에 특화된 형식이 아닙니다."
5. "REST 인터페이스는 **대규모 초미디어 데이터 전송**에 효율적으로 설계되었으며, 웹의 **일반적인 케이스를 최적화**하지만, 다른 형태의 아키텍처적 상호작용에 대해 최적이 아닌 인터페이스로 이어집니다."
6. **필딩 제약 조건**
   1.  Four Interface Constraints

       Identification of Resources → URI 등으로 리소스를 식별할 수 있다.

       Manipulation of Resources through Representations → 표현으로 리소스를 조작한다.

       Self-descriptive Messages → 메시지는 자기서술적이기 때문에 여러 레이어에서 처리/변환 가능하다.

       > JSON 같은 범용 포맷을 작게 사용하면 어떻게 해석해야 하는지 알 수 없기 때문에 자기서술적이기 어렵다. 뒤에서 다룰 MIME 타입으로 설명한다면, application/json이 아니라 application/dns+json 같은 타입을 써야 한다.

       > REST API를 이야기할 때 까다로운 부분 중 하나.

       Hypermedia as the Engine of Application State → 줄여서 HATEOAS라고 부른다. REST API를 이야기할 때 까다로운 부분 중 하나.
   2.  아키텍처 요소(5.2)에서 리소스와 표현을 구분

       Resource → 추상. ⇒ 특정 시점의 스냅샷이 아니라, 모든 시간에 통용되는 엔티티 집합. 객체지향에서 말하는 Entity라고 생각하면 편하다. <객체지향의 사실과 오해>의 표현을 빌린다면, “앨리스”라는 리소스는 키가 커지던 작아지던 항상 “앨리스”다.



       Representation → Data + Metadata + Meta-metadata… ⇒ 사실상 HTTP 메시지라고 보면 됨. 예를 들어, 리소스를 어떻게 조작할 것인가는 HTTP Method로 표현하게 되고, 리소스를 무엇으로 조작할 것인가는 Content-Type과 Body로 표현하게 된다.


   3.  URI 파트(6.2)에서 리소스에 대해 다시 강조

       “The resource is not the storage object. The resource is not a mechanism that the server uses to handle the storage object.”\
       "리소스는 저장 객체가 아닙니다. 리소스는 서버가 저장 객체를 처리하는 데 사용하는 메커니즘도 아닙니다." \
       리소스, 표현, 실제 데이터 등은 전부 구분된다.\

   4.  아키텍처 데이터 뷰(5.3.3)에서 HATEOAS에 대해 언급.

       마지막 문단의 첫 문장: “The model application is therefore an **engine** that moves from one state to the next by examining and **choosing** from among the alternative **state transitions** in the current set of **representations**.”

       > 이렇게 하려면 표현에 선택 가능한 상태 전환이 포함돼야 한다.

       > 이게 바로 하이퍼미디어 링크.



       대부분은 효율 문제로 표현에 링크를 넣지 않고, 클라이언트 개발자가 API 문서를 활용해 처리한다. 표현에서 상태 전환을 선택하는 게 아니라, API 문서를 참조해서 상태 전환을 강제하는 것.

       \
       &#x20;[Richardson Maturity Model](https://martinfowler.com/articles/richardsonMaturityModel.html)

       > \<RESTful Web API>의 공저자인 레오나르드 리처드슨은 Hypermedia Control(대표적인 게 바로 링크)을 강조.

       > 성숙한 REST라면 표현에 하이퍼미디어 컨트롤(링크)이 포함되어야 한다.



6️⃣ **Layered System**

7️⃣ **Code-On-Demand**

REST는 API를 위한 아키텍처 스타일이 아니다. 논문에서 밝힌 것처럼 “common case of the Web”에 특화된 방법이다. 하지만 API를 만들 때 유용하게 활용할 수 있다.

로이 필딩은 필딩 제약 조건을 지키지 않는 API를 REST API라고 부르는 것에 반대하겠지만, 업계에서 그냥 리처드슨 성숙도 모델의 레벨 2만 만족해도 REST API라고 부르고 있기 때문에 여기서도 그냥 REST API라고 이야기할 예정.

사실 이번에 배우는 내용은 REST에 관한 내용이라 REST API까지도 가지도 못함\
그래서 그냥 슬 훑어보면 될듯?
