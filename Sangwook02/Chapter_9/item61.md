# Item 61. 박싱된 기본 타입보다는 기본 타입을 사용하라

오토박싱이 있지만, 분명한 차이가 있으니 구분해서 사용해야.  
### 차이점
1. 기본 타입은 값만 가지지만, 박싱된 기본 타입은 식별성도 가짐.
2. 박싱된 타입은 null을 가질 수 있음.
3. 기본 타입이 시간, 메모리면에서 효율적

### 박싱된 기본 타입을 사용해야 하는 경우
- 컬렉션의 원소, 키, 값
- 매개변수화 타입이나 매개변수화 메서드의 타입 매개변수
- 리플렉션을 통해 메서드를 호출하는 경우