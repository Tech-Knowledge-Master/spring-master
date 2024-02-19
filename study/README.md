# Spring

<details>
  <summary>Spring DI/IoC는 어떻게 동작하나요?</summary>
  </br>
  <p>IoC(제어의 역전)은 프로그램의 제어 흐름을 직접 제어하는 것이 아니라 외부에서 관리하는 것으로 코드의 최종호출은 개발자가 제어하는 것이 아닌 프레임워크의 내부에서 결정된 대로 이루어집니다.</p>
  <p>DI(의존관계 주입)은 Spring 프레임워크에서 지원하는 IoC의 형태로 클래스 사이의 의존관계를 빈 설정 정보를 바탕으로 컨테이너가 자동으로 연결해줍니다.</p>
  <p>스프링에서는 스프링 컨테이너 ApplicationContext를 이용하여 설정 정보를 생성, 등록하고 필요한 객체를 생성자 혹은 setter를 통해 주입합니다.</p>
</details>

<details>
  <summary>Spring Bean이란 무엇인가요?</summary>
  </br>
  <p>IoC 컨테이너 안에 들어있는 객체로 필요할 때 IoC컨테이너에서 가져와서 사용합니다. @Bean 을 사용하거나 xml설정을 통해 일반 객체를 Bean으로 등록할 수 있습니다.</p>
</details>

<details>
  <summary>스프링 Bean의 생성 과정을 설명해주세요.</summary>
  </br>
  <p>객체 생성 → 의존 설정 → 초기화 → 사용 → 소멸 과정의 생명주기를 가지고 있습니다. Bean은 스프링 컨테이너에 의해 생명주기를 관리하며 빈 초기화방법은 @PostConstruct 를 빈 소멸에서는 @PreDestroy 를 사용합니다.</p>
  <p>생성한 스프링 빈을 등록할 때는 ComponentScan을 이용하거나 @Configuration 의 @Bean 을 사용하여 빈 설정파일에 직접 빈을 등록할 수 있습니다.</p>
</details>

<details>
  <summary>스프링 Bean의 Scope에 대해서 설명해주세요.</summary>
  </br>
  <p>빈 스코프는 빈이 존재할 수 있는 범위를 뜻하며 싱글톤, 프로토타입, request, session, application 등이 있습니다.</p>
  <p>싱글톤은 기본 스코프로 스프링 컨테이너의 시작과 종료까지 유지되는 가장 넓은 범위의 스코프입니다.</p>
  <p>프로토타입은 빈의 생성과 의존관계 주입까지만 관여하고 더는 관리하지 않는 매우 짧은 범위의 스코프입니다.</p>
  <p>request는 웹 요청이 들어오고 나갈때까지 유지하는 스코프, session은 웹 세션이 생성, 종료할때까지, application은 웹 서블릿 컨텍스트와 같은 범위로 유지하는 스코프입니다.</p>
</details>

<details>
  <summary>IoC 컨테이너의 역할은 무엇이 있을까요?</summary>
  </br>
  <p>애플리케이션 실행시점에 빈 오브젝트를 인스턴스화하고 DI 한 후에 최초로 애플리케이션을 기동할 빈 하나를 제공해준다</p>
</details>

<details>
  <summary>DI 종류는 어떤것이 있고, 이들의 차이는 무엇인가요?</summary>
  </br>
  <p>DI는 세가지 방법이 있습니다. 생성자 삽입, Setter를 이용한 메소드 매개 변수 삽입, 필드 주입이 있습니다.</p>
  <p>생성자 주입은 생성자 호출시점에 딱 1번만 호출되는 것을 보장하며 불변, 필수 의존관계에 사용합니다.</p>
  <p>Setter주입은 선택, 변경 가능성이 있는 의존관계에 사용되며 스프링빈을 선택적으로 등록이 가능합니다.</p>
  <p>필드 주입은 `@Autowired` 를 사용하는데 외부에서 변경이 불가능하여 테스트 하기 힘듭니다. DI 프레임워크 없이는 작동하기 힘들며, 주로 애플리케이션과 관계없는 테스트코드나 `@Configuration` 같은 스프링 설정 목적으로 사용합니다. </p>
</details>

<details>
  <summary>Autowiring 과정에 대해서 설명해주세요.</summary>
  </br>
  <p>컨테이너에서 타입(인터페이스 또는 오브젝트)을 이용해 의존 대상 객체를 검색하고 할당할 수 있는 빈 객체를 찾아 주입한다</p>
</details>

