## Spring DI / IoC는 어떻게 동작하나요

### Inversion of Control ( IoC )

- 제어의 역전
- *Don’t call us. We’ll call you. ( Hollywood Principle )*

- 프레임워크를 적용하지 않은, 개발자가 작성하는 코드의 특징
    - 객체의 생명주기 ( 객체의 생성, 초기화, 메서드 호출, 소멸 )을
      클라이언트 구현 객체가 직접 관리함.
    - 외부 라이브러리를 호출하더라도, 해당 코드의 호출 시점 역시 개발자가 직접 관리함.
- 프레임워크를 적용하는 경우 ( ex. Spring Framework 적용 )
    - Controller, Service 같은 객체들의 동작을 우리가 직접 구현
    - 해당 객체들이 어느 시점에 호출될지는 신경쓰지 않는다.
    - 프레임워크의 요구사항에 맞춰, 객체를 생성하면.
      프레임워크가 해당 객체들을 가져다가 생성하고,
      메서드를 호출하고, 소멸시킴.
    - 객체의 생명주기를 프레임워크가 관리.
      즉, 프로그램의 제어권이 개발자에게서 프레임워크로 역전된 것

### **< Library vs Framework > - IoC 관점**

- 라이브러리를 사용하는 어플리케이션의 경우,
  프로그래머는 라이브러리를 사용하여 객체를 생성하고, 사용하여 프로그램의 흐름을 제어한다.
  즉 프로그램의 제어권은 프로그래머에게 있다.
- 프레임워크를 사용하는 어플리케이션의 경우,
  어플리케이션 코드에 작성한 객체들을 프레임워크가 필요한 시점에 가져다가 프로그램을 구동한다.
  즉, 프로그램의 제어권은 프레임워크로 역전된다.

### Ioc의 예시

- **Spring, Django, Node.js**와 같은 웹 프레임워크
- **Java JUnit** 테스트 프레임워크
    - 개발자는 테스트 메서드를 작성하지만, 해당 메서드들에 대한 제어권은 Junit Framework에 있음.
    - **@Test , @BeforeEach, @AfterEach** 어노테이션이 붙은 메서드들도 호출시점을 Junit 프레임워크가 정하고, 관리한다. ( 테스트의 제어가 JUnit에게 역전됨 )
- **Java 템플릿 메서드 패턴( Template Method Pattern )**
    - Template Method Pattern
        - 상위 추상 클래스에서 알고리즘의 구조를 메서드에 정의하고, 하위 클래스에서 알고리즘의 ‘구조’의 변경 없이 알고리즘을 재정의하는 패턴
    - 하위 클래스에서 **메서드의 실제 구현**을 하지만,
      해당 메서드의 ***호출 제어권 ㅡ 추상 클래스에 정의된 다른 메서드들에서 해당 템플릿 메서드가 수행되는 순서 등 ㅡ 호출 순서*** 등은 상위의 추상 클래스에 있게 된다.

### IoC의 장점

- 프로그램의 진행 흐름과 구체적인 구현을 분리시킬 수 있다.
- 개발자는 핵심 비즈니스 로직에만 집중할 수 있다.
- 흐름에 구현체를 끼워맞추면 되니, 구현체 사이의 변경이 용이하다. ( OCP )
- 구현 객체 간 의존성이 낮아진다.

### Dependency Injection ( DI )

- 의존성 주입
- IoC 기법 중 하나
- 객체의 의존관계를 외부에서 주입시키는 디자인 패턴
- IoC와 DI는 다른 개념이다. DI는 IoC를 구현하기 위한 패턴 중 하나

### 마틴 파울러의 글 ( DI ≠ IoC )

```
As a result I think
we need a more specific name for this pattern. ( DI )
Inversion of Control is too generic a term,
and thus people find it confusing.
As a result with a lot of discussion with various IoC advocates
we settled on the name Dependency Injection.

그 결과 이 패턴에 대해 좀 더 구체적인 이름이 필요하다고 생각한다. 
Inversion of Control은 너무 일반적인 용어이기 때문에 
사람들은 그것을 혼동한다. 
그 결과 다양한 IoC 옹호자들과 많은 논의를 거쳐 
Dependency Injection이라는 이름을 정했다.
```

### 의존성 ( Dependency )

- 어떤 클래스 A가 클래스 B에 대해 알고 있으면 = 사용하면,
  A는 B에 의존한다고 한다.

```java
// A가 내부에서 B를 생성한다.
// A가 B의 구체적 기능을 사용한다. ( 메서드 이름도 알아야한다 )
// A와 B는 강한 결합을 가진다.
public class A {
		private B b = new B();
}
```

