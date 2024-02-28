# Spring Bean Life Cycle
## Bean Create
스프링에서 빈은 @Bean, @Component, @Configure 라는 어노테이션이 달려있는 클래스를 패키지 위에서부터 아래로 스캔하면서 만들기 시작한다.

하지만 생성자로 인해 순서에서 뒷순위인 인스턴스가 필요한 경우, 그 인스턴스를 먼저 찾아가서 생성하게 된다.

따라서 Spring에서 DI는 생성자 주입을 권고하는 편이다.

### 스프링 부트에서 컴포넌트 스캔방식 + 생성자 주입 방식인 경우

- Bean 생성자 호출 순서 : controller -> service -> repository (패키지 알파벳 순)

- Bean 생성완료 순서: repository -> service -> controller

## Bean LifeCycle
![BeanLifeCycle.png](image%2FBeanLifeCycle.png)
1. 스프링 컨테이너 생성
2. 스프링 빈 생성
3. 의존관계 주입
4. 초기화 콜백 : 빈이 생성되고, 빈의 의존관계 주입이 완료된 후
5. 사용
6. 소멸전 콜백 : 빈이 소멸되기 직전에 호출
7. 스프링 종료

### 참고 자료
- https://jh-labs.tistory.com/108
- https://velog.io/@zihs0822/Spring-Bean-%EC%83%9D%EC%84%B1-%EB%B0%A9%EC%8B%9D%EB%B3%84-%EB%8F%99%EC%9E%91
- 