<details>
  <summary>Spring Web MVC의 Dispatcher Servlet의 동작 원리에 대해서 간단히 설명해주세요.</summary>
  </br>
  <p></p>
</details>

<details>
  <summary>프론트 컨트롤러 패턴이란 무엇인가요?</summary>
  </br>
  <p>클라이언트의 다양한 요청마다 서블릿을 만들어서 사용한다고 하면 개발과 유지보수의 효율이 떨어질 수 밖에 없습니다. 프론트 컨트롤러 패턴을 사용함으로써 각 요청을 적절한 곳으로 위임해줌으로써 개발과 유지보수의 효율성이 증가하고 모든 요청에 대해 보안, 국제화, 라우팅 및 로그와 같은 일반적인 기능을 한 곳에서 캡슐화할 수 있습니다. Spring에서는 DispatcherServlet이 프론트 컨트롤러 패턴을 사용한 예이며, DispatcherServlet이 Bean으로 등록되어 package를 scan하고 @Controller, @RestController 애노테이션을 확인하여 어떠한 요청이 들어왔을 때 적절한 Handler Method에 위임해줍니다.</p>
</details>

<details>
  <summary>Servlet Filter와 Spring Interceptor의 차이는 무엇인가요?</summary>
  </br>
  <p>Filter는 Servlet Filter로써 javax.servlet 스펙에 포함되는 클래스입니다.</p>
  <p>Interceptor는 Spring MVC 스펙에 포함되어 있는 클래스입니다.</p>
  <p>Filter는 Servlet에서 전후처리를 담당하며, Interceptor는 Spring에서 Handler를 실행하기 전후나, ViewResolver를 통해 컨트롤러에서 리턴한 View Name으로부터 렌더링을 담당할 View 오브젝트를 준비해 돌려준 후 실제 View를 렌더링한 후에 어떠한 처리를 담당합니다.</p>
  <p>Filter는 Web Application(Tomcat을 사용할 경우 web.xml)에 등록하며, Interceptor는 Spring의 Application Context에 등록합니다.</p>
  <p>Filter는 Method Signature에 있는 Argument인 HttpServletRequest 혹은 HttpServeltResponse를 ServletRequest, ServletResponse 등으로 교체할 때 사용하거나, 데이터 변환(다운로드 파일의 압축 및 데이터 암호화 등), XSL/T를 이용한 XML 문서 변경, 사용자 인증, 자원 접근에 대한 로깅 등에 사용합니다.</p>
  <p>Interceptor의 경우 AOP를 흉내내거나, Spring 애플리케이션에서 전역적으로 전후처리 로직에서 예외를 사용하도록 하거나, Handler Method에서 사용자의 권한을 체크해서 다른 동작을 시켜준다거나 할 때 사용합니다.</p>
  <p></p>
</details>

<details>
  <summary>Spring에서 CORS 에러를 해결하기 위한 방법을 설명해주세요.</summary>
  </br>
  <p>Servlet Filter를 사용하여 커스텀한 Cors 설정하거나, WebMvcConfiguer를 구현한 Configuration 클래스를 만들어서 addCorsMappings()를 재정의할 수도 있고, 마지막으로 Spring Security에서 CorsConfigurationSource를 Bean으로 등록하고 config에 추가해줌으로써 해결할 수 있습니다.</p>
  <p>Controller 클래스에 @Crossorigin 어노테이션을 통해 해결할 수 있습니다.</p>
</details>

<details>
  <summary>Bean/Component 어노테이션에 대해서 설명해주시고, 둘의 차이점에 대해 설명해주세요.</summary>
  </br>
  <p>두 어노테이션 모두 IoC 컨테이너에 Bean을 등록하기 위해 사용합니다</p>
  <p>@Component : 개발자가 작성한 class를 기반으로 실행시점에 인스턴스 객체를 1회(싱글톤) 생성합니다</p>
  <p>@Controller, @Service, @Repository 는 모두 @Component 이며 실행시점에 자동으로 의존성을 주입합니다</p>
  <p>@Bean : 개발자가 작성한 method를 기반으로 메서드에서 반환하는 객체를 인스턴스 객체로 1회(싱글톤) 생성합니다</p>
</details>

<details>
  <summary>POJO란 무엇인가요? Spring Framework에서 POJO는 무엇이 될 수 있을까요?</summary>
  </br>
  <p>POJO는 프레임워크 인터페이스, 클래스를 구현하거나 확장하지 않은 단순한 클래스로 Java에서 제공하는 API 외에 종속되지 않습니다. 특정 환경에 종속되지 않아 코드가 간결하고 테스트 자동화에 유리합니다. 스프링에서는 도메인과 비즈니스 로직을 수행하는 대상이 POJO대상이 될 수 있습니다.</p>
