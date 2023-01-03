# 디자인 패턴
### 싱글톤 패턴
- 하나의 클래스에 오직 하나의 인스턴스만 가지는 패턴
- 데이터 베이스 연결 모듈에 많이 사용됨
- 생성 비용 감소, 의존성 높아짐 -> DI 이용 결합 느슨하게  
```
public class Settings {
    private Settings() {}

    private static class SettingsHolder() {
        private static final Settings INSTANCE = new Settings();
    }

    public static Settings getInstance() {
        return SettingsHolder.INSTANCE;
    }
}
```
### 팩토리 패턴
- 객체 생성 부분을 추상화한 패턴, 상위 클래스는 사용만
```
class CoffeeFactory {
    public static Coffee getCoffee(String type, int price) {
        // type에 따라 생성 분기 처리
    }
}
..
public static void main(String[] args) {
    // 옵션에 따라 다른  객체 반환 
    Coffee _coffee_ = CoffeeFactory.getCoffee("옵션", 1000) 
    ..
}
..
```
### 전략 패턴, 정책 패턴
- 객체의 행위를 바꾸고 싶을 때, 직접 수정하지 않고 전략이라고 부르는 캡슐화한 알고리즘을 컨텍스트 안에서 바꿔 상호 교체가 가능하게 하는 패턴
```
interface PaymentStrategy {
    public void pay(int amount);
}
class A_CardStrategy implement PaymentStrategy { 
    @Override pay(){ } 
    ... 
}
class B_CardStrategy implement PaymentStrategy { 
    @Override pay(){ } 
    ... 
}
class Shop { 
    pay(PaymentStrategy paymentMethod ) { 
        paymentMethod.pay(); 
    } 
    ... 
}
..
public static void main() {
    ..
    shop.pay(new A_CardStrategy());
    shop.pay(new B_CardStrategy());
    ..
}
```
### 옵저버 패턴
- 주체가 어떤 객체의 상태 변화를 관찰하다가 상태 변화가 있을 때마다 메서드 등을 통해 옵저버 목록에 있는 옵저버들에게 변화를 알려주는 패턴
- 이벤트 기반 시스템에서 사용, MVC 패턴에서도 사용 
- Observer가 Subject를 구독하는 형식
```
interface Subject {
    public void register(Observer obj);
    public void unregister(Observer obj);
    public void notifyObservers();
    public Object getUpdate(Observer obj);
}
interface Observer {
    public void update();
}
```
### 프록시 패턴과 프록시 서버
* 프록시 객체
  어떤 대상의 기본적인 동작(속성 접근, 할당, 순회, 열거 등)의 작업을 가로챌 수 있는 객체를 뜻한다.
  - target : 프록시할 대상, handler : target 동작을 가로채서 정의할 동작
* 프록시 패턴
  대상 객체에 접근하기 전 그 접근에 대한 흐름을 가로채 대상 객체 앞단의 인터페이스 역할을 하는 디자인 패턴이다.
  - 보안, 데이터 검증, 캐싱, 로깅에 사용함.
* 프록시 서버
  nginx 등, 서버 앞단에서 DDOS 방어, HTTPS 구축에 사용됨. 
  CORS(Cross-Origin Resource Sharing)와 프론트엔드 프록시 서버
  - 서버가 웹 브라우저에서 리소스를 로드할 때, 다른 오리진 통해 로드 못하게 막는 것 > 프록시 서버를 두어 요청되는 오리진을 바꿈


