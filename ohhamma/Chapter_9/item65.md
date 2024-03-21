# 리플렉션보다는 인터페이스를 사용하라

## 리플렉션 기능

```
💡 리플렉션은 복잡한 특수 시스템을 개발할 때 필요한 강력한 기능이지만, 단점도 많다.
```

- `java.lang.reflect` : 임의의 클래스에 접근 가능

### 이점

- `Class` 객체 → `Constructor`, `Method`, `Field` 인스턴스 가져올 수 있음
    - 인스턴스 이용 → 각각에 연결된 실제 생성자, 메서드 필드 조작 가능
- 컴파일 당시에 존재하지 않던 클래스 이용 가능

### 단점

- 컴파일타임 타입 검사가 주는 이점을 누릴 수 없음
- 코드 가독성 ↓
- 성능 ↓ : 일반 메서드 호출보다 훨씬 느림

### 언제 써야 하는가?

```
💡 리플렉션은 아주 제한된 형태로만 사용해야 단점을 피하고 이점만 취할 수 있다.
```

- 리플렉션은 **인스턴스 생성**에만 쓰자
- 위에서 만든 인스턴스는 인터페이스나 상위 클래스로 참조해 사용하자
- 런타임에 존재하지 않을 수도 있는 다른 클래스, 메서드, 필드와의 **의존성을 관리**하는 경우
    - 외부 패키지 다룰 때 유용