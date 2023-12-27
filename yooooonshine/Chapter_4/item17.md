# 변경 가능성을 최소화하라
---
## 불변 클래스란?
그 인스턴스의 내부 값을 변경할 수 없는 클래스를 의미한다.

`String`, `BigInteger`, `BigDecimal`이 여기에 속한다.

불변 클래스는 가변 클래스보다 설계, 구현이,사용이 쉽고, 오류가 생길 여지도 적다.
## 그럼 불변 클래스로 만들려면 어떻게 해야할까
* 클래스를 확장할 수 없도록한다., 대표적으로 클래스를 final로 설정하면 된다.
* 객체의 상태를 변경하는 메소드를 제공하지 않는다.
* 모든 필드를 final로 설정한다.
* 모든 필드를 priavate로 설정한다.
* 자신 외에는 내부의 가변 컴포넌트에 접근할 수 없도록 한다. 즉 방어적 복사를 사용하여, 내부의 가변 컴포넌트에 접근할 수 없도록 한다.

## 함수적 프로그래밍 vs 절차적 프로그래밍
함수적 프로그래밍이란, 피연산자에 함수를 적용하여 리턴하지만, 피연산자는 적용후에도 변하지 않는 것

절차적 프로그래밍이란 피연산자가 함수를 적용하면 자신의 상태가 변하는 것.
이 때 메서드 이름은 동사보다 전치사를 사용한다.
# 불변 객체의 장점
## 불변 객체는 스레드 안전하여 따로 동기화할 필요가 없다.
객체를 불변 객체로 만들면, 상태변화가 업으므로, 스레드가 동시에 사용해도 문제가 되지 않는다.
## 불변 객체는 자유롭게 공유할 수 있음은 물론, 불변 객체끼리는 내부 데이터를 공유할 수 있다.
## 객체를 만들 때 다른 불변 객체들을 구성요소로 사용하면 이점이 많다.
불변객체로 구성요소들이 이루어 진다면, 아무리 복잡하더라도 불변식을 유지하기 휠씬 수월하다.
## 불변 객체는 그 자체로 실패 원자성을 제공한다.
상태가 안변하니 불일치 상태에 빠질 가능성 자체가 없다.
# 불변 클래스의 단점
## 값이 다르다면 반드시 독립된 객체로 만들어야 한다.
값이 조금이라도 다르면 모두 독립적으로 만들어야 하므로, 비용이 많이 든다.


## 불변 클래스를 만들기 위해, 상속을 막는 다른 방법
그건 바로 모든 생성자를 private 혹은 package-private로 두고,
public 정적 팩터리를 제공하는 방법이다.