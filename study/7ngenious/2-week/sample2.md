# Spring Bean의 Scope에 대해 설명

Spring Framework에서 Bean의 Scope는 해당 Bean 인스턴스의 생명주기와 관련이 있습니다. Scope는 Bean이 생성되고 유지되는 시간과 범위를 결정합니다.

1. Singleton: 기본 Scope로, 하나의 Bean 인스턴스를 애플리케이션 전체에서 공유합니다. 여러 요청에서 동일한 인스턴스를 사용하고 싶을 때 유용합니다.

2. Prototype: 매번 요청할 때마다 새로운 Bean 인스턴스를 생성합니다. 각 요청마다 독립적인 인스턴스를 사용하고 싶을 때 유용합니다.

3. Request: 각각의 HTTP 요청마다 새로운 Bean 인스턴스를 생성합니다. 웹 애플리케이션에서 사용됩니다.

4. Session: 각각의 HTTP 세션마다 새로운 Bean 인스턴스를 생성합니다. 웹 애플리케이션에서 사용됩니다.

5. Global Session: 전역 HTTP 세션마다 새로운 Bean 인스턴스를 생성합니다. 포털 애플리케이션에서 사용됩니다.

6. Custom: 사용자 정의 Scope를 정의할 수 있습니다.

각 Scope는 다른 용도와 특징을 가지고 있으며, 애플리케이션의 요구에 맞게 적절한 Scope를 선택해야 합니다.