</details>

<details>
  <summary>Spring Web MVC에서 요청 마다 Thread가 생성되어 Controller를 통해 요청을 수행할텐데, 어떻게 1개의 Controller만 생성될 수 있을까요?</summary>
  </br>
  <p>@Controller 어노테이션을 타고 들어가보면 @Component라는 어노테이션이 붙어 있습니다. 따라서 컨트롤러는 IoC컨테이너에 등록되어 Spring bean으로 관리됩니다. Spring의 빈 생성 전략의 기본은 싱글턴입니다. IoC컨테이너에 Controller Bean은 싱글턴 전략에 의해 1개만 존재하고 Application이 Init 되는 시점에 초기화됩니다. 그리고 실제 사용되는 시점에 의존성 주입을 통해서 사용됩니다. 요청시마다 새로 Bean을 생성해서 사용하는 것이 아닌 이미 생성되어있는 Bean을 가져다 쓰게됨으로써 여러개의 Thread에서 Contoller를 사용해도 1개의 동일한 컨트롤러인 것입니다. 만약 요청이 올때마다 새로운 컨트롤러가 생기길 바란다면 Bean scope를 Singleton 이 아닌, request 등으로 설정하면 요청이 들어올 때 혹은 지정한 전략마다 새로운 컨트롤러 Bean이 생기도록 할 수 있습니다.</p>
</details>

<details>
  <summary>Spring WEB MVC의 근간에는 Java Servlet 이 있는데요. Spring 은 Servlet을 어떻게 구성해서 이를 구현했을까요?</summary>
  </br>
  <p>Servlet은 Java로 웹페이지를 구성할 때 동적으로 웹페이지를 구성해주는 자바 클래스 입니다. Spring에서도 이 Servlet을 사용하고 있지만 특성이 조금 다릅니다. 기본적으로 Java의 Servlet은 하나의 Request에 대해서 하나의 Servlet을 생성합니다. 이 방법은 간단하고 직관적이지만 Servlet이 많이 생성되면 관리하기 힘들어지는 단점이 있습니다. 반면 Spring의 경우에는 DispatcherServlet이라는 FrontController 패턴을 사용해서 중앙에서 하나의 Servlet이 요청을 받아서 HandlerMapping을 통해 그에 맞는 컨트롤러로 분배하는 방식을 사용합니다. 이렇게 할 경우 하나의 객체에서 모든 요청을 먼저 처리하기 때문에 재사용성 및 유연한 매핑, 인터셉터의 사용, 관리의 용이성 등이 있겠습니다.</p>
</details>

<details>
  <summary>Filter는 Servlet의 스펙이고, Interceptor는 Spring MVC의 스펙입니다. Spring Application에서 Filter와 Interceptor를 통해 예외를 처리할 경우 어떻게 해야 할까요?</summary>
  </br>
  <p>Filter는 DispatcherServlet 외부에 존재하기 때문에 예외가 발생했을 때 ErrorController에서 처리해야 합니다. 하지만 Interceptor는 DispatcherServlet 내부에 존재하기 때문에 @ControllerAdvice를 적용해서 처리할 수 있습니다.</p>
</details>

<details>
  <summary>Spring Application을 구동할 때 메서드를 실행시키는 방법에 대해 설명해주세요.</summary>
  </br>
  <p>CommandLineRunner, ApplicationRunner를 구현한 클래스를 만들어서 실행시키는 2가지 방법이 있습니다. 또한 Spring의 ApplicationEvent를 사용한 방법, @Postconstruct를 사용한 방법, InitializingBean 인터페이스를 구현하는 방법, @Bean의 initMethod를 사용한 방법이 있습니다.</p>
</details>

<details>
  <summary>의존성과 설정값을 생성자 인자로 주입해야 하는 이유에 대해 설명해주세요.</summary>
  </br>
  <p>모든 의존성을 생성자를 통해 주입하면, 인스턴스 생성 시 즉시 어떠한 동작을 실행할 수 있습니다. 또한 추가적인 설정은 필요하지 않으며, 뜻하지 않게 의존성과 설정값을 빠뜨리는 일이 발생하지 않고 테스트에도 용이합니다.</p>
</details>

---
### Spring 추가 질문들
### ( 메인 질문 대답 작성하실 때, 이 부분도 고려해서 작성해주시면 좋을 거 같아요 )

