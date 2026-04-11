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


## Factory Method Pattern

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

' 일본에 갔을 때 110V를 사용하기 위해 돼지코를 중간에 끼워서 핸드폰 충건하는거 생각하면 됨 `

![alt text](</assets/img/Study/Pattern/AddapterPattern.png>)




## Bridge Pattern




---

# Behavioral Design Patterns
- 객체가 서로 어떻게 데이터를 주고받고 책임을 분산시키는 지에 대해 설명 
- 객체 간의 결합도를 낮추면서, 복잡한 제어 흐름을 효율적으로 관리

## Strategy Pattern

## Mediator Pattern

## Observer Pattern