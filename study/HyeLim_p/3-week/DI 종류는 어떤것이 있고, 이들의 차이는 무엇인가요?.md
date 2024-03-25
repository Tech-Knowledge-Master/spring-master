# DI 종류는 어떤것이 있고, 이들의 차이는 무엇인가요?

### 생성자 주입 Vs 수정자 주입, 필드주입
* 생성자 주입은 빈 객체를 생성하는 시점에 생성자의 파라미터 자리의 빈 객체를 찾아서 먼저 주입한 뒤에 주입받은 빈 객체를 이용하게 된다.
    - 런타임 시점이 아닌 애플리케이션 구동 시점에 순환 참조 오류 발견 가능
* 수정주입, 필드주입은 빈을 먼저 생성한 후에 어노테이션이 붙은 필드에 해당하는 빈으르 찾아서 주입하는 방식
    - 빈을 먼저 생성한 후에 필드에 주입하기 때문에 빈 객체 생성한 시점에는 순환 참조 발생 여부 확인 불가능
## 생성자 주입
컴파일 시점에 객체를 주입받는다.
생성자의 호출 시점에 1회 호출되는 것이 보장된다. -> 주입받은 객체가 변하지 않거나, 반드시 객체 주입이 필요한 경우에 강제하기 위해 사용된다.

## 수정자 주입
필드 값을 변경하는 Setter 를 통해 의존관계를 주입하는 법
* 객체 생성 이후에 호출되므로 final 사용 할 수 없다.
* 주입이 필요한 객체르 ㄹ주입하지 않더라도 객체가 생성되어 NullPointerException의 발생 가능성이 있다.
* 객체 생성 후에도 의존성을 주입할 수 있으며 의존관계 변경 및 선택이 필요한 경우에 사용이 가능하지만, 의존관계가 변경되지 않도록 설계하는 것이 좋다
```java
//library 의 book 필드에 setter 로 주입되지 않은 경우 NullPointerException 발생
Library library = new Library();
library.setBook(new ScienceBook());
library.readBook();
```

## 필드 주입
* 객체 생성 이후에 호출되므로 final 사용 할 수 없다.
* 외부에서 변경이 불가능해 테스트 코드 작성이 어렵다.
* DI 를 지원하는 프레임워크가 필요하다
* @Autowired 를 남용하면 필드가 많아져 단일 책임 원칙에 위배 될 수 있다.
* @Autowired 를 사용하면 서비스 코드에 스프링 의존성이 침투된다.
```java
import org.springframework.beans.factory.annotation.Autowired;
// 스프링 의존성이 UserService에 import되어 코드로 박혀버림

@Service
public class UserService {

    @Autowired
    private UserRepository userRepository;
    @Autowired
    private MemberService memberService;

}
```

## 생성자 주입
* final 사용이 가능하다.
* 생성자 호출 시점에 단 한번만 호출되어 불변성을 지닌다.
* 주입이 필요한 객체를 주입해주지 않는다면, 컴파일 오류로 객체 생성이 불가능하다.
* 애플리케이션 구동 시점(객체 생성 시점) 과 의존관계 주입 즉, 객체 의 생성과 조립이 동시에 시행되어 순환참조에러를 잡을 수 있다.
  (다른 주입 방식의 경우 생성과 조립이 분리되어있기 때문에 런타임때, 호출이 되고 나서야 순환 이슈를 파악이 가능하다.)