1) Spring Framework란 무엇인가요?
2) Spring에서 Service, Controller, Repository Annotaion의 차이점이 어떻게 되나요?
3) Spring에서 Controller, RestController의 차이는 어떻게 되나요?
4) Spring에서 Service와 Component의 차이는 어떻게 되나요?
5) 다른 프레임워크도 많은데, 왜 굳이 Spring을 쓰셨나요? Spring의 장점이 뭔가요?
6) IoC Container를 직접 만든다면, 어떻게 구현하실 생각인가요?
7) Spring에서 Bean을 등록하는 방법은 어떻게 되나요?
8) ControllerAdvice가 무엇인가요?
9) Spring MVC에서 요청이 들어왔을 때부터 응답이 나갈 때까지의 흐름을 설명해주세요.
10) Field 주입, 생성자 주입, Setter 주입에 대해 설명해주세요.
11) Spring Web MVC에서 요청이 들어와서 DB까지의 흐름을 설명해주세요.
12) AOP에 대해 설명해주세요.
13) Spring MVC 구조와 처리과정에 대해 설명해주세요.
14) Spring과 SpringBoot의 차이는 무엇인가요?
15) SpringBoot의 장점은 무엇인가요?
16) Servlet이 무엇인가요?
17) Lombok이 생성하는 메서드가 어느 시점에서 생성되는지 아시나요?
18) Deep Copy와 Shallow Copy에 대해 설명해주세요 
19) VO란 무엇인가요? DTO란 무엇인가요? DAO란 무엇인가요?
20) Layered Architecture에서 Presentation, Application, Domain, Infrastructure layer의 역할에 대해 설명해주세요.
21) @RequestParam, @RequestBody, @ModelAttribute 어노테이션에 대해 설명해주세요.
22) Spring Security에 대해 설명해주세요. JWT, OAuth에 대해 설명해주세요.
23) JDK Dynamic Proxy와 CGLIB의 차이에 대해 설명해주세요.
24) Spring MVC1 vs MVC2의 차이에 대해 설명해주세요.
25) PSA란 무엇인가요?
26) Weaving은 무엇인가요?
27) HttpMessageConverter에 대해 설명해주세요.
28) ArgumentResolver에 대해 설명해주세요.
29) @Scheduled, @Async, @SessionAttribute, @SessionAttributes 어노테이션에 대해 설명해주세요.
30) ViewResolver, Conterter, Formatter에 대해 설명해주세요.
31) Spring의 Logging에 대해 설명해주세요.

# JPA

<details>
  <summary>JPA 영속성 컨텍스트의 이점(5가지)을 설명해주세요.</summary>
  </br>
  <p>영속성 컨텍스트는 엔티티를 영구 저장하는 환경을 의미합니다.</p>
  <p>영속성 컨텍스트를 쓰는 이유는 1차 캐시, 동일성 보장, 쓰기 지연, 변경감지(Dirty checking), 지연로딩이 있습니다.</p>
  <ul>
    <li>1차 캐시: 조회가 가능하며 1차 캐시에 없으면 DB에서 조회하여 1차 캐시에 올려 놓습니다.</li>
    <li>동일성 보장: 동일성 비교가 가능합니다.(==)</li>
    <li>쓰기 지연: 트랜잭션을 지원하는 쓰기 지연이 가능하며 트랜잭션 커밋하기 전까지 SQL을 바로 보내지 않고 모아서 보낼 수 있습니다.</li>
    <li>변경 감지(Dirty checking): 스냅샷을 1차 캐시에 들어온 데이터를 찍습니다. commit 되는 시점에 Entity와 스냅샷과 비교하여 update SQL을 생성합니다.</li>
    <li>지연 로딩: 엔티티에서 해당 엔티티를 불러올 때 그 때 SQL을 날려 해당 데이터를 가져옵니다.</li>
  </ul>
</details>

<details>
  <summary>JPA Propagation 전파단계를 설명해주세요.</summary>
  </br>
  <p>대기업면접에서 나왔던 질문으로 트랜잭션 고립단계와 같이 질문할 가능성이 있습니다.</p>
  <p>JPA Propagation은 트랜잭션 동작 도중 다른 트랜잭션을 호출(실행)하는 상황에 선택할 수 있는 옵션입니다.</p>
  <p>@Transactional의 propagation 속성을 통해 피호출 트랜잭션의 입장에서는 호출한 쪽의 트랜잭션을 그대로 사용할 수도 있고, 새롭게 트랜잭션을 생성할 수도 있습니다.</p>
  <p>REQUIRED(디폴트): 부모 트랜잭션 내에서 실행하며 부모 트랜잭션이 없을 경우 새로운 트랜잭션을 생성합니다.</p>
  <p>이 외에도 종류가 REQUIRES_NEW, SUPPORTS, MANDATORY, NOT_SUPPORT, NEVER, NESTED 가 있지만 신입이 실제로 다뤄본 경험이 적기 때문에 REQUIRED(디폴트)값만 답변했습니다.</p>
