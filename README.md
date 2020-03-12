# IOS-INTERVIEW


## 2020-03-12


### 지혜: [instance 메서드와 class 메서드의 차이점 설명](https://www.zehye.kr/swift/2020/03/12/1swift_instance_class_method/)

### 홍석: Singleton 패턴을 활용하는 경우를 예를 들어 설명

### 수민: Delegate 패턴을 활용하는 경우를 예를 들어 설명



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
