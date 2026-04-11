---
title: GeeksforGeeks에서 디자인 패턴 5가지 공부하기
author: Chaewon Kim
date: 2026-04-11
category: Study
layout: post
---

## 중간고사 대비 디자인 패턴 공부하기 
- 2026-1학기 객체지향설계화패턴 시험 공부
- [GeeksforGeeks: Software Design Patterns](https://www.geeksforgeeks.org/system-design/software-design-patterns/)


# Creational Desing Patterns (생성 패턴)
- 객체를 직접 new 키워드로 만들어내는 것이 아닌, 상황에 맞게 효율적으로 객체를 만드는 방법에 대해 설명
- 객체 생성의 복잡성을 숨기고, **어떤 객체를 생성할지에 대해 효율적이고 유연하게 결정**하도록 도와주는 설계


## Abstract Factory Pattern
- 관련있는 객체들을 통째로 묶어서 생성
- 하나의 객체가 아닌 세트로 취급해주기 
- facotry of factories -> 일관성 보장, 교체 용이
- 서로 어울리는 부품들을 세트로 찍어내기 위해, 상황에 맞는 공장을 통째로 선택해서 사용하는 패턴

![alt text](/assets/img/Study/Pattern/AbstractFactoryPattern.png)

위 다이어그램은 라이트모드, 다크 모드 두가지를 UI에게 제공한다. 

문제: 라이트 모드일 때는 버튼도 하얗고 글자색은 검정. 
반대로 다크 모드일 때는 버튼이 어둡고 글자색은 흰색

해결 (추상 팩토리)
- 추상 공장: "버튼과 텍스트박스를 만드는 공장"이라는 틀을 생성
  - 라이트 공장: 하얀 버튼과 검은 글자를 만드는 구체적인 공장
  - 다크 공장: 어두운 버튼과 밝은 글자를 만드는 구체적인 공장

사용자는 어떤 공장인지만 알고 createButton()을 호출하면 현재 설정된 테마에 맞는 버튼이 생성된다. 

**구성요소**
- **Abstract Factory**
  - 모든 concrete factory가 따라야하는 표준 설계도
- **Concrete Factories**
  - abstract factory를 기반으로 실제로 구현하여 특정 패밀리의 객체를 찍어내는 실체
- **Abstract Products**
  - 공장에서 만들어질 결과물이 공통 규격
- **Concrete Products**
  - 각 패밀리의 색깔이 입혀진 실제 객체
- **Client**
  - 실제 사용자
  - 공장이나 제품의 구체적 종류 몰라도 됨


언제 사용하는걸까?
- 내가 지금 무슨 물건을 쓰긴 해야 하는데, 그 물건의 구체적인 종류가 실행 환경(OS, 국가, 설정)에 따라 통째로 바뀌어야 할 때

- 눈높이 설명
  - 게임을 만들 때 쉬움모드 vs 어려움 모드
    - 쉬움 모드 : 약한 몬스터, 내구도 강한 아이템
    - 어려움 모드 : 강한 몬스터, 내구도 약한 아이템
  - 난이도가 결정되는 순간에 해당 난이도 전욕 팩토리로 갈아끼우면됨
  - 그러면 엔진 코드 수정할 필요 없이 팩토리가 주는 몬스터와 아이템 설정하면 됨 

![alt text](/assets/img/Study/Pattern/AbstractFactoryExample.png)
위의 사진을 통해 더 자세히 알아보자. 

**시나리오**
- 공장에서 자동차를 생산하려고함
- 국가마다 자동차 규제가 다름
- 국가마다 찍어내는 차가 다름 
  
**CarFactory (Abstract interface)**
- 모든 공장은 createCar()와 createSpecificatino() 메서드를 가지고 있어야함.

**Car, CarSpecification (Abstract Products)**
- 제품의 추상적인 타입을 나타냄

**CarFactoryClient (Client)**
- 운영자
- concrete product 몰라도 됨


```cpp
#include <memory>
#include "Car.h"
#include "CarSpecification.h"


/* Abstract Factory Interface */
class CarFactory {
public:
    virtual Car* createCar() = 0;
    virtual CarSpecification* createSpecification() = 0;
};

/* Concrete Factories */
class NorthAmericaCarFactory : public CarFactory {
public:
    std::unique_ptr<Car> createCar() override {
        return std::make_unique<Sedan>();
    }
    std::unique_ptr<CarSpecification> createSpecification() override {
        return std::make_unique<NorthAmericaSpecification>();
    }
};

class EuropeCarFactory : public CarFactory {
public:
    std::unique_ptr<Car> createCar() override {
        return std::make_unique<Hatchback>();
    }
    std::unique_ptr<CarSpecification> createSpecification() override {
        return std::make_unique<EuropeSpecification>();
    }
};

/* Abstract Product Interface */
//Car
class Car {
public:
    virtual void assemble() = 0;
};
//Car Specifications
class CarSpecification {
public:
    virtual void display() = 0;
};

/* Concrete Products */
//  Sedan Car
class Sedan : public Car {
public:
    void assemble() {
        std::cout << "Assembling Sedan car." << std::endl;
    }
};

//  Hatchback Car
class Hatchback : public Car {
public:
    void assemble() {
        std::cout << "Assembling Hatchback car." << std::endl;
    }
};

// NorthAmerica Car Specification
class NorthAmericaSpecification : public CarSpecification {
public:
    void display() {
        std::cout << "North America Car Specification: Safety features compliant with local regulations." << std::endl;
    }
};

// Europe Car Specification
class EuropeSpecification : public CarSpecification {
public:
    void display() {
        std::cout << "Europe Car Specification: Fuel efficiency and emissions compliant with EU standards." << std::endl;
    }
};

```
**장점**
- 느슨한 결합
- 교체 편리
- OCP 원칙 지원

**단점** 
- 클래스 폭발
- 새로운 제품 추가시 모두 고쳐야함



## Factory Method Pattern
- 객체 생성을 Factory 클래스로 캡슐화 처리하여 대신 생성하게 하는 패턴 

![alt text](/assets/img/Study/Pattern/FactoryMethodPattern.png)

만약 위의 패턴을 사용하지 않는다면 if-else로 도배된 코드가 될거임

예시- 결제 시스템
- 카카오페이
- 삼성페이
- 어떤것을 선택하느냐 따라 기기가 뱉은 인스턴트가 달라짐

**구성 요소**
- **Product (interface)**
  - 모든 객체가 가져야할 공통 메서드
- **Concrete Product**
  - 팩토리 메서드가 생산한 실제 객체
- **Creator (abstract class/interface)**
  - 객체를 만드는 규칙과 그 객체로 무엇을 할지 정하는 얘
- **Concrete Creator**
  - 상황에 맞춰 실제 객체를 찍어내는 공장

![alt text](/assets/img/Study/Pattern/FactoryMethodPatternEx.png)

```java
// Library classes
abstract class Vehicle {
    public abstract void printVehicle();
}

class TwoWheeler extends Vehicle {
    public void printVehicle(){
        System.out.println("I am two wheeler");
    }
}
class FourWheeler extends Vehicle {
    public void printVehicle(){
        System.out.println("I am four wheeler");
    }
}

// Factory Interface
interface VehicleFactory {
    Vehicle createVehicle();
}

// Concrete Factory 
class TwoWheelerFactory implements VehicleFactory {
    public Vehicle createVehicle(){
        return new TwoWheeler();
    }
}
// Concrete Factory 
class FourWheelerFactory implements VehicleFactory {
    public Vehicle createVehicle(){
        return new FourWheeler();
    }
}

// Client class
class Client {
    private Vehicle pVehicle;
    public Client(VehicleFactory factory){
        pVehicle = factory.createVehicle();
    }
    public Vehicle getVehicle() { return pVehicle; }
}

// Driver program
public class GFG {
    public static void main(String[] args)
    {
        VehicleFactory twoWheelerFactory = new TwoWheelerFactory();
        Client twoWheelerClient = new Client(twoWheelerFactory);
        Vehicle twoWheeler = twoWheelerClient.getVehicle();
        twoWheeler.printVehicle();

        VehicleFactory fourWheelerFactory = new FourWheelerFactory();
        Client fourWheelerClient = new Client(fourWheelerFactory);
        Vehicle fourWheeler = fourWheelerClient.getVehicle();
        fourWheeler.printVehicle();
    }
}

```

내가 눈높이로 위 두개 요약하기
- 햄버거 가계가 있음
- 어떤 햄버거 가계를 창업할지를 정할 때에는 추상 팩토리 메서드 패턴
- 창업 후 어떤 햄버거를 만들지 정할 때에는 팩토리 매서드 패턴


## Builder Pattern
- 복잡한 객체를 조립하듯 하나하나 쌓아 올려서 만드는 방식 
- 서브웨이처럼 빵고르고 햄 고르고 치즈 고르고 소스 고르는 느낌

**시나리오**
1. 빵은 뭘로 할까요? (허니오트)
2. 길이는요? (15cm)
3. 치즈는요? (아메리칸 치즈)
4. 야채는 다 넣을까요? (할라피뇨 빼고 다요)
5. 소스는요? (스위트 칠리)

```java
// 그냥 쌩으로 객체 생성시 
Subway mySandwich = new Subway("허니오트", 15, "아메리칸", true, true, true, false, "칠리", ...);

// 빌더 패턴 사용시 
// 빌더 패턴을 사용한 깔끔한 주문
Subway mySandwich = new SubwayBuilder()
    .setBread("허니오트")
    .setLength(15)
    .setCheese("아메리칸")
    .addVegetables()
    .setSource("스위트 칠리")
    .build(); // 마지막에 딱 완성!
```

**구성요소**
- **Product** (최종 결과물: 샌드위치)
  - 당신의 손에 쥐어진 완성된 15cm 에그마요 샌드위치.
- **Builder** (샌드위치 제조 매뉴얼)
  - 서브웨이의 제조 순서
- **Concrete Builder** (샌드위치 아티스트 - 알바생)
  - 내 주문을 듣고 실제로 빵을 가르고 재료를 넣는 알바생.
- **Director** (추천 꿀조합 / 메뉴판)
  - 추천 조합 및 서브웨이 클럽 주세요라는 주문 그 자체.
  - 특징: 우리가 일일이 야채를 고르기 귀찮을 때, **"메뉴판에 적힌 순서대로(Director) 만들어주세요"**라고 하면 알바생(Builder)이 알아서 정해진 순서대로 조립합니다.
  - 즉, 복잡한 조립 과정을 미리 정해진 루틴대로 실행해 주는 매니저입니다.
- **Client** (나 - 배고픈 손님)
  - 어떤 샌드위치를 먹을지 정하고, 알바생(Builder)을 지목한 뒤, 공정(Director)을 시작시킵니다.

```java
// 순서 고정 
// 1. Product: 최종 결과물 (샌드위치)
class Sandwich {
    private String bread;
    private String mainIngredient;
    private String sauce;

    public void setBread(String bread) { this.bread = bread; }
    public void setMainIngredient(String mainIngredient) { this.mainIngredient = mainIngredient; }
    public void setSauce(String sauce) { this.sauce = sauce; }

    public void displayInfo() {
        System.out.println("--- 주문하신 샌드위치 내역 ---");
        System.out.println("빵: " + bread);
        System.out.println("메인 재료: " + mainIngredient);
        System.out.println("소스: " + sauce + "\n");
    }
}

// 2. Builder Interface: 제조 매뉴얼
interface SandwichBuilder {
    void buildBread();
    void buildMainIngredient();
    void buildSauce();
    Sandwich getResult();
}

// 3. ConcreteBuilder: 특정 메뉴 전담 알바생 (에그마요 전담)
class EggMayoBuilder implements SandwichBuilder {
    private Sandwich sandwich = new Sandwich();

    @Override
    public void buildBread() {
        sandwich.setBread("허니오트 (Honey Oat)");
    }
    @Override
    public void buildMainIngredient() {
        sandwich.setMainIngredient("에그마요 (Egg Mayo)");
    }
    @Override
    public void buildSauce() {
        sandwich.setSauce("랜치 & 스위트 칠리");
    }
    @Override
    public Sandwich getResult() {
        return sandwich;
    }
}

// 4. Director: 꿀조합 레시피 (매니저)
class SubwayDirector {
    // 레시피대로 조립을 지시함
    public void construct(SandwichBuilder builder) {
        builder.buildBread();
        builder.buildMainIngredient();
        builder.buildSauce();
    }
}

// 5. Client: 손님 (나)
public class Main {
    public static void main(String[] args) {
        // 1. 에그마요 잘 만드는 알바생(Builder)을 부릅니다.
        SandwichBuilder eggMayoBuilder = new EggMayoBuilder();
        
        // 2. 레시피(Director)를 가져옵니다.
        SubwayDirector director = new SubwayDirector();

        // 3. 매니저가 알바생에게 "레시피대로 만드세요"라고 지시합니다. (조립)
        director.construct(eggMayoBuilder);

        // 4. 완성된 샌드위치를 받습니다. (getResult)
        Sandwich mySandwich = eggMayoBuilder.getResult();

        // 5. 맛있게 확인합니다.
        mySandwich.displayInfo();
    }
}

```

**장점**
- 가독성 좋음
- 불변성

**단점**
- 클래스 개수 증가
- 구조 변경 취약
  
---


# Structural Desing Patterns (구조 패턴)
- 이미 만들어진 클래스나 객체를 합치거나, 서로 다른 객체끼리 어떻게 연결할 지에 대해 설명 
- 서로 다른 인터페이스를 가진 객체들을 협력하게 함
- 복잡한 시스템을 **구조화하여 확장성 높이기**
- 컴포넌트 간의 관계를 간소화시킴으로써 코드 유연성 개선

## Adapter Pattern
- 두 개의 일치하지 않는 인터페이스를 다리로서 연결해주는 것
- legacy code나 third-party libraries를 새로운 시스템에 넣을 때 매우 유용함

legacy code란
- 과거의 누군가가 남겨둔 코드
- 결합도가 높거나 유지 관리가 어려운 코드
- 주석이 없어 파악이 어려운 코드
- 테스트 코드가 없는 코드

이렇게 사용은 해야하지만 수정 및 유지보수가 어려운 코드를 레거시 코드라고 한다. 

이 코드를 가져올 때 우리가 새로 정한 인터페이스와 일치하지 않는 경우가 있다. 

레거시 코드를 수정하자니 버그가 발생할 수도 있고, 새로 만들자니 시간이 낭비된다. 

이를 해결하는 방법으로 레거시 코드를 그대로 두고 중간 다리로 **Class Adapter(using inheritance), Object Adapter(using composition)**를 만들어준다. 

일본에 갔을 때 110V를 사용하기 위해 돼지코를 중간에 끼워서 핸드폰 충건하는거 생각하면 됨

![alt text](</assets/img/Study/Pattern/AddapterPattern.png>)

**구성요소**
- **Target interface**
  - 클라이언트(사용자)가 지금 바로 사용하고자 하는 표준 규격 (220V)
- **Adaptee**
  - 이미 존재하지만, 현재의 타겟 인터페이스와 맞지 않는 인터페이스를 가진 클래스(110V)
- **Adapter**
  - 타겟 인터페이스를 구현하면서, 내부적으로는 어댑티를 감싸서 사용하는 중간 다리 (돼지코)
- **Client**
  - 타겟 인터페이스를 통해 기술을 사용하려는 사람 (일본여행간 한국인)

**시나리오**
- printDocument()라는 이름의 메서드를 가진 LegacyPrinter class를 가지고 있다. 
- print() 라는 이름의 메서드를 가진 새로운 시스템에 적용하고 싶다. 
- Adapter design pattern을 이용해서 해결해보자. 

```cpp
// target interface
class Printer{
    public:
        virtual void print() = 0;
};

//Adaptee
class LegacyPrinter{
    public:
        void printDocument(){
            std::cout <<"legacy printer code " << std::endl;
        }
};

// Adapter
class PrinterAdapter : public Printer{
    private:
        LegacyPrinter legacyPrinter;
    public:
        // 기존 코드 오버라이딩하기 
        // print가 호출되면 legacy의 printDocument가 실행되도록 
        void print() override{
            legacyPrinter.printDocument();
        }
};

//client code
void clientCode(Printer& printer){
    printer.print();
}

```
장점
- 코드 재사용성 좋아짐
- 단일 책임 원칙
- 교체 용이성 

단점
- 복잡성 증가
- 성능 오버헤드
- 어댑터 많아지면 오히려 유지 보수가 어려워짐 


## Bridge Pattern




---

# Behavioral Design Patterns
- 객체가 서로 어떻게 데이터를 주고받고 책임을 분산시키는 지에 대해 설명 
- 객체 간의 결합도를 낮추면서, 복잡한 제어 흐름을 효율적으로 관리

## Strategy Pattern

## Mediator Pattern

## Observer Pattern