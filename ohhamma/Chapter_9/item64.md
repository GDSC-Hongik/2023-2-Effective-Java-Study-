# 객체는 인터페이스를 사용해 참조하라

## 인터페이스를 타입으로 사용하는 습관을 길러두자

```
💡 적합한 인터페이스만 있다면 매개변수, 반환값, 변수, 필드를 전부 인터페이스 타입으로 선언하라.
```

```java
Set<Son> sonSet = new LinkedHashSet<>();
Set<Son> sonSet = new HashSet<>();
```

- 나중에 구현 클래스를 교체하는 경우 → 새 클래스의 생성자만 호출하면 됨

### 구현 타입 변경 동기

- 성능 개선
- 신기능 제공

### 주의할 점

- 기존 클래스가 특별한 기능을 제공하는 경우
- 새로운 클래스도 반드시 같은 기능을 제공해야 함
- ex) `LinkedHashSet` → `HashSet` (반복자의 순회 순서 보장 x)

## 적합한 인터페이스가 없다면 클래스로 참조하자

```
💡 클래스의 계층구조 중 필요한 기능을 만족하는 가장 상위의 클래스를 타입으로 사용하자.
```

### 값 클래스

- 여러 가지로 구현될 가능성 x → **final**
- ex) `String`, `BigInteger`

### 클래스 기반으로 작성된 프레임워크가 제공하는 객체

- 그래도 **기반 클래스**(추상 클래스)를 사용해 참조하자
- ex) `java.io` 패키지의 여러 클래스 (`OutputStream` 등)

### 인터페이스에 없는 특별한 메서드를 제공하는 클래스

- ex) `PriorityQueue` : comparator 메서드 제공
- 추가 메서드를 **꼭** 사용해야 하는 경우에만 클래스 타입을 직접 사용하자