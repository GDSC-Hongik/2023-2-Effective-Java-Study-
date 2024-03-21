# 복구할 수 있는 상황에는 검사 예외를, 프로그래밍 오류에는 런타임 예외를 사용하라

```
💡 확실하지 않다면 비검사 예외를 던지자.
```

## 검사 예외

- 호출하는 쪽에서 **복구**하리라 여겨지는 상황
- 호출자가 예외를 catch로 잡아 처리하거나 더 바깥으로 전파
- 복구 가능 여부 → API 설계자의 판단에 달림

## 비검사 예외

```
💡 여러분이 구현하는 비검사 throwable은 모두 RuntimeException의 하위 클래스여야 한다.
```

- 프로그램에서 잡을 필요가 없거나 잡지 말아야 함
    - 적절한 오류 메시지를 내뱉으며 중단

### 런타임 예외

- 프로그래밍 **오류**를 나타내는 경우
- 전제조건을 만족하지 못했을 때 발생

### 에러

- JVM이 더 이상 수행을 계속할 수 없는 상황
    - 자원 부족
    - 불변식 깨짐
- `Error`는 상속하지 말아야 함, throw 문으로 직법 던지는 일도 없어야 함

## 예외도 객체다

- 어떤 메서드라도 정의 가능
- 예외를 일으킨 상황에 대한 정보를 코드 형태로 전달
- 검사 예외 : 예외 상황에서 **벗어나는 데 필요한 정보**를 알려주는 메서드 함께 제공