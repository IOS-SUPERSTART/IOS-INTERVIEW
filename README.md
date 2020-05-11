# IOS-INTERVIEW

## 2020-05-07 

### 지혜: View 객체에 대해 설명하시오.

### 종현 : [UIView 에서 Layer 객체는 무엇이고 어떤 역할을 담당하는지 설명하시오.](https://znf.kr/post/2/)

### 홍석: [UIWindow 객체의 역할은 무엇인가?](https://zeddios.tistory.com/283)
- UIWindow는 사용자 인터페이스에 배경(backdrop)을 제공하고, 중요한 이벤트 처리 행동(behaviors)을 제공하는 객체
- 스크린에 나타나는 모든 View는 Window로 묶여 있고, 각 Window는 앱의 다른 View와 독립적
- 대부분의 앱은 기기의 기본화면에 앱의 콘텐츠를 표시하는 하나의 Window만 있으면 됩니다.
- UIWindow는 UIView의 하위클래스이다.

### 수민 : [UINavigationController 의 역할이 무엇인지 설명하시오.](https://jeonsumin.github.io/blog/ios/navigation-Bar)
- 네비게이션 컨트롤러는 컨테이너 뷰 컨트롤러로써 네비게이션 스택을 사용하여 다른 뷰 컨트롤러를 관리하는 역할을 합니다. 
- 두개의 뷰를 화면에 표시하여 하나는 내비게이션 스택뷰에 포함된 최상위 컨텐트 뷰 컽르롤러의 콘텐츠를 나나태는 뷰 와 내비게이션 컨트롤러가 직접 관리하는 뷰가 있습니다. 
- 네비게이션 인터페이스의 변화에 따른 특정 액션을 동작하도록 하기 위해 내비게이션 델리게이트 객체를 사용할 수 있습니다. 

### 혜지: [모든 View Controller 객체의 상위 클래스는 무엇이고 그 역할은 무엇인가?](https://github.com/khyeji98/interview-study/blob/master/README.md#-모든-view-controller-객체의-상위-클래스는-무엇이고-그-역할은-무엇인가)

## 2020-04-30


### 홍석: NotificationCenter 동작 방식과 활용 방안에 대해 설명하시오.

- 동작방식 : 
특정 객체가 NotificationCenter에 등록된 Event를 발생시키면, 해당 Event를 처리할 것이라고 등록된 Observer들이 Event에 대한 행동을 취하는 것이 NotificationCenter가 동작하는 방식. 이렇게 특정 객체가 Event를 발생시키는 것을 Post라고 한다.

