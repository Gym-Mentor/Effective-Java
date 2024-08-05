# Item 1 Consider static factory methods instead of constructors

클래스가 인스턴스를 제공하는 전통적인 방법은 public 생성자를 만드는 것이다.  
다른 방법은 **public static factory method를 제공하여** 클래스의 인스턴스를 리턴하는 것이다.

public 생성자를 만드는 것 대신 static factory method를 제공하는 것은 여러 장단점이 있다.  
**장점**
- 생성자와 다르게 이름이 존재한다.
  - 리턴되는 오브젝트를 묘사할 수 있는 이름을 가질 수 있음
  - 여러 개의 이름이 있기에, 생성자와 달리 파라미터로 구분하지 않아도 됨
- 생성자와 다르게 static factory method는 호출될 때마다 새로운 오브젝트를 생성할 필요가 없다
  - immutable class나 static factory method가 미리 생성한 캐시된 인스턴스를 사용하는 것을 허용함
  - 불필요한 중복 오브젝트가 생성되는 것을 피하기위해 반복적으로 인스턴스를 제공한다.
  - Boolean.valueOf(boolean) 메서드를 예로 들 수 있다. 이 메서드는 객체를 절대 생성하지 않는다.
- 생성자와 달리 static factory method는 반환 타입의 하위 타입을 리턴할 수 있음
- 입력 파라미터의 함수로 호출마다 반환되는 객체의 클래스가 달라질 수 있다
- 메서드를 포함하는 클래스를 작성할 때 반환되는 객체의 클래스가 존재할 필요가 없다

**단점**
- public 또는 protected 생성자가 없는 클래스는 subclassed 되지 못한다.
- 개발자가 이를 찾기어렵다
  - from : 단일 파라미터를 받아 이 타입의 해당 인스턴스를 반환하는 타입 변환 메서드
  - of : 여러 파라미터를 받아 이를 포함하는 이 타입의 인스턴스를 반환하는 집계 메서드
  - valueOf : from과 of의 더 자세한 대안
  - instance 또는 getInstance : 파라미터 설명되는 인스턴스를 반환하지만 동일한 값이라고 할 수는 없음
  - create 또는 newInstance : getInstance와 유사하지만, 각 호출이 새로운 인스턴스를 반환할 것을 보장