- 다른 말로, B의 내부 구현이 바뀌면, 그것이 A의 구현에 영향을 미친다.
- 프로그램을 이루는 객체들 간의 의존성이 많아지면,
  한 클래스의 구현을 바꿨을 때, 변경의 전파범위가 매우 커지고,
  이 변경의 전파는 또다른 변경의 전파를 만들어내는..
  작은 거 하나 고치기 어려운 프로그램,
  즉 유지보수가 쉽지 않은 프로그램이 된다.

```java
// A의 외부에서 B라는 의존 객체를 주입해준다.
// B가 구체 클래스라면, 여전히 A는 B에 의존한다.
// 즉, B가 변경되면, A도 변경된다.
// 만약, B를 인터페이스로 추상화하면,
// B 인터페이스의 규약을 지키는 다양한 구현체들이 들어올 수 있다.
// A는 B 객체의 구체적 구현까진 몰라도 되고, 제공하는 기능만 알면 된다.
// B 객체가 바뀌어도, A 객체는 영향을 받지 않는다.
// A와 B가 느슨하게 결합한다. ( A가 내부적으로 B를 생성한다면 )
// Spring Framework를 통해, B 구현체가 들어옴으로써,
// 의존성을 주입받고, 의존성을 다각화할 수 있다. 
public class A {
		private B b;

		// DI 방법 중, 생성자 주입 방법.
		public A(B b){
				this.b = b;
		}
}
```

### 의존성 주입 In 토비의 스프링

- 클래스 모델이나 코드에는 런타임 시점의 의존관계가 드러나지 않는다. 그러기 위해서는, 객체들이 서로의 인터페이스에만 의존하고 있어야 한다.
- 런타임 시점의 의존관계는
  **컨테이너**나 **팩토리** 같은 제 3의 존재가 결정한다.
- 의존관계는 사용할 오브젝트에 대한 래퍼런스를 외부에서 제공(주입) 해줌으로써 만들어진다.

### DI 방법 3가지

- 생성자 주입 ( Constructor Injection )
    - Spring에서 권장하는 방식

- Setter 주입 ( Setter Injection )
    - 런타임에 의존관계가 바뀔 수 있으므로,
      신뢰성 있는 프로그램이 아니게 된다.
    - 권장되지 않음.

```java
public class A {
    private B b;
    
    public void setB(B b) {
        this.b = b;
    }
}
```

- 인터페이스 주입 ( Interface Injection )
    - 어떤 의존성을 주입할 지 인터페이스에 명시하고,
      의존성을 주입받는 클래스는 해당 인터페이스의 구현체로 만든다.
    - Setter 주입과 비슷함.

```java
public interface BInjection {
    void inject(B b);
}

public A implements BInjection {
    private B b;
    
    @Override
    public void inject(B b) {
        this.b = b;
    }
}
```

### DI의 장점

- 코드가 더 깔끔해지고, ( 가독성 )
  객체간 의존성이 줄어든다. ( = 변경에 덜 취약해진다 )
- 재사용성이 높아진다.
- 모듈 간의 결합도가 낮아진다.
- 클래스를 테스트하기 더 쉬워지고,
  단위 테스트에서 Stub, Mock을 사용할 수 있다.


---
### DI

- Spring이 다른 프레임워크와 차별화되어 제공하는 의존관계 주입 기능
- 객체를 직접 생성하는게 아니라, 외부 ( 스프링 )에서 생성하고 주입 시켜주는 방식
  ( = 객체 스스로가 의존하는 객체를 만드는 것이 아니라,
  제어권을 스프링에게 위임하여 스프링이 만들어놓은 객체를 주입한다 )
- Spring이 모든 의존성 객체를 Spring이 실행될 때 다 만들어주고, 필요한 곳에 주입시켜준다.
- Bean들은 싱글턴 패턴의 특징을 가진다.

**< A객체가 의존성을 직접 관리 VS A객체 외부에서 의존성 주입 >**
![DI.png](img%2FDI.png)

- Spring Container ( = IoC Container )에서
  프로그래머가 작성한 클래스 코드를 통해, Spring Bean을 생성하여
  객체끼리 연관짓고(의존관계 설정), 객체의 생명주기(생성, 메서드 사용, 삭제)를 관리한다.

- **IoC Container**에서, Dependency Injection 방법으로 각 객체들끼리 연관을 지어
  전체 Application을 동작하도록 만든다.
  ( IoC Container = DI Container = Bean Factory = ApplicationContext )
  ( Spring Container 는 단순한 DI 작업보다 더 많은 일을 하는데,
  DI 를 위한 Bean Factory에 여러가지 기능을 추가한 것을 ApplicationContext라고 한다. )

- metadate(.xml 파일)과 POJO(Plain Old Java Object)를 사용하여 완전한 소프트웨어를 만들어냄.

