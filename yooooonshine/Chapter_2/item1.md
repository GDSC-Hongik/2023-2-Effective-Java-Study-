# 생성자 대신 정적 팩토리 메서드를 고려하라

## 정적 팩터리 메서드란?
단순히 그 클래스의 인스턴스를 반환하는 메서드
## 장점
* 이름을 가질 수 있다.: 
	* 이름을 가지므로 생성자가 하는 역할에 대한 정확한 설명을 해주어 실수할 일이 줄어들게 된다. 또한 같은 매개변수를 가지면서 다른 역할을 하는 생성자를 만들고 싶을 때 단순 생성자로는 어렵지만, 정적 팩터리 메서드를 통해서는 가능하다.
* 호출될 때마다 인스턴스를 새로 생성하지 않아도 된다.
	* 따라서 인스턴스를 미리 만들어 놓거나, 인스턴스를 캐싱하여, 성능을 올릴 수 있다.
	* 반복 요청에 같은 인스턴스를 반환하면서, 인스턴스의 생명 주기를 통제할 수 있는 클래스를 인스턴스 통제 클래스라고 한다. 이를 통해 3가지 장점이 있다.
		* 1. 싱글톤으로 만들 수 있다.
		* 2. 인스턴스 불가로 만들 수 있다.
		* 3. 불변 값 클래스에서 동치(a == b일때만 a.equals(b)성립, 즉 주소가 같을 때만 같은 인스턴)인 인스턴스가 단 하나뿐임을 보장할 수 있다.
* 반환 타입의 하위 타입 객체를 반환할 수 있는 능력이 있다.
	* 반환할 객체의 클래스를 선택할 수 있다는 것이다.
	* 즉 리턴 타입을 클래스가 상속한 인터페이스로 하여도 무관해서, 유연성이 생긴다는 것이다.
* 입력 매개변수에 따라 매번 다른 클래스의 객체를 반환할 수 있다.
	* 상위 클래스의 정적 팩토리 메서드 반환 타입은 하위(자식)클래스이어도 무관하기에, 상위 클래스를 extends한 하위 클래스에서 상황에 알맞게 구현하여, 상위 클래스 정적팩토리에 메서드 반환으로 하위 클래스 인스턴스를 리턴한다.
* 정적 팩토리 메서드를 작성하는 시점에는 반환할 객체의 클래스가 존재하지 않아도 된다.
```java
public class TickeStore {
	public static List<TicketSeller> getSellers(){
		return new ArrayList<>();
	}
}
```
이와 같이 구현체를 만들지 않았어도 나중에 주입을 통해 가능하므로 존재하지 않아도 된다는 뜻이다. 
## 단점
* 상속을 하려면 public이나 protected 생성자가 필요하니 정적 팩터리 메서드만 제공하면 하위 클래스를 만들 수 없다.
	* 즉 상속을 할때는 하위 클래스의 생성자에서는 super()를 통해 미리 상위 클래스 객체를 만들어야 하는데, private, protected라 접근이 불가능해 생성자를 호출할 수 없다는 것이다.
* 정적 팩터리 메서드는 프로그래머가 찾기 힘들다.
	* 즉 사용자가 정적 팩토리 메서드 클래스를 인스턴스화 할 방법을 찾아야 한다는 것이다. 이 불편함을 어느정도 해소하기 위하여 널리 사용되는 메서드명을 사용하는 것이다. 아래는 그 예시이다.

## 메서드 명
* from: 매개변수를 하나 받아서 해당 타입의 인스턴스를 반환
* of: 여러 매개변수를 받아 적합한 타입의 인스턴스를 반환
* valueOf: from과 of의 더 자세한 버전이라는 데 잘 모르겠다.
* instance, getInstance: 매개변수로 명시한 인스턴스를 반환, 혹은 싱글톤 객체를 가져올 때 사용
	* 예를 들어 File클래스 인스턴스를 3개 생성하여 보관중이라면 이를 매개변수로 구분해 가져오는 것.
* create, newInstance: instance와 getInstance와 같지만 매번 새로운 인스턴스를 반환한다.
* getType: getFile등으로 사용되며, File클래스의 인스턴스를 반환하라는 것이다. 주로 생성할 클래스가 아닌 다른 클래스에 팩터리 메서드를 정의할 때 쓴다.
* newType: 위의 getType과 유사하나 매번 새로운 인스턴스를 반환한다.
* type: getType과 newType을 구분하기 귀찮을 때 사용하는 것.