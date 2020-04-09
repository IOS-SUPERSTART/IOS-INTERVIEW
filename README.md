# IOS-INTERVIEW

## 2020-04-09

### Safearea에 대해서 설명하시오
### 지혜: [Left Constraint 와 Leading Constraint 의 차이점을 설명하시오](https://www.zehye.kr/ios/2020/04/02/11iOS_leading_trailing_left_right/)
### 종현: 오토레이아웃을 코드로 작성하는 방법은 무엇인가? (3가지)


1. Anchor를 사용하는 방법

```
let subView = UIView.init()
subView.backgroundColor = UIColor.red
self.view.addSubview(subView)
 
subView.translatesAutoresizingMaskIntoConstraints = false
subView.leftAnchor.constraint(equalTo: view.leftAnchor, constant: 20.0).isActive = true
subView.rightAnchor.constraint(equalTo: view.rightAnchor, constant: -20.0).isActive = true
subView.topAnchor.constraint(equalTo: view.topAnchor, constant: 20.0).isActive = true
subView.bottomAnchor.constraint(equalTo: view.bottomAnchor, constant: -20.0).isActive = true
```

2. NSLayoutConstraint 를 사용하는 방법
```
let subView = UIView.init()
subView.backgroundColor = UIColor.red
subView.translatesAutoresizingMaskIntoConstraints = false
self.view.addSubview(subView)

let widthConstraint = NSLayoutConstraint.init(item: subView, attribute: .width, relatedBy: .equal, toItem: nil, attribute: .notAnAttribute, multiplier: 1.0, constant: 100)
subView.addConstraint(heightConstraint)
subView.addConstraint(widthConstraint)
let centerX = NSLayoutConstraint.init(item: subView, attribute: .centerX, relatedBy: .equal, toItem: self.view, attribute: .centerX, multiplier: 1.0, constant: 0)
let centerY = NSLayoutConstraint.init(item: subView, attribute: .centerY, relatedBy: .equal, toItem: self.view, attribute: .centerY, multiplier: 1.0, constant: 0)
self.view.addConstraint(centerX)
self.view.addConstraint(centerY)
```

3. Auto Layout Visual Format Language 

https://www.raywenderlich.com/277-auto-layout-visual-format-language-tutorial

### hugging, resistance에 대해서 설명하시오
### 혜지: [Intrinsic Size에 대해서 설명하시오](https://github.com/khyeji98/interview-study#-intrinsic-size에-대해서-설명하시오)

## 2020-04-02

### 홍석: 접근 제어자의 종류엔 어떤게 있는지 설명하시오
### 종현: defer란 무엇인지 설명하시오.  / defer가 호출되는 순서는 어떻게 되고, defer가 호출되지 않는 경우를 설명하시오
var value = "Hello"
func b() -> String {
    defer {
        value.append("world")
    }
    return value
}
print("B : \(b())")

value = "Hello"
func c() -> String {
    value.append("world")
    return value
}
print("C : \(c())")

value = "Hello"
func d() -> String {
    var f = value
    value.append("world")
    return f
}
print("D : \(d())")

func e() {
    do {
        defer{
            print("1")
        }
        defer{
            print("2")
        }
        defer{
            print("3")
        }
    }
}
print("E : 실행")
e()
print("E : 끝")
func f() {
    guard let fileURL = Bundle.main.url(forResource: "sample", withExtension: "txt") else {
        return
    }
    do {
        let content = try String(contentsOf: fileURL)
        print("Content : \(content)")
    }catch {
        print("Something went wrong")
    }
}
f()

### 혜지: [생성자(designated/convenience/required)의 차이점과 특징을 설명하시오](https://github.com/khyeji98/interview-study/blob/master/README.md#-생성자designatedconveniencerequired의-차이점과-특징을-설명하시오)
### 지혜: [프로토콜 지향 프로그래밍에 대해서 설명하시오](https://www.zehye.kr/ios/2020/04/03/12iOS_protocol_programming/)

## 2020-03-26

### 혜지: [Hashable이 무엇이고, Equatable을 왜 상속해야 하는지 설명하시오](https://github.com/khyeji98/interview-study#hashable)
### 홍석: [mutating 키워드에 대해 설명하시오](https://zeddios.tistory.com/258)
구조체와 열거형은 값타입

값타입 프로퍼티들은 해당 인스턴스 메소드 내에서 수정 불가

그러나 mutating 사용하여 특정 메소드 내에서 구조체, 열거형의 프로퍼티 수정 가능

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
익스텐션은 구조체, 클래스, 열거형, 프로토콜 타입에 새로운 기능을 추가할 수 있는 기능인데, 기능을 추가하려는 타입의 구현된 소스 코드를 알지 못하거나 볼수 없다해도, 타입만 알고 있다면 그 타입의 기능을 확장 할 수 있다. 

익스텐션으로 추가할 수 있는 기능은 

연산 타입의 프로퍼티/연산 인스턴스 프로퍼티

