#IOS-INTERVIEW

## 2020-03-26

### 혜지: [Hashable이 무엇이고, Equatable을 왜 상속해야 하는지 설명하시오](https://github.com/khyeji98/interview-study#hashable)
### 홍석: mutating 키워드에 대해 설명하시오(https://zeddios.tistory.com/258)
### 종현: 탈출 클로저에 대하여 설명하시오

1. Closure의 의미
 - Apple 공식 
 - Closures are self-contained blocks of functionality that can be passed around and used in your code
 - 클로저는 코드내에서 사용가능한 독립된 기능 블록이다.
  { (parameters) -> return type in
      statements
  }
  이런식으로 사용된다.
2. Closure의 사용처 
 - 제일 많이 사용되는 사용처
 - 경험상 Api 호출할 때
 - CustomView만들 때
    init(title: String?, style: UIAlertAction.Style, handler: ((UIAlertAction) -> Void)? = nil)
    이런식으로 우리가 만든 Custom View 도 설정 가능하다.

### 수민: Extension에 대해 설명하시오
### 지혜: [Class/struct/enum 차이점과 사용하는 나의 기준에 대해 설명하시오](https://www.zehye.kr/swift/2020/01/15/19swift_grammer12/)

## 2020-03-19

### 지혜: [KVO 동작 방식에 대해 설명하시오](https://www.zehye.kr/ios/2020/03/19/11iOS_KVO/)

### 홍석: Delegates와 Notification 방식의 차이점에 대해 설명하시오(https://medium.com/@Alpaca_iOSStudy/delegation-notification-%EA%B7%B8%EB%A6%AC%EA%B3%A0-kvo-82de909bd29)

### 수민: 멀티 쓰레드로 동작하는 앱을 작성하고 싶을 때 고려할 수 있는 방식들을 설명하시오

### 종현: MVC 구조에 대해 블록 그림을 그리고, 각 역할과 흐름을 설명하시오

![mvc](https://user-images.githubusercontent.com/59017672/77244438-24e30100-6c58-11ea-949b-c94951cb2056.jpg)

M - Model : 소프트웨어에서 데이터를 의미
V - View : 사용자에게 보여지는 부분을 의미
C - Controller : 사용자 입력 받는 부분을 의미

User -> C -> M -> C -> V -> User
유저는 Controller를 통해 Application에 입력을 하고, Controller를 입력받은 부분을 Model에서 데이터 처리한후 Controller에서 View에 보여줘 유저에게 Response을 보여준다.

Model : 예) NSObject
View : 예) Storyboard, UIView
Controller : 예) ViewController

### 혜지: [프로토콜이란 무엇인지 설명하시오](https://github.com/khyeji98/interview-study#프로토콜)


## 2020-03-12


### 지혜: [instance 메서드와 class 메서드의 차이점 설명](https://www.zehye.kr/swift/2020/03/12/1swift_instance_class_method/)

### 홍석: Singleton 패턴을 활용하는 경우를 예를 들어 설명
(https://www.edwith.org/boostcourse-ios/lecture/16876/)
(https://developer.apple.com/library/archive/documentation/General/Conceptual/DevPedia-CocoaCore/Singleton.html)

- 객체의 생성 과정 관여하는 패턴
- 특정 클래스의 인스턴스가 오직 하나임을 보장하고(고정된 메모리) 이 인스턴스에 접근할 방법 제공(전역)
- 애플이 제공하는 공식 문서 예시로, 응용 프로그램에서 다른 객체들에 사운드를 제공하는 클래스가 있다면, 싱글턴 패턴을 활용할 수 있다고 한다. 혹은 부스트코스 2강에서 Singleton 구현해보기 파트에서 UserInformation 클래스에서 타입 프로퍼티 shared 활용 예시 참고.
- 생성자가 여러 차례 호출되어도 실제로 메모리에 할당되는 객체는 하나이기 때문에 메모리 낭비를 방지할 수 있다.
- 싱글턴으로 생성된 클래스의 인스턴스는 전역 인스턴스이기 때문에 다른 클래스의 인스턴스들이 데이터를 공유하기 쉽다.
- 싱글턴 인스턴스가 너무 많은 일을 하거나, 많은 데이터를 공유하면 다른 클래스 인스턴스들 간 결합도가 높아져 수정이 어려워지고 테스트하기 어려워진다.

### 수민: Delegate 패턴을 활용하는 경우를 예를 들어 설명
델리게이트는 어떤 객체가 해야 하는 일을 부분적으로 확장해서 대신 처리하는 것을 말합니다.
델리게이트는 대신 처리 해줄 객체와 처리하라고 시키는 객체라 생각할 수 있고
델리게이트 패턴을 활용하는 경우는 대표적으로 테이블 뷰에서 활용합니다.
범용적이고 재사용 하기위해 델리게이트 패턴을 활용하는 경우가 있습니다. 

## 2020-03-05


### 지혜: [Optional은 무엇인지 설명하시오](https://www.zehye.kr/swift/2020/03/05/swift_optional_interview/)


### 홍석: [Struct가 무엇이고 어떻게 사용하는지 설명하시요](https://jusung.gitbook.io/the-swift-language-guide/language-guide/09-classes-and-structures)

* 스위프트의 자료구조는 크게 클래스, 구조체, 열거형, 프로토콜로 형성

* 그 중 클래스와 구조체의 공통점
1. 값 저장 위한 프로퍼티 정의, 기능 제공 위한 메소드 정의
2. 내부에서 subscript 문법을 이용해 특정 값 접근 가능
3. 초기화
4. 기본 구현을 기능 확장
5. 특정 종류의 표준 기능을 제공하기 위해 프로토콜 채택

* 클래스만 가능한 것 - 참조타입
1. 상속
2. 타입캐스팅
3. 소멸자
4. 참조카운트(구조체는 항상 복사 전달)

* 구조체와 열거형은 값타입

* 클래스 대신 구조체를 사용하는 경우, 그 외에 모든 경우에는 클래스 사용하면 된다
1. 구조체의 주 목적이 관계된 간단한 값을 캡슐화하는 경우
2. 구조체 인스턴스가 참조되기 보다 복사되길 기대하는 경우
3. 구조체로 저장된 어떤 프로퍼티가 참조되기 보다 복사되길 기대하는 경우
4. 구조체가 프로퍼티나 메소드 등을 상속할 필요가 없는 경우


### 수민 

#### fast-enumeration

Swift는 Objective-C에서 fast-enumeration이라는 집합 타입 내 원소 객체 들을 순회하는 반복문을 지원한다. Python과 비슷하게 swift의 for...in 구문은 시퀀스, 제너레이터 라는 개념을 사용하고 있다. 

swift가 기본적으로 제공하는 Array, Dictionary는 기본적으로 for..in 구문에 적용이 가능하고 내부적으로 SequenceType 이라는 프로토콜을 따르고 있다. 

Objective-C 2.0에 들어 열거형 변수를 좀더 효과적이고 안전하게 사용하기 위해 for 문법이 업그레이드 되었는데 이것을 fast Enumeration 이라한다. 주로 foreach와 같은 기능을 한다. 

```swift
for anItem in aSequenceType {
    doSomthingWith(anItem)
}
```