</details>

<details>
  <summary>JPA를 쓴다면 그 이유에 대해서 설명해주세요.</summary>
  </br>
  <p>사실 면접관이 의도한 바를 파악하는게 중요합니다. 각기 다른 조건에서 같은 질문을 들었을 때 대답을 다르게 했던 기억이 납니다.</p>
  <p>제가 JPA를 사용하는 이유는 객체지향 프레임워크이기 때문입니다. JPA를 사용하면 비즈니스 로직이 RDBMS에 의존하는 것이 아니라, 자바 코드로 표현될 수 있기 때문입니다. 그로 인해서 생산성이 높아진다고 볼 수 있습니다.(이는 JPA에 익숙하다는 것을 전제로 합니다.)</p>
  <p>또, JPA는 JPQL로 SQL을 추상화하기 때문에 RDBMS Vendor에 관계없이 동일한 쿼리를 작성해서 같은 동작을 기대할 수 있다는 장점도 가지고 있습니다. 이는 database dialect를 지원하기 때문에 가지는 장점입니다.</p>
</details>

<details>
  <summary>N + 1 문제는 무엇이고 이것이 발생하는 이유와 이를 해결하는 방법을 설명해주세요.</summary>
  </br>
  <p>JPA와 관련된 단골문제입니다. 꼭 학습해둡시다.</p>
  <p>N + 1 쿼리 문제는 즉시 로딩과 지연 로딩 전략 각각의 상황에서 발생할 수 있습니다. 하위 엔티티들이 존재하는 경우 한 쿼리에서 모두 가져오는 것이 아닌, 필요한 곳에서 각각 쿼리가 발생하는 경우를 이릅니다.</p>
  <p>즉시 로딩에서 발생하는 이유는 JPQL을 사용하는 경우 전체 조회를 했을 때, 영속성 컨텍스트가 아닌 데이터베이스에서 직접 데이터를 조회한 다음 즉시로딩 전략이 동작하기 때문입니다.<br>
  지연 로딩에서 발생하는 이유는 지연로딩 전략을 사용한 하위 엔티티를 로드할 때, JPA에서 프록시 엔티티를 unproxy 할 때 해당 엔티티를 조회하기 위한 추가적인 쿼리가 실행되어 발생합니다.</p>
  <p>해결 방법으로는 Fetch Join이라고 불리는 JPQL의 join fetch를 사용하는 방법이 있으며, 또 다른 방법으로는 <code>@EntityGraph</code>를 사용하는 방법, <code>@Fetch(FetchMode.SUBSELECT)</code>를 사용하는 방법, <code>@BatchSize</code>를 사용해 조절하거나 전역적인 batch-size를 설정하는 방법이 있습니다.</p>
  <p>각 해결방안에 대한 유의점은 작성하지 않습니다.</p>
</details>

---
### JPA 추가 질문들
1) JPA란 무엇인가요?
2) JPA는 왜 쓰는건가요? ORM은 어떤 장점이 있죠? 쓰면서 불편한점이 있었나요?
3) ManyToOne을 쓴 이유? 반대쪽에서 OneToMany를 쓸 수도 있지 않나요?
4) Open Session in View
5) JPA 사용할 때랑 직접 SQL 사용할 때의 차이가 있나요?
6) @Transactional 어노테이션의 동작과정에 대해 설명해주세요. readOnly를 붙이는 이유가 뭘까요?
7) JPA FetchType의 Lazy, Eager을 어떤 기준으로 사용하나요? 즉시 로딩과 지연 로딩의 차이가 무엇인가요?
8) JPA에서 PK는 어떻게 설정하나요?
9) 본인이 생각하기에 칼럼이 많고 적음의 기준이 있나요? 
10) PreparedStatement와 Statement의 차이는 무엇인가요?
11) JPA에서 Entity를 설계할 때 주의할 점이 있나요?
12) DB 커넥션 풀 ( HikariCP )에 대해 설명해주세요.

---
핵심 질문 원본 레포 : https://github.com/ksundong/backend-interview-question <br>
참고하면 좋을 레포 : https://github.com/NKLCWDT/cs?tab=readme-ov-file
