# Spring Bean이란 무엇인가요?

IoC 컨테이너 안에 있는 객체로 필요할 때 IoC 컨테이너에서 가져와서 사용한다.

## 스프링 빈 vs 자바 빈
### 자바 빈
* 특정 형태의 클래스를 가리킴 - DTO 혹은 VO 형태
* private 필드, getter/setter 통해서만 접근 가능, 전달 인자가 없는 생성자를 가지는 형태의 클래스
* POJO 와 거의 동일
### 스프링 빈 
  * IoC 컨테이너가 관리하는 자바 객체
    * 스프링에 의해 생성되고, 라이프 사이클을 수행하고, 의존성 주입이 일어나는 객체들
    * 개발자가 관리하는 객체가 아닌 스프링에게 제어권을 넘긴 객체
* 스프링빈으로 자바 빈을 사용했었음
* setter가 문제가 되므로 스프링 빈이 자바 빈을 사용안함


## 스프링 빈 등록하는 방법
### @Bean
* 메서드 위에 선언가능하고, 외부 라이브러리를 Bean 으로 등록할 때 사용됨
  * 외부 라이브러리의 경우 ReadOnly File 이므로 개발자가 직접 컨트롤 할 수 없어 @Component 선언이 불가능하다. 따라서 외부 라이브러리를 빈으로 등록해야한다면 인스턴스를 생성하는 메소드를 만든 후 그 메서드에 빈을 선언해 빈으로 등록해야한다.
  * 예시
    ```java
        @Bean
        public PasswordEncoder passwordEncoder(){
            return new BCryptPasswordEncoder();
         }   
    ```
    
### @Component
* 클래스 위에 선언 가능하고, 직접 컨트롤리 가능한 객체에서 사용된다.

## 스프링 컨테이너, IoC 컨테이너, DI 컨테이너

(1) 수동으로 빈 관리, BeanFactory
- BeanFactory는 빈을 등록하고 생성하고 조회하고 돌려주는 등 빈을 관리하는 역할
- getBean() 메소드를 통해 빈을 인스턴스화할 수 있다.
- 처음으로 getBean() 메소드가 호출된 시점에서야 해당 빈을 생성 -> lazy loading 으로 작동하기 때문에 애플리케이션이 실행될 때 빈 객체들이
  생성되지 않고 해당 빈 객체를 조회할 때 생성된다.

```java
@Configuration
public class AppConfig {

    @Bean
    public OrderService orderService() {
        return new OrderServiceImpl(discountPolicy());
    }

    @Bean
    public FixDiscountPolicy discountPolicy() {
        return new FixDiscountPolicy();
    }
}

//활용법
public class Main {

    public static void main(String[] args) {
        final BeanFactory beanFactory = new AnnotationConfigApplicationContext(AppConfig.class);
        final OrderService orderService = beanFactory.getBean("orderService", OrderService.class);
        final Order order = orderService.createOrder(15, "샤프", 3000);
        System.out.println(order.getDiscountPrice());
    }
}
```

(2) 수동으로 빈 관리, ApplicationContext
- 빈의 프리로딩 지원-!!
- ApplicationContext도 BeanFactory처럼 빈을 관리할 수 있다.
- BeanFactory 를 상속 받았다.
- 스프링 컨테이너는 ApplicationContext 를 의미한다고 봐도 된다:)
- Context 초기화 시점에 모든 싱글톤 빈을 미리 로드한 후 애플리케이션 가동 후에는 빈을 지연 없이 받을 수 있다. 이 점 때문에 스프링 컨테이너로 ApplicationContext를 채택함

```java
public class Main {

    public static void main(String[] args) {
        final ApplicationContext beanFactory = new AnnotationConfigApplicationContext(AppConfig.class);
        final OrderService orderService = beanFactory.getBean("orderService", OrderService.class);
        final Order order = orderService.createOrder(15, "샤프", 3000);
        System.out.println(order.getDiscountPrice());
    }
```


(3) 설정 정보 없이 자동으로 등록, 컴포넌트 스캔
```
@Configuration
@ComponentScan
public class AppConfig {

}
@Component
public class OrderServiceImpl implements OrderService {

    private final DiscountPolicy discountPolicy;

    (@Autowired 생략가능)
    public OrderServiceImpl(DiscountPolicy discountPolicy) {
        this.discountPolicy = discountPolicy;
    }

    @Override
    public Order createOrder(int age, String itemName, int itemPrice) {
        int discountPrice = discountPolicy.discount(age, itemPrice);
        return new Order(itemName, itemPrice, discountPrice);
    }
}

@Component
public class RateDiscountPolicy implements DiscountPolicy {

    private static final int ADULT = 20;
    private static final int DISCOUNT_PERCENT = 10;

    @Override
    public int discount(int age, int price) {
        if (age < ADULT) {
            return price * DISCOUNT_PERCENT / 100;
        }
        return 0;
    }
}
//활용법
public class Main {

    public static void main(String[] args) {
        final ApplicationContext context = new AnnotationConfigApplicationContext(AppConfig.class);
        final OrderService orderService = context.getBean(OrderService.class);
        final Order order = orderService.createOrder(15, "연필", 3000);
        System.out.println(order.getDiscountPrice());
    }
}
```
- 빈을 자동 등록할 때 빈의 이름은 등록하려는 객체의 맨앞 글자를 소문자로 바꾸고 나머지는 그대로 쓰기 때문에 이름을 등록하지 않아도된다.
- @ComponentScan이 @Component가 붙은 모든 객체를 찾아서 빈으로 등록한다.
