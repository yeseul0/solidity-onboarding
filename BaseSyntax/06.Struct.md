# Struct

`struct`는 Solidity에서 **사용자 정의 데이터 타입**을 만들기 위해 사용된다.

여러 개의 서로 다른 타입의 데이터를 하나의 단위로 묶어 관리할 수 있으며, 관련된 정보들을 그룹화해서 코드의 구조를 명확하게 만들 수 있다.

예를 들어, 사람에 대한 정보를 저장할 때 이름, 나이, 지갑 주소 등을 하나로 묶어 관리하고자 할 때 `struct`가 유용하게 사용된다.

![struct](../image/struct.png)

---

## **Struct의 기본 구조**

```solidity

// struct 정의
struct Person {
    string name;
    uint age;
    address wallet;
}
```

- 위 코드는 `Person`이라는 이름의 구조체를 정의한 예시이다.
- 이 구조체는 세 개의 필드(`name`, `age`, `wallet`)를 포함하고 있으며, 각각 문자열, 정수, 주소 타입으로 구성되어 있다.
- 구조체 안에 포함된 각 필드를 "멤버"라고 부르며, 서로 다른 타입의 데이터를 함께 저장할 수 있다.

---

## **Struct 접근하기**

구조체의 각 멤버에 접근하기 위해서는 **멤버 접근 연산자(.)**를 사용한다.

즉, 구조체 변수 뒤에 마침표(`.`)를 붙여 원하는 멤버에 접근할 수 있다.

예를 들어:

```solidity

Person memory user = Person("Alice", 30, msg.sender);
string memory username = user.name;
```

- 첫 번째 줄에서 `Person` 구조체 타입의 변수를 `user`로 선언하고, 이름, 나이, 지갑 주소를 초기값으로 설정한다.
- 두 번째 줄에서는 `user.name`을 통해 구조체 `user` 안에 있는 `name` 필드에 접근하고 있다.

이처럼 `struct`는 관련된 데이터를 하나로 묶고, 그 안의 각 필드에 명확하게 접근할 수 있는 구조를 제공한다.

## **예제 코드**

다음 코드는 Solidity에서 구조체를 사용하는 방법을 보여준다.

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.24;

contract Test {
    // 구조체 정의
    struct Book {
        string title;
        string author;
        uint book_id;
    }

    // Book 구조체 타입의 변수 선언
    Book book;

    // 구조체 인스턴스 설정 함수
    function setBook() public {
        book = Book('Learn Solidity', 'TP', 1);
    }

    // 구조체 멤버에 접근하여 반환하는 함수
    function getBookId() public view returns (uint) {
        return book.book_id;
    }

    function getBookAuthor() public view returns (string memory) { // ⬅️ memory 추가
        return book.author;
    }
    
    function getBookTitle() public view returns (string memory) { // ⬅️ memory 추가
        return book.title;
    }
}
```

이 코드는 `Book`이라는 구조체를 정의하고, 해당 구조체를 사용하는 방법을 보여주는 기본적인 예제이다.

하나의 책 정보를 구조체 형태로 묶어서 저장하고, 그 안의 개별 필드들에 접근하여 값을 가져오는 기능을 포함하고 있다.

---

### **구조체 정의 및 변수 선언**

```solidity

struct Book {
    string title;
    string author;
    uint book_id;
}
Book book;
```

- `Book`이라는 이름의 구조체를 정의하였다.
- 이 구조체는 책의 제목(`title`), 저자(`author`), 도서 ID(`book_id`) 세 가지 정보를 담고 있다.
- `Book book;`은 구조체 타입의 변수 `book`을 선언한 것으로, 하나의 책 정보를 저장할 수 있는 공간을 만든 것이다.

---

### **setBook 함수**

```solidity

function setBook() public {
    book = Book('Learn Solidity', 'TP', 1);
}
```

- 이 함수는 구조체에 값을 할당하는 역할을 한다.
- `Book(...)`은 구조체의 생성자처럼 작동하며, 구조체 각 필드에 값을 순서대로 할당한다.
- 이 함수가 실행되면 `book.title = "Learn Solidity"`, `book.author = "TP"`, `book.book_id = 1`이 된다.

---

### **getBookId 함수**

```solidity

function getBookId() public view returns (uint) {
    return book.book_id;
}
```

- 구조체의 `book_id` 필드 값을 반환하는 함수이다.
- 상태를 변경하지 않기 때문에 `view` 키워드를 사용하였다.

---

### **getBookAuthor 함수**

```solidity

function getBookAuthor() public view returns (string memory) {
    return book.author;
}

```

- 구조체의 `author` 필드 값을 반환한다.
- 문자열은 `memory` 키워드를 함께 사용해야 반환이 가능하다.

---

### **getBookTitle 함수**

```solidity

function getBookTitle() public view returns (string memory) {
    return book.title;
}
```

- 구조체의 `title` 필드 값을 반환하는 함수이다.
- 마찬가지로 문자열 반환을 위해 `memory` 키워드가 사용된다.

### 요약

- 이 예제는 `struct`를 정의하고 값을 설정한 뒤, 개별 멤버에 접근하여 값을 가져오는 구조를 보여준다.
- 구조체를 사용하면 서로 관련 있는 여러 데이터를 하나로 묶어 관리할 수 있다.
- `.`(점) 연산자를 통해 구조체 변수 내부의 개별 멤버에 접근할 수 있다.
- 구조체는 컨트랙트 내부 상태를 보다 **정리된 형태로 유지**할 수 있게 해주는 중요한 도구이다.

이 예제를 통해 `struct`의 정의, 할당, 접근 방식을 실습해볼 수 있다.