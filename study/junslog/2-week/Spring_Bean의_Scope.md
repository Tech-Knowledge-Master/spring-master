### Spring Bean Scope

- Sping Bean이 앱이 구동되는 동안 존재할 수 있는 범위
- Bean의 Scope를 설정함으로써 Bean 객체의 생명 주기를 제어할 수 있음.

### Spring에서 제공하는 스코프 5종류

1) Singleton

- (Default) 스프링 IoC 컨테이너당 하나의 인스턴스만 사용 ( = 앱 구동 시 모든 인스턴스들을 각각 하나씩만 사용 )

2) Prototype

- 매번 새로운 빈을 정의해서 사용

3) Request

- HTTP Life Cycle 마다 한 개의 빈을 사용
- Web-Aware 컨텍스트에서만 사용 가능 - ex. ApplicationContext만 유효함.

4) Session

- HTTP Session마다 하나의 Bean을 사용
- Web-Aware 컨텍스트에서만 사용 가능

5) Application

- ServletContext 라이프 사이클 동안 한 개의 빈만 사용
- Web-Aware 컨텍스트에서만 사용 가능

6) WebSocket

- WebSocket 라이프사이클 안에서 한개의 빈만 사용, Web-Aware 컨텍스트에서만 사용 가능

⇒ request, session, application 세 개를 묶어서 Web Scope 라고도 함.

### 스코프 설정 방법

- @Scope 어노테이션 사용
- XML 설정 파일에서 요소의 Scope 속성을 사용하는 방법

[https://0soo.tistory.com/225#:~:text=Spring Bean 스코프란%2C 스프링,제거하는 것을 담당합니다](https://0soo.tistory.com/225#:~:text=Spring%20Bean%20%EC%8A%A4%EC%BD%94%ED%94%84%EB%9E%80%2C%20%EC%8A%A4%ED%94%84%EB%A7%81,%EC%A0%9C%EA%B1%B0%ED%95%98%EB%8A%94%20%EA%B2%83%EC%9D%84%20%EB%8B%B4%EB%8B%B9%ED%95%A9%EB%8B%88%EB%8B%A4).