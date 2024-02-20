## Spring Bean이란 무엇인가요

### Java Bean

- 스프링에서 객체를 지칭할 때 사용하는 용어
- 다음의 코딩 관례를 지켜 작성된 자바 클래스
    - 매개변수가 없는 public 생성자가 있음. ( NoArgsConstructor )
    - public getter / setter 메소드 존재
    - java.io.Serializable을 구현한다.
- Java Bean ≠ Spring Bean

### Bean 이름 유래

- Java가 커피 이름이라 그런지, 자바 프로그램의 구성요소, 즉 자바 객체들을 커피콩(Bean)이라 했다는 이야기가 있다.
- 여담으로, Bean 들을 항아리에 담겠다고 해서, 최종 빌드된 패키징 파일은 .jar 파일로 명명함.
- 자바의 .class 파일을 hex 문자열로 보면, 파일내용의 맨 앞에 CAFEBABE ( 카페 베이베 )라고 되어있다 한다..

### Spring Bean

- 스프링이 관리하는 오브젝트
- Spring Framework Container ( IoC Container ) 에 의해 인스턴스화되고, 구성되고, 관리되는 객체
- Spring Config File, 어노테이션에 의해 정의되고,
  스프링에 의해 인스턴스화된 다음 응용 프로그램에 주입된다. ( DI )
- 초기 버전에서는 스프링이 자바빈과 함께 사용하기 위한 것이어서, 이름이 Bean이었다.
- Spring은 기본 생성자와 Getter, Setter와 같은 Java Bean의 필수 특성이 없어도 거의 모든 객체를 관리할 수 있다.
- Spring Bean은 Java Bean이 될 수도 있지만, 꼭 지켜지지 않아도 프로그램 개발이 가능