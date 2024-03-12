# clone 재정의는 주의해서 진행하라

- `Cloneable`을 구현하는 것만으로는 외부 객체에서 `clone` 메서드를 호출할 수 없음
    - Object에 선언됨
    - protected

```
💡 실무에서 Cloneable을 구현한 클래스는 clone 메서드를 public으로 제공하며, 사용자는 당연히 복제가 제대로 이뤄지리라 기대한다.
```

## 제대로 동작하는 clone 메서드를 구현해보자

### 모든 필드가 기본 타입이거나 불변 객체를 참조하는 경우

- 불변 클래스 → 굳이 clone 메서드를 제공하지 않는 게 좋음
    - 쓸데없는 복사를 지양하자

### 클래스가 가변 객체를 참조하는 경우

- `clone`은 원본 객체에 아무런 해를 끼치지 않는 동시에 복제된 객체의 불변식을 보장해야 한다
    - 사실상 생성자와 같은 효과
- clone을 재귀적으로 호출하는 방법
    - 배열을 복사하는 경우 → 배열의 `clone` 메서드 사용
    - 복사하는 필드가 `final`인 경우
        - Cloneable 아키텍처 : ‘가변 객체를 참조하는 필드는 final로 선언하라’는 일반 용법과 충돌
        - 일부 필드에서 final 제거 필요
- clone 재귀 호출로 충분하지 않은 경우 : `HashTable`
    - deep copy 지원
    - 엔트리 자신이 가리키는 연결 리스트 → 반복자를 사용하여 순회하며 복사
- `super.clone`을 호출하여 모든 필드를 초기 상태로 설정한 후 원본 객체의 상태 다시 생성
    - 고수준 API 활용, **BUT** 저수준으로 처리할 때보단 느림

## Cloneable을 구현한 모든 클래스는 clone을 재정의해야 한다

- 접근 제한자 : public
- 반환타입 : 클래스 자신
- public인 clone 메서드에서는 throws절을 없애야 한다
- Cloneable 구현 여부를 하위 클래스에서 선택
- clone 재정의 이후 동기화 필요 (스레드 안전 클래스)

## 이 모든 작업이 꼭 필요한 걸까?

- Cloneable을 이미 구현한 클래스를 확장하는 경우 → 어쩔 수 없이 clone 구현
- 더 나은 객체 복사 방식 제공 가능 : 복사(변환) 생성자, 복사(변환) 팩터리
    - 인터페이스 타입의 인스턴스를 인수로 받을 수 있음
    - 원본 구현 타입에 얽매이지 않고 복제본의 타입 적절히 선택 가능 (TreeSet)