- 개발자는 Metadata와 POJO를 적절히 사용하면 쉽게 전체 프로그램 개발 가능

![IoC_ApplicationContext.png](img%2FIoC_ApplicationContext.png)

### IoC Container 세부사항

### BeanFactory vs ApplicationContext

![BeanFactory_ApplicationContext_Hierarchy.png](img%2FBeanFactory_ApplicationContext_Hierarchy.png)

**→ BeanFactory**

- Spring Container ( IoC Container )의 최상위 인터페이스
- Spring Bean을 관리하고 조회하는 역할을 담당한다.
- 대표적으로 getBean() 메소드를 제공함.

**→ ApplicationContext**

```java
public interface ApplicationContext extends EnvironmentCapable, ListableBeanFactory, 
                                            HierarchicalBeanFactory, MessageSource, ApplicationEventPublisher, 
                                            ResourcePatternResolver {
```

- ApplicationContext는 Bean Factory 기능을 모두 상속 받아서 제공한다.
- 위의 ***I/F***에서 extends 한 ***I/F***들은 Bean Factory에 없는 추가 기능을 가지고 있다.
  따라서, ApplicationContext는 이를 혼합하여 다음과 같은 기능을 제공함.
  - 메시지 소스를 활용한 국제화 기능
    - 한국에서 Request가 들어오면 한국어로, 영어권에서 들어오면 영어로 출력
  - 환경 변수
    - 로컬, 개발, 운영 등을 구분해서 처리한다.
  - 어플리케이션 이벤트
    - 이벤트를 발행하고 구독하는 모델을 편리하게 지원한다.
  - 편리한 리소스 조회
    - 파일, 클래스 패스, 외부 등에서 리소스를 편리하게 조회한다.

### 설정 메타 정보

- IoC Container의 가장 기초적인 역할은, **오브젝트를 생성하고 이를 관리하는 것**.
- Spring Container가 관리하는 이런 오브젝트를 Spring Bean이라고 한다.
- 설정 메타정보 (.xml, Annotation..등 )는 바로 이 Bean을 어떻게 만들고, 어떻게 동작하게 할 것인가에 관한 정보임.
- **Spring Container**는 J**ava Code ( = Annotation ), XML, Groovy** 등 다양한 형식의 설정 정보를 받아들일 수 있도록 유연하게 설계되어 있음.

![ApplicationContext_Implementations_AnnotationBased_XMLBased.png](img%2FApplicationContext_Implementations_AnnotationBased_XMLBased.png)

### Spring Bean 설정 : Annotation 기반 Java Code vs XML 기반

< Annotation 기반의 Spring Bean 설정 >

```java
@Configuration
public class AppConfig {

        @Bean
        public MemberService memberService() {
                return new MemberServiceImpl(memberRepository());
        }
}
```

- **@Configuration : 1개 이상의 Bean을 제공하는 클래스의 경우 반드시 명시해야 함.**
- **@Bean : 클래스를 Bean으로 등록할 때 사용함.**

< XML 기반의 Spring Bean 설정 >

```xml
<beans xmlns="http://www.springframework.org/schema/beans"xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"xsi:schemaLocation="http://www.springframework.org/schema/beans http://
www.springframework.org/schema/beans/spring-beans.xsd">

     <bean id="memberService" class="hello.core.member.MemberServiceImpl">
             <constructor-arg name="memberRepository" ref="memberRepository"/>
     </bean>
</beans>
```

- XML 기반의 설정 파일을 보면, Java 코드로 된 설정 파일과 거의 비슷함.
- XML 기반으로 설정하는 것은 최근에 잘 사용하지 않음.

### Spring Bean 설정 메타 정보 - BeanDefinition

- Spring은 어떻게 XML 기반, Annotation 기반 Bean 설정 등, 다양한 형식을 지원하는 것인가?
  - 그 핵심에는 **BeanDefinition** 이라는 추상화가 있음.
- Spring은, XML을 읽어서 BeanDefinition을 만들고
  Java Code를 읽어서 BeanDefinition을 만든다.
- 즉, Spring Container 는 XML / Annotaion .. 등의 설정인지 여부에 의존하지 않고,
  오직 그들의 추상화인 BeanDefinition에만 의존한다. ( 오직 BeanDefinition 만 알면 된다 ) ( DIP )
- BeanDefinition ⇒ Bean 설정 메타 정보,
  @Bean : Annotaion , <bean> : XML 당 하나의 메타 정보가 생성된다.

![BeanDefinition.png](img%2FBeanDefinition.png)

- AnnotationConfigApplicationContext는 AnnotationBeanDefinitionReader를 사용해서
  AppConfig.class 를 읽고 BeanDefinition을 생성함.
