# Spring에서의 DI, IOC
## DI(Dependency Injection)
Spring에서 DI는 외부(IOC 컨테이너)에서 setter나 생성자를 통해 주입시키는 방식을 사용하고 있다.

Spring은 이런 DI를 극대화하여 객체들을 모두 생성하여 IOC 컨테이너에 싱글톤 패턴을 사용해서 생성해놓는다.
그 후 각 객체가 필요한 의존 객체들을 이 컨테이너에서 뽑아서 주입시키는 방식을 사용하고 있다.

이렇게 구현할 수 있다면 개발자는 따로 결합성을 크게 신경쓰지 않고 코드를 개발할 수 있다.

DI를 Spring에서 구현하는 방식은 크게 3가지가 존재한다.
1. 생성자 주입(Constructor Injection)

   일반적으로 필드 변수를 final로 지정한 후, 생성자를 통해 인스턴스를 생성하는 방식이다.
2. 필드 주입(Field Injection)

   @Autowired라는 어노테이션을 필드 변수에 넣어서 프레임워크가 알아서 주입하도록 하는 방식이다.
   이런 방식은 프레임워크에 너무 의존적인 방식이다.
3. 수정자 주입(Setter Injection)

   Setter를 통해 주입하는 방식이나 모든 곳에서 변경이 가능하여 추천하지 않는다.

여기서 Spring은 생성자 주입을 권장하며, 이유는 불변성, 테스트에 용이하기 때문이다.

## IoC(Inversion of Control)
Spring에서 IoC란 제어의 역전을 말하는 것으로 객체의 생성, 사용, 생명주기 관리 모든 것이 개발자가 아닌 프레임워크에 맡기는 형태를 말한다.

따라서 컨테이너가 이 모든 것을 관리하면서 개발자는 좀 더 비지니스 로직에 집중하여 개발할 수 있게 되었다.
이러한 IoC는 DL(Dependency Lookup)과 DI(Dependency Injection)로 구성되어 있다.

DL은 의존을 주입 받아야 할 객체가 직접 의존 관계를 찾는 방식을 말한다.

이 모든 것을 Spring 컨테이너가 책임지며 크게 Bean Factory, ApplicationContext가 존재한다.

ex, junit 테스트 코드도 이런 ioc를 가지며, template 디자인 패턴도 IoC를 따라가는 것이다.

### Bean Factory
단순히 객체를 생성하고, 주입하는 기능만 제공하는 컨테이너이다.

### Application Context
위의 Bean Factory에서 더 많은 Spring 기능을 추가한 컨테이너이며, 실무에서는 이 컨테이너를 주로 사용한다.


### 참고 자료
- https://velog.io/@gillog/Spring-DIDependency-Injection
- https://dev-coco.tistory.com/80
- https://velog.io/@tank3a/%EC%8A%A4%ED%94%84%EB%A7%81-%EC%BB%A8%ED%85%8C%EC%9D%B4%EB%84%88%EC%99%80-%EC%8A%A4%ED%94%84%EB%A7%81-%EB%B9%88
- https://dev-coco.tistory.com/70
- https://dev-coco.tistory.com/69
- https://velog.io/@dusdn2424/%EC%8A%A4%ED%94%84%EB%A7%81-Spring-IoC-DI-DL-%EA%B0%9C%EB%85%90-%EC%A0%95%EB%A6%AC