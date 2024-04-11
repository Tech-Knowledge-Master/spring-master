## Filter는 Servlet의 스펙이고, Interceptor는 Spring MVC의 스펙입니다. Spring Application에서 Filter와 Interceptor를 통해 예외를 처리할 경우 어떻게 해야 할까요?

---

### Filter와 Interceptor의 차이?
필터와 인터셉터는 관리되는 영역이 다르다.
필터는 스프링 이전의 서블릿 영역에서 관리되지만, 인터셉터는 스프링 영역에서 관리되는 영역이기 때문에 필터는 스프링이 처리해주는 내용을 적용 받을 수 없다. 
이로 인한 차이로 발생하는 대표적인 예시가 스프링에 의한 예외처리가 되지 않는다는 것!

1. Filter의 예외처리   
   Filter는 서블릿 컨테이너 수준에서 동작한다. 이는 Spring 컨텍스트 외부에서 작동한다는 의미로, Spring의 DispatcherServlet이 처리하기 전의 요청과 처리한 후의 응답에 개입할 수 있다.
   Filter에서 발생하는 예외는 Spring의 예외 해석 메커니즘과는 별도로 처리되어야 한다. 예외를 catch하고 로그를 남긴 뒤, 적절한 에러 응답을 직접 생성하고 클라이언트에 반환해야 한다.
   따라서 Spring 애플리케이션의 컨텍스트 밖에서 처리되어야 하는 예외에 적합하다.

2. Interceptor의 예외처리   
   Interceptor는 Spring MVC의 컨트롤러를 처리하는 과정에서 동작한다. 이는 Spring 컨텍스트 내부에서 작동한다는 의미로, 
   Spring의 @Controller 또는 @RestController가 처리하는 요청에 대해 동작한다.
   Interceptor 내부에서 발생한 예외는 Spring의 @ControllerAdvice나 @ExceptionHandler 등을 통해 처리될 수 있다.
   Interceptor에서 예외를 던지면 Spring MVC가 이를 잡아 적절한 예외 처리기로 전달할 수 있다.

```text
    Filter는 Spring `컨텍스트 외부`에서 작동하며, 예외 처리를 직접 관리해야 한다.
    Interceptor는 Spring `컨텍스트 내부`에서 작동하며, Spring의 예외 처리 메커니즘과 통합될 수 있다.
```


[MangKyu's Diary:티스토리](https://mangkyu.tistory.com/173)   
[참고 링크](https://velog.io/@dabeen-jung/cs-Spring-%EC%84%9C%EB%B8%94%EB%A6%BF-Filter%EC%99%80-Spring-Interceptor-%EC%B0%A8%EC%9D%B4-%EC%98%88%EC%99%B8%EC%B2%98%EB%A6%AC)