- GenericXmlApplicationContext는 XmlBeanDefinitionReader를 사용해서 appConfig.xml 설정 정보를 읽고 BeanDefinition을 생성함.
- 새로운 형식의 설정 정보가 추가되면, XxxBeanDefinitionReader 를 만들어서, BeanDefinition을 생성하면 됨.

이렇게 생성된 Bean을, Spring 실행 시 다 생성하여 Spring Container에 넣어뒀다가
JVM Class Loader에 의한, 클래스 로드시 생성되는 객체에 의존관계를 주입해준다.
***( IoC Container에서 관리하는 Bean을 DI 해준다. )***

### DI Implementation

### 1) Field 주입

```java
@Service
public class BurgerService {

    @Autowired
    private BurgerRecipe burgerRecipe;
}
```

- 변수 선언부에 @Autowired Annotation을 붙인다.
- 사용하기 편하지만,
  - 단일 책임 원칙 위반 가능성이 커짐. ( 변수 위에 @Autowired 만 달아주면 되어, 의존성 주입이 쉬워져서 많은 필드에 대해 의존성 주입을 남용 → 한 클래스가 많은 클래스에 의존. 어떤 클래스의 변경 시, 그 전파범위가 작지 않아짐. )
  - 의존성이 숨는다 = 생성자 주입에 비해 의존 관계를 파악하기 어렵다.
- DI Container와의 결합도가 커진다.
- 순환 참조가 발생할 수 있다. ( = Bean들 서로 간 의존, A Bean이 B Bean의 메서드 호출, 해당 메서드에서 A Bean의 메서드 호출… 반복.. 스택오버플로우 터짐 )

### 2) Setter 주입

```java
@Service
public class BurgerService {

    private BurgerRecipe burgerRecipe;

        @Autowired
    public void setBurgerRecipe(BurgerRecipe burgerRecipe) {
        this.burgerRecipe = burgerRecipe;
    }
}
```

- Setter 역할의 메서드에 @Autowired Annotation을 붙인다.
  - Bean들 간 선택적인 의존성을 사용할 수 있다는 장점 But
    - 런타임 도중 의존관계가 바뀔 수 있음. 추적이 어렵다, 버그 발생 가능
    - 의존관계가 주입된느 대상의 클래스 ( 위에서 BurgerService ) 에 모든 의존성을 주입하지 않아도 해당 객체를 생성할 수 있고, 주입받지 못한 Bean의 메서드를 호출하는 경우 NPE가 발생할 수 있다.
    - 순환 참조 문제 발생 가능

### 3) 생성자 주입

```java
@Service
public class BurgerService {

    private BurgerRecipe burgerRecipe;

    @Autowired
    public BurgerRecipe(BurgerRecipe burgerRecipe) {
        this.burgerRecipe = burgerRecipe;
    }
}
```

- 생성자에 @Autowired 어노테이션을 붙여서 의존성을 주입받는다. ( 가장 권장됨 )
- 즉, 객체의 생성 시 의존성을 주입받는다.
  - 장점)
    - 의존관계를 모두 주입해야만 객체 생성이 가능하므로, NPE 방지 가능
    - 불변성 보장 가능 ( = 한번 생성된 이후 바뀔 일이 없다 )
    - **순환 참조를 컴파일 단계에서 찾아낼 수 있다.**
    - 의존성을 주입하기 번거롭고, 생성자 인자가 많아지면 코드가 길어져 위기감 느낄 수 있음.
      - 이를 바탕으로 SRP 원칙을 생각하게 되고, 객체 간 의존성을 낮추려는 리팩터링 촉진 가능.

### 순환 참조

- DI 방식 중 필드 주입, 수정자 주입은
  **객체 ( Spring Bean ) 생성 이후에** 비즈니스 로직 상에서 순환 참조가 일어나기에 ( = 런타임 ),
  컴파일 단계에서 순환 참조를 잡아낼 수 없음 ( = 컴파일러가 판단 불가능 )

- 생성자 주입일 때, 순환참조 발생 가능성이 있으면 아래와 같이 로그가 찍히며 실행 실패 ( = 컴파일러가 잡아준다 )

```java
***************************
APPLICATION FAILED TO START
***************************

Description:

The dependencies of some of the beans in the application context form a cycle:

┌─────┐
|  courseServiceImpl defined in file [/.../CourseServiceImpl.class]
↑     ↓
|  studentServiceImpl defined in file [/.../StudentServiceImpl.class]
```

- 생성자 주입은 Spring Container가 Bean을 생성하는 시점에 순환 참조를 확인하기에,
  컴파일 단계에서 순환 참조를 잡아낼 수 있다!

