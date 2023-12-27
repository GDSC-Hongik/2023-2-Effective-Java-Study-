# 상속을 고려해 설계하고 문서화하라. 그러지 않았다면 상속을 금지하라
---
## 상속을 고려한 설계와 문서화란?
상속을 고려한다면, 상속용 클래스는 재정의할 수 있는 메서드들을 내부적으로 어떻게 사용하는 지 문서로 남겨야 한다.

예를 들어, API 클래스 내부의 특정 메서드가, 내부의 다른 메서드를 호출하는 데, 만약 호출하는 메서드가 재정의 가능 메서드라면, 호출되는 메서드에 이에 대한 사실을 API 설명에 적시해야 한다.

더 넓게 말하면 재정의 가능 메서드를 호출할 수 있는 모든 상황을 문서로 남겨야 한다.

또한 클래스의 내부 동작 과정 중간에 끼어들 수 있는 hook을 잘 선별하여 protected 메서드 형태로 공개해야 할 수도 있다.
## 상속용 클래스의 생성자는 직접적으로든 간접적으로든 재정의 가능 메서드를 호출해서는 안 된다.
상위 클래스의 생성자가 호출된 다음, 하위 클래스의 생성자가 호출되고, 상위 클래스의 생성자에서 재정의 가능 메서드를 호출한다면,  하위 클래스에서 재정의한 메서드가 하위 클래스의 생성자보다 먼저 호출된다.
만약 재정의된 메서드에서 하위 클래스의 값을 사용한다면, 이는 아직 객체가 만들어지지 않았으므로 에러가 날 것이다.
## `Cloneable`이나 `Serializable`인터페이스를 구현하는 클래스는 상속할 수 있게 설계하지 말자
우선적으로 클래스를 확장하려는 프로그래머에게 큰 부담이 된다.
또한 이들은 생성자를 호출하는 것과 매우 유사하므로,
마찬가지로 상속용 클래스의 생성자는 재정의 가능 메서드를 호출하면 안된다.