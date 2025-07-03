# 생성자(Constructor)

**생성자(Constructor)** 는 Solidity에서 **스마트 계약(Smart Contract)** 을 **객체(Object)** 처럼 다루는 **객체지향 프로그래밍(OOP)** 의 중요한 개념 중 하나다.  
이 함수는 **스마트 계약이 블록체인에 배포(deploy)** 될 때 **단 한 번 실행**된다.  

1. **초기 상태 설정**: 스마트 계약이 시작될 때 필요한 변수나 상태를 초기화  
2. **초기화 작업 수행**: 계약이 정상적으로 동작하도록 필요한 준비 작업을 처리

---

## **객체지향 프로그래밍과의 연결**

객체지향 프로그래밍에서는:

- **클래스(Class)**: 객체(Object)의 설계도  
- **생성자(Constructor)**: 객체를 생성할 때 초기 상태를 설정하는 함수  

이를 Solidity에 대입하면:

- **스마트 계약(Smart Contract)** = 클래스(Class)  
- **배포된 스마트 계약** = 클래스의 인스턴스(객체)

---

### **요약**  
생성자는 스마트 계약이 블록체인에 배포될 때 **한 번만 실행**되며,  
계약의 **초기 상태를 설정**하고, **필요한 초기화 작업**을 수행하는 함수.

---
## **구성 요소 설명**

### 1. **constructor 키워드**
- **`constructor`** 키워드는 함수가 생성자임을 나타낸다.  
- 생성자는 이름이 따로 없으며, **`constructor`** 키워드로만 선언

### 2. **매개변수 (Parameters)**
- 생성자는 **입력 값(매개변수)** 을 받을 수 있다.  
- 각 매개변수는 **타입** 과 함께 정의되며, 입력된 값을 활용해 상태 변수를 초기화한다.

### 3. **가시성 (Visibility)**
- 생성자의 접근 범위를 **`public`** 또는 **`internal`** 로 지정할 수 있다.  
  - **`public`**: 누구나 생성자를 호출할 수 있다.  
  - **`internal`**: 생성자가 내부적으로만 호출될 수 있다. 이 경우, 해당 계약은 **추상 계약(Abstract Contract)** 으로만 동작한다.  
  -> 추상 계약은 직접 배포될 수 없고, 다른 계약이 이를 상속하여 생성자를 호출해야 한다.

## 예시
```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.24;

contract MyContract {
    uint public value;
    address public owner;

    // 생성자
    constructor(uint _value) {
        value = _value;
        owner = msg.sender;
    }

    // 상태 변수 반환 함수
    function getValue() public view returns (uint) {
        return value;
    }

    function getOwner() public view returns (address) {
        return owner;
    }
}
```

### constructor 정의
```solidity
    constructor(uint _value) {
        value = _value;
        owner = msg.sender;
    }
```
매개변수로 _value 값을 받아 상태 변수 value와 owner를 각각 초기화한다.

=> deploy시에 `_value` 파라미터 값을 꼭 넣어줘야한다.