- [예제](https://baked-corn.tistory.com/42) : 
첫번째 뷰컨트롤러에서 특정 버튼 누르면, 두번째 뷰컨에 있는 레이블 숨기고, 세번째 뷰컨에 있는
레이블 표시하는 등, 다수의 객체들에게 동시에 이벤트의 발생을 알릴 수 있다.

- 활용방안 : 
로그인의 상태가 변하여 많은 뷰들을 업데이트해야 하는 경우에는 Notification이 적절할 것으로 생각된다.

- Delegate와의 차이점 : 
Delegate Pattern이 오직 지정된 객체랑 상호작용할 수 있는 반면, NotificationCenter는 어플리케이션 어느 곳에서, 어느 객체와도 상호작용을 할 수 있다. NotificationCenter는 단순한 Event를 다수의 객체에 동시에 알리고자 할 때 활용하면 좋겠지만, 그외에는 프로토콜을 정의하여 사용하는 Delegate 패턴을 사용하는 것이 더 좋을 것이다. (조금의 노력을 들여서 Delegate로 연결을 하면 코드가 읽기도 쉽고 추적이 쉬워진다)



### 혜지: [UIKit 클래스들을 다룰 때 꼭 처리해야하는 애플리케이션 쓰레드 이름은 무엇인가?](https://github.com/khyeji98/interview-study/blob/master/README.md#-uikit-클래스들을-다룰-때-꼭-처리해야하는-애플리케이션-쓰레드-이름은-무엇인가)

### 지혜: TableView를 동작 방식과 화면에 Cell을 출력하기 위해 최소한 구현해야 하는 DataSource 메서드를 설명하시오.

### 수민 : 하나의 View Controller 코드에서 여러 TableView Controller 역할을 해야 할 경우 어떻게 구분해서 구현해야 하는지 설명하시오.
- UIViewController 내에서 UITableViewDataSource 프로토콜 내 함수를 구현하게 되면 여러개의 UITableView가 모두 같은 메소드를 호출하기 때문에 뜻하지 않은 결과를 얻을 수 있는데 
- 이런 경우 UITableViewDataSource 프로토콜 내의 함수에서 분기해서 처리하면 됩니다. 
- 분기할때의 방법은 두가지 정도가 있는데 
    1. 각 테이블 뷰를 전역으로 가지고 있다가 메서드 인자중 하나인 tableView와 비교하는 것
    2. 각 테이블 뷰를 생성할때 Tag 값을 지정하고, 메서드 인자인 TableView의 Tag 값을 확인 하여 처리하는 방법이 있습니다. 
```swift
ovveride func viewDidLoad(){
super.viewDidLoad()

topTableView.delegate = self
topTableView.dataSource = self

bottomTableView.delegate = self
battomTableView.dataSource = self

// tag로 구분 
TopTalbleView.tag = 1
bottomTalbleView.tag = 1
}
``` 
```swift
//MARK: - tableView delegate
func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell{
    let cell = tableView.dequeueReusableCell(WithIdentifier: "Cell", for: indexPath)
    
    if tableView.tag == 1 {
        cell.taxtLabel?.text = "Top Table view \(indexPath.row)"
    }
    if tableView.tag == 2 {
        cell.taxtLabel?.text = "bottom Table View \(indexPath.row)"    
    }
    return cell
}

```

### 종현 : [App Bundle의 구조와 역할에 대해 설명하시오.](https://znf.kr/post/1/)

## 2020-04-23

### 지혜: [NSOperationQueue 와 GCD Queue 의 차이점을 설명하시오](https://www.zehye.kr/ios/2020/04/23/11iOS_GCD_NSOperation_queue/)

- 추가로 참고할 자료: [바로가기](https://www.zehye.kr/ios/2020/04/10/11iOS_GCD/)

### 홍석: [GCD API 동작 방식과 필요성에 대해 설명하시오](https://baked-corn.tistory.com/134)

**동작방식** 
- 프로그래머가 실행할 태스크(작업)을 생성하고 Dispatch Queue에 추가하면, GCD는 태스크(작업)에 맞는 스레드를 자동 생성해서 실행하고, 작업이 종료되면 해당 스레드 제거
- 디스패치 대기열(Dispatch Queue)은 GCD 기술 일부, Serial 과 Concurrent 2가지 종류
1. Serial Dispatch Queue는 한 번에 하나의 작업만을 실행
2. Concurrent Dispatch Queue는 이미 시작된 작업이 완료될 때까지 기다리지 않고 가능한 많은 작업을 진행
- 디스패치 소스 (Dispatch Source): 특정 유형의 시스템 이벤트 정보를 캡슐화하고, 해당 이벤트가 발생할 때마다 특정 클로저(블록) 객체 혹은 기능을 디스패치 대기열(Dispatch Queue)에 전달

**언제 사용해야 할까요?**
- **`Operation Queue`** : 비동기적으로 실행되어야 하는 작업을 객체 지향적인 방법으로 사용하는 데 적합합니다. KVO(key Value Observing)를 사용해 작업 진행 상황을 감시하는 방법이 필요할 때도 적합합니다.
- **`GCD`** : 작업이 복잡하지 않고 간단하게 처리하거나 특정 유형의 시스템 이벤트를 비동기적으로 처리할 때 적합합니다. 예를 들면 타이머, 프로세스 등의 관련 이벤트입니다.

**추가 내용**
- `Operation`은 `GCD`를 상위 수준으로 추상화한 api, 즉 `Operation`을 사용하는 것은 은연 중 `GCD`를 사용하는 것과 같음
- `GCD`는 시스템의 유닉스 레벨 수준에서 직접적으로 상호작용하는 저수준 C api, `Operation`은 Objective-C api 
- `Operation`은 보다 저수준에서 동작하는 `GCD`보다 상대적으로 느릴 수 밖에 없음
- `GCD` 와 `Operation Queue` 차이점?  
1. `Operation Queue` 에서는 동시에 실행할 수 있는 연산(Operation)의 최대 수 지정 가능
2. `Operation Queue` 에서는 KVO 사용할 수 있는 많은 프로퍼티 존재
3. `Operation Queue` 에서는 연산 일시 중지, 다시 시작 및 취소 가능


### 수민: [자신만의 Custom View를 만들려면 어떻게 해야하는지 설명하시오.](https://seonift.github.io/2018/05/23/Swift-%EC%BB%A4%EC%8A%A4%ED%85%80-UIView-%EC%A0%9C%EC%9E%91%ED%95%98%EA%B8%B0-with-Xib/)
커스텀뷰를 만드는 이유는 View마다 레이아웃을 따로 만들게 되면 view의 재사용에 용이? 하고 관리면에서 편리?하기 때문?에 커스텀뷰를 만들어 사용하게 되는데 cutomView를 만드는 방법은 기본적으로 swift 파일과 User Interface에 위치해있는 xib파일을 생성 한 후에 xib 파일에서 레아웃을 제작 한 후 swift 과 class를 연결해주어 xib가 생성한 swift 파일을 바라보게 하면 된다. 그 후에는 탬플릿 클래스로 만들어서 상속하여 사용할 수도 있습니다. 

### iOS 앱을 만들고, User Interface를 구성하는 데 필수적인 프레임워크 이름은 무엇인가? UIKit


### 혜지: [Foundation Kit은 무엇이고 포함되어 있는 클래스들은 어떤 것이 있는지 설명하시오.](https://github.com/khyeji98/interview-study/blob/master/README.md#-foundation-kit은-무엇이고-포함되어-있는-클래스들은-어떤-것이-있는지-설명하시오)

### 종현: [Delegate란 무언인가 설명하고, retain 되는지 안되는지 그 이유를 함께 설명하시오.](https://znf.kr/post/8/)


## 2020-04-16

### 홍석: [Bounds 와 Frame 의 차이점을 설명하시오](https://www.edwith.org/boostcourse-ios/lecture/16874/)

- Bounds는 뷰자기 자신의 좌표계이다. 이 좌표를 수정하게 되면 자신 아래에 있는 서브뷰들이 영향을 받는다.
- Frame은 자신의 슈퍼뷰에서 자신의 좌표를 나타내는 좌표계이다.
- 차이점? 프레임은 슈퍼 뷰 기준, 바운드는 해당 뷰 기준

<img src="https://cphinf.pstatic.net/mooc/20180102_77/1514826834081an6DQ_PNG/65_14.png"></img>

### 수민 : 실제 디바이스가 없을 경우 개발 환경에서 할 수 있는 것과 없는 것을 설명하시오
실제 디바이스가 없이 시뮬레이터를 이용할 경우 대표적으로  가속계 및 자이로스코프같은 모션, 카메라 및 마이크, 근접센서, 기압계 주변 광 센서를 테스트 해볼 수 없고 Apple의 푸시알림 받기 및 보내기, 개인정보 알림 등 을 테스트 할 수 없다. 

그 외 기능들은 시뮬레이터에서 테스트 가능하다 


### 종현 : [앱이 foreground에 있을 때와 background에 있을 때 어떤 제약사항이 있고, 상태 변화에 따라 다른 동작을 처리하기 위한 델리게이트 메서드들을 설명하시오](https://znf.kr/post/7/)



### 혜지: [scene delegate에 대해 설명하시오](https://github.com/khyeji98/interview-study/blob/master/README.md#-scene-delegate에-대해-설명하시오)

### 지혜: [앱이 In-Active 상태가 되는 시나리오를 설명하시오](https://www.zehye.kr/ios/2020/04/16/11iOS_application_state/)


## 2020-04-09

### 홍석: [Safearea에 대해서 설명하시오](https://devmjun.github.io/archive/SafeArea_1)

- Safe Area를 사용하는 이유?

아이폰X부터 적용된 노치 디자인에 맞춰 뷰의 컨텐츠와 컨트롤 부분이 올바르게 표시되고 간단히 탭 할 수 있어야 한다. Safe Area는 앱이 iPhoneX의 새로운 규격에 맞게 제대로 동작하는지 확인하기 위해 사용된다.
<img src="https://t1.daumcdn.net/cfile/tistory/99DEF33D5B3F27C704"></img>

- Swift에서 Safe Area 영역 값 확인, Safe Area 값을 확인하려면 #available(iOS 11.0, *) 적용

```
    if #available(iOS 11.0, *) {
        let window = UIApplication.shared.keyWindow
        let topPadding = window?.safeAreaInsets.top
        let bottomPadding = window?.safeAreaInsets.bottom
        let leftPadding = window?.safeAreaInsets.left
        let leftPadding = window?.safeAreaInsets.right
    }
```

- 예제

상단

    topSubview.frame.origin.x = view.safeAreaInsets.left
    topSubview.frame.origin.y = view.safeAreaInsets.top
    topSubview.frame.size.width = view.bounds.width - view.safeAreaInsets.left - view.safeAreaInsets.right
    topSubview.frame.size.height = 300

하단

    bottomSubview.leftAnchor.constraint(equalTo: view.safeAreaLayoutGuide.leftAnchor).isActive = true
    bottomSubview.rightAnchor.constraint(equalTo: view.safeAreaLayoutGuide.rightAnchor).isActive = true
    bottomSubview.bottomAnchor.constraint(equalTo: view.safeAreaLayoutGuide.bottomAnchor).isActive = true
    bottomSubview.heightAnchor.constraint(equalToConstant: 300).isActive = true

<img src="https://devmjun.github.io/img/posts/SafeArea_2.png" width="300px" height="300px"></img>
<img src="https://devmjun.github.io/img/posts/SafeArea_3.png" width="300px" height="300px"></img>

UIKit에서 Safe Area 프로퍼티와 메서드를 가지는 클래스들: UIView, UIViewController, UIScrollView, UITableView, UIColelctionView

### 지혜: [Left Constraint 와 Leading Constraint 의 차이점을 설명하시오](https://www.zehye.kr/ios/2020/04/02/11iOS_leading_trailing_left_right/)
### 종현: [오토레이아웃을 코드로 작성하는 방법은 무엇인가? (3가지)](https://znf.kr/post/6/)


### 수민: hugging, resistance에 대해서 설명하시오
huggin 과 resistance는 intrinsicContentSize를 알아야 하는데
intrinsicContentSize는 view 자체의 크기를말하는데 기본적으로 제공되는 view들이 width 와 heigth를 가질 수 있습니다. 

hugging 은 최대 크기에 대한 제한을 두고,

resistance는 최소 크기에 대한 제한 이라는 제약을 뜻합니다. 

hugging은 주어진크기보다 작아질 수 있다,

resistance는 주어진 크기보다 커질 수 있다라 해석할 수 있습니다. 




### 혜지: [Intrinsic Size에 대해서 설명하시오](https://github.com/khyeji98/interview-study#-intrinsic-size에-대해서-설명하시오)

## 2020-04-02

### 홍석: [접근 제어자의 종류엔 어떤게 있는지 설명하시오](https://jusung.gitbook.io/the-swift-language-guide/language-guide/25-access-control)

Swift 5개의 접근레벨

- Open & Public : Open과 Public 접근자 모두 선언한 모듈이 아닌 다른 모듈에서 사용가능. Open은 다른 모듈에서 오버라이드와 서브클래싱이 가능하지만, Public 접근자로 선언된 것은 다른 모듈에서는 오버라이드와 서브클래싱이 불가능.
- Internal : 기본 접근레벨, 아무 접근레벨을 선언하지 않으면 Internal로 간주. Internal레벨로 선언되면 해당 모듈 전체에서 사용 가능.
- File-private : 특정 엔티티를 선언한 파일 안에서만 사용 가능.
- Private : 특정 엔티티가 선언된 괄호({}) 안에서만 사용 가능.

접근레벨 가이드 원칙 (Guiding Principle of Access Levels)

- Swift에서 접근 레벨은 더 낮은 레벨을 갖고 있는 다른 엔티티를 특정 엔티티에 선언해 사용할 수 없다는 일반 가이드 원칙
- ex) public 변수는 더 낮은 레벨인 internal, File-private, private 타입에서 정의 불가

접근레벨 3가지 유형: 기본 접근레벨, 단일 타겟 앱을 위한 접근레벨, 프레임워크를 위한 접근레벨

- 예시
```
public class SomePublicClass {                  // explicitly public class
    public var somePublicProperty = 0            // explicitly public class member
    var someInternalProperty = 0                 // implicitly internal class member
    fileprivate func someFilePrivateMethod() {}  // explicitly file-private class member
    private func somePrivateMethod() {}          // explicitly private class member
}

class SomeInternalClass {                       // implicitly internal class
    var someInternalProperty = 0                 // implicitly internal class member
    fileprivate func someFilePrivateMethod() {}  // explicitly file-private class member
    private func somePrivateMethod() {}          // explicitly private class member
}

fileprivate class SomeFilePrivateClass {        // explicitly file-private class
    func someFilePrivateMethod() {}              // implicitly file-private class member
    private func somePrivateMethod() {}          // explicitly private class member
}

private class SomePrivateClass {                // explicitly private class
    func somePrivateMethod() {}                  // implicitly private class member
}
```
-> [더 자세한 예시](https://zeddios.tistory.com/383)

### 종현: [defer란 무엇인지 설명하시오.  / defer가 호출되는 순서는 어떻게 되고, defer가 호출되지 않는 경우를 설명하시오](https://znf.kr/post/4/)

### 혜지: [생성자(designated/convenience/required)의 차이점과 특징을 설명하시오](https://github.com/khyeji98/interview-study/blob/master/README.md#-생성자designatedconveniencerequired의-차이점과-특징을-설명하시오)
### 지혜: [프로토콜 지향 프로그래밍에 대해서 설명하시오](https://www.zehye.kr/ios/2020/04/03/12iOS_protocol_programming/)

## 2020-03-26

### 혜지: [Hashable이 무엇이고, Equatable을 왜 상속해야 하는지 설명하시오](https://github.com/khyeji98/interview-study#hashable)
### 홍석: [mutating 키워드에 대해 설명하시오](https://zeddios.tistory.com/258)
구조체와 열거형은 값타입

값타입 프로퍼티들은 해당 인스턴스 메소드 내에서 수정 불가

그러나 mutating 사용하여 특정 메소드 내에서 구조체, 열거형의 프로퍼티 수정 가능

### 종현: [탈출 클로저에 대하여 설명하시오](https://znf.kr/post/3/)

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


### 종현: [MVC 구조에 대해 블록 그림을 그리고, 각 역할과 흐름을 설명하시오](https://znf.kr/post/5/)


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
