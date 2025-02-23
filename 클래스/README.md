## 클래스

> * 프로토타입 기반의 객체지향 언어
> * 프로토 타입 객체지향 언어 => 클래스가 필요 없는 객체지향 프로그래밍 언어

## 클래스 정의

 ```javascript
// 클래스 선언문
class Person {}

// 익명 클래스 표현식
const Person = class {};

// 기명 클래스 표현식
const Person = class MyClass {};
```

> * 클래스 선언문도 변수 선언, 함수 정의와 마찬가지로 호이스팅이 일어난다.
>   * let, const로 선언한 변수처럼 호이스팅이 일어난다.

## 인스턴스 생성

```javascript
// 클래스 선언문
class Person {}

 ```javascript
class Person {}

// 인스턴스 생성
const me = new Person();
console.log(me); // Person {}
```

>* 클래스는 인스턴스를 생성하는 것이 유일한 존재 이유이므로 반드시 new 연산자와 함께 호출
>* 클래스 표현식에서 사용한 클래스 이름은 외부 코드에서 접근 불가능

## 메서드

### constructor
>* 인스턴스를 생성하고 초기화하기 위한 메서드
>* 이름 변경 불가능
>* 생략 가능 => 암묵적으로 빈 constructor 정의


```javascript
// 클래스
class Person {
    // 생성자
    constructor(name) {
        // 인스턴스 생성 및 초기화
        this.name = name;
    }
}

// 생성자 함수
function Person(name) {
    // 인스턴스 생성 및 초기화
    this.name = name;
}
```

```javascript
class Person {
    constructor(name) {
        this.name = name;

        // 명시적으로 객체를 반환하면 암묵적인 this 반환이 무시된다.
        return {};
    }
}

// constructor에서 명시적으로 반환한 빈 객체가 반환된다.
const me = new Person('Lee');
console.log(me); // {}
```

### 프로토타입 메서드

#### 1) 생성자 함수를 사용하여 인스턴스를 생성하는 경우 명시적으로 프로토타입 메서드를 추가

```javascript
// 생성자 함수
function Person(name) {
    this.name = name;
}

// 프로토타입 메서드
Person.prototype.sayHi = function () {
    console.log(`Hi! My name is ${this.name}`);
};

const me = new Person('Lee');
me.sayHi(); // Hi! My name is Lee
```
#### 2) 클래스 몸체에서 정의한 메서드

```javascript
class Person {
    // 생성자
    constructor(name) {
        // 인스턴스 생성 및 초기화
        this.name = name;
    }

    // 프로토타입 메서드
    sayHi() {
        console.log(`Hi! My name is ${this.name}`);
    }
}

const me = new Person('Lee');
me.sayHi(); // Hi! My name is Lee
```

### 정적 메서드

>* 인스턴스를 생성하지 않아도 호출 할 수 있는 메서드

```javascript
class Person {
    // 생성자
    constructor(name) {
        // 인스턴스 생성 및 초기화
        this.name = name;
    }

    // 정적 메서드
    static sayHi() {
        console.log('Hi!');
    }
}
```

### 클래스 인스턴스의 생성 과정

1. 인스턴스 생성과 this 바인딩
2. 인스턴스 초기화
3. 인스턴스 반환

## 프로퍼티

### 인스턴스 프로퍼티
> * constructor 내부에서 정의

```javascript
class Person {
    constructor(name) {
        // 인스턴스 프로퍼티
        this.name = name;
    }
}

const me = new Person('Lee');
console.log(me); // Person {name: "Lee"}
```

### 접근자 프로퍼티
>* 다른 데이터의 값을 읽거나 저장할 때 사용하는 접근자 함수로 구성된 프로퍼티
>* getter 함수와 setter 함수로 구성
```javascript
const person = {
    // 데이터 프로퍼티
    firstName: 'Ungmo',
    lastName: 'Lee',

    // fullName은 접근자 함수로 구성된 접근자 프로퍼티다.
    // getter 함수
    get fullName() {
        return `${this.firstName} ${this.lastName}`;
    },
    // setter 함수
    set fullName(name) {
        // 배열 디스트럭처링 할당: "36.1. 배열 디스트럭처링 할당" 참고
        [this.firstName, this.lastName] = name.split(' ');
    }
};
```

### 클래스 필드 정의 제안
>* 클래스가 생성할 인스턴스의 프로퍼티를 가리키는 용어

```javascript
class Person {
// 클래스 필드에 문자열을 할당
    name = 'Lee';

// 클래스 필드에 함수를 할당
    getName = function () {
        return this.name;
    }
// 화살표 함수로 정의할 수도 있다.
// getName = () => this.name;
}

const me = new Person();
console.log(me); // Person {name: "Lee", getName: ƒ}
console.log(me.getName()); // Lee
```



