## Spring Application을 구동할 때 메서드를 실행시키는 방법에 대해 설명해주세요.

---

1. CommandLineRunner와 ApplicationRunner 인터페이스 구현
- 애플리케이션이 시작될 때 로직을 실행하는 편리한 방법
- 해당 인터페이스의 run 메서드는 Spring ApplicationContext가 완전히 로드되고 애플리케이션이 실행된 직후에 호출된다
- CommandLineRunner code example 🔽
```java
    import org.springframework.boot.CommandLineRunner;
    import org.springframework.stereotype.Component;
    
    @Component
    public class MyCommandLineRunner implements CommandLineRunner {
        @Override
        public void run(String... args) throws Exception {
            // 여기에 실행하고 싶은 코드를 넣습니다.
            System.out.println("애플리케이션이 시작될 때 실행됩니다.");
        }
    }
  ```
- ApplicationRunner code example 🔽
```java
    import org.springframework.boot.ApplicationRunner;
    import org.springframework.boot.ApplicationArguments;
    import org.springframework.stereotype.Component;

    @Component
    public class MyAppRunner implements ApplicationRunner {
        @Override
        public void run(ApplicationArguments args) throws Exception {
            // 여기에 실행하고 싶은 코드를 넣습니다.
            System.out.println("애플리케이션이 시작될 때 실행됩니다.");
        }
    }
```


2. @EventListener 어노테이션
- 애플리케이션 이벤트가 발생했을 때 실행되어야 하는 메서드를 정의
- 특히, ApplicationReadyEvent를 사용하면 애플리케이션이 완전히 시작된 후에 메서드를 실행 가능
```java
    import org.springframework.boot.context.event.ApplicationReadyEvent;
    import org.springframework.context.event.EventListener;
    import org.springframework.stereotype.Component;
    
    @Component
    public class MyApplicationListener {
        @EventListener(ApplicationReadyEvent.class)
        public void doSomethingAfterStartup() {
            System.out.println("애플리케이션이 준비되고 나서 실행됩니다.");
        }
    }
```


3. @PostConstruct 어노테이션
- Java EE 5에서 소개된 어노테이션
- 의존성 주입이 완료된 후, 초기화 목적으로 한 번만 호출되어야 하는 메서드에 사용
-  Spring에서도 이 어노테이션을 지원하여, 빈이 생성되고 나서 초기화 작업을 수행할 때 사용 가능
```java
    import javax.annotation.PostConstruct;
    import org.springframework.stereotype.Component;
    
    @Component
    public class MyBean {
        @PostConstruct
        public void init() {
            // 초기화 코드
            System.out.println("@PostConstruct로 초기화 메서드를 실행합니다.");
        }
    }
```


4. InitializingBean 인터페이스와 DisposableBean 인터페이스
- `InitializingBean`을 구현하면, 빈이 생성되고 의존성이 주입된 후 초기화를 위해 afterPropertiesSet 메서드를 자동으로 호출
- 반대로, `DisposableBean`은 빈이 소멸되기 직전에 destroy 메서드를 호출
```java
    import org.springframework.beans.factory.DisposableBean;
    import org.springframework.beans.factory.InitializingBean;
    import org.springframework.stereotype.Component;
    
    @Component
    public class MyBean implements InitializingBean, DisposableBean {
        @Override
        public void afterPropertiesSet() throws Exception {
            // 초기화 코드
            System.out.println("빈이 생성되고 의존성 주입이 완료된 후 실행됩니다.");
        }
    
        @Override
        public void destroy() throws Exception {
            // 정리 코드
            System.out.println("빈이 소멸되기 전에 실행됩니다.");
        }
    }
```


5. @Bean 초기화와 소멸 메서드 지정
- @Configuration 클래스 내에서 @Bean 어노테이션을 사용할 때, 빈의 초기화와 소멸 시점에 호출될 메서드를 지정 가능
-  XML 기반의 구성(init-method와 destroy-method 속성 사용)과 유사한 방법


6. @Profile 어노테이션을 이용한 조건부 실행
- @Profile 어노테이션을 이용하여 특정 프로파일이 활성화될 때만 빈이 생성되거나 특정 메서드가 실행되도록 구성이 가능
- 개발, 테스트, 운영 등 환경에 따라 다른 동작을 수행하고자 할 때 유용