타입 메소드/ 인스턴스 메소드, 

이니셜라이저, 

서브스크립트, 

중첩 타입 

특정 프로토콜을 준수할 수 있도록 기능을 추가할 수 있다. 

추가로 기존에 존재하는 기능을 재정의 할 수는 없고, 기존에 존재하는 타입이 추가적으로 다른 프로토콜을 채택할 수 있도록 확장 할 수 있다. 


### 지혜: [Class/struct/enum 차이점과 사용하는 나의 기준에 대해 설명하시오](https://www.zehye.kr/swift/2020/01/15/19swift_grammer12/)

## 2020-03-19

### 지혜: [KVO 동작 방식에 대해 설명하시오](https://www.zehye.kr/ios/2020/03/19/11iOS_KVO/)

### 홍석: [Delegates와 Notification 방식의 차이점에 대해 설명하시오](https://medium.com/@Alpaca_iOSStudy/delegation-notification-%EA%B7%B8%EB%A6%AC%EA%B3%A0-kvo-82de909bd29)
Delegates와 Notification, 그리고 KVO 세가지 패턴 모두 특정 이벤트가 발생할 때 원하는 객체에 알려주어 해당되는 처리를 하는 방법을 가지고 있다.

- Delegates 는 보통 protocol 을 정의하여 사용

장점: 엄격한 Syntax, 로직 흐름 쉬움, 모니터링하는 외부 객체 필요없음

단점: 많은 줄의 코드 필요, delegate 설정에 nil 들어가지 않게 주의, 많은 객체들에게 이벤트 알려주는 것이 어렵고 비효율적

- Notification 은 Notification Center 라는 싱글턴 객체를 통해 이벤트들의 발생 여부를 옵저버를 등록한 객체들에게 Notification을 post 하는 방식

장점: 쉽게 구현 가능, 다수 객체에 동시에 이벤트 발생 알림 등

단점: key 값으로 Notification의 이름과 userInfo 를 서로 맞추기 때문에 컴파일 문제, 올바르게 userInfo 값 받아오는지 체크 불가

추적 쉽지 않음, Notification post 이후 정보를 받을 수 없음

KVO를 사용하는 경우는 (프로퍼티 단위의 변화 감지) 그 이유 명확

Delegation 과 Notification 경우 

이왕이면 프로토콜로 정의되어 있는 Delegation 을 웬만하면 사용하는 것이 좋다. (코드 읽기 쉽고 추적도 쉬워진다는 이유)


### 수민: 멀티 쓰레드로 동작하는 앱을 작성하고 싶을 때 고려할 수 있는 방식들을 설명하시오

기본적으로 멀티 쓰레드는 메인 스레드(main thread)에서 구현되어야 한다. 
가장 신경써야될 작업은 스레드에 안전하지 않은(Thread-unsafe) 변수는 서로 다른 스레드에서 동시에 접근하면 위험하기 때문에 해당 작업에 신경을 많이 써야한다.

1. Mutable, Immutable 
Immutable한 인스턴스는 스레드에 안전(Thread-safe)합니다. 

즉, 여러 스레드에서 한번에 접근해도 문제가 되지 않습니다. 

Mutable한 인스턴스는 스레드에 안전(Thread-safe)하지 않지만 읽기 전용으로만 사용한다면 문제가 되진 않습니다.

하지만 Mutable한 인스턴스를 하나 이상의 스레드에서 변경이 이루어진다면 문제가 발생합니다. 

2. 프로퍼티 속성
프로퍼티 속성에는 atomic, nonatomic이 있습니다. 

어떤 프로퍼티를 두 개의 스레드가 참조하고 있는 상황에서 해당 프로퍼티 접근자 메서드가 atomic하지 않는다면 값에 대한 싱크가 맞지 않아 문제가 발생할 수 있다. 이런 경우에 atomic으로 설정되어야 한다. 
하지만, Mutable한 인스턴스가 변경 중에 동시 접근할 경우가 없다면 nonatomic으로 사용해도 된다. 

3. Synchronized
메소드를 실행할 때 동시에 접근할 수 없도록 막고 싶을 때 해당 부분을 Lock을 걸 수 있다.
Lock을 걸어줌으로써 한 스레드에서 해당 부분이 끝낼 때 까지 다른 스레드에서 접근할 수 없게된다.

4. GCD
Swift에서 스레드 관련 작업은 Grand Central Dispatch API를 통해 처리한다.

GCD는 클로저 블록 안에 있는 특정 작업을 큐에 올리고, 해당 큐를 특정 스레드에 실행하는 방식입니다. 

애플이 스레드 프로그래밍을 효율적으로 할 수 있게 만들어준 만큼 적절하게 사용하여 Thread-safe하게 구현하는 것이 중요합니다.

5. Class, Struct

클래스는 레퍼런스 타입, 구조체는 값 타입입니다. 즉, 구조체가 파라미터로 전달될 때 스레드에 안전(Thread-safe)합니다.


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
