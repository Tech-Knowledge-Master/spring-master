## Spring Web MVC에서 요청 마다 Thread가 생성되어 Controller를 통해 요청을 수행할텐데, 어떻게 1개의 Controller만 생성될 수 있을까요?

--- 

Controller 객체는 힙(heap) 영역에 생성되지만, 생성된 객체의 정보는 메서드(Method) 영역에 올라가기 때문이다.
메서드 영역은 모든 스레드에 의해 공유되기 때문에, 이 영역에 저장된 클래스 정보나 메서드는 모든 스레드가 접근 가능하다.
즉, Controller 객체가 힙에 생성되더라도 그 클래스의 메소드와 정보는 모든 스레드에 의해 공유될 수 있는 메서드 영역에 저장되므로
실제로는 이러한 메서드들을 가지는 Controller 객체가 하나만 필요하다는 것을 의미한다.
여러 스레드가 동일한 메서드와 정보를 공유할 수 있기 때문에, Controller 객체는 다수 생성할 필요가 없는 것이다.


### Thread는 여럿, Controller는 하나
스프링 웹 애플리케이션에서는 클라이언트로부터 오는 각각의 요청(request)을 별도의 스레드가 처리한다.
하나의 컨트롤러가 어떻게 여러 개의 스레드의 요청을 처리하는 것일까?

- Thread는 singleton으로 생성된 Controller를 포함한 Bean들을 참고하여 일을 한다. Bean들은 기본적으로 Singleton으로 생성되고 관리된다.
- 사실상 이 Thread들은 그 1개의 Singleton Controller 객체를 공유하는 것이다.
- 즉, 하나의 싱글톤 컨트롤러가 동시에 여러 요청을 처리하는 것이 아니라, 각각의 Thread가 singleton으로 생성된 Controller 인스턴스를 참조하여 각자의 요청을 처리하는 것이다.