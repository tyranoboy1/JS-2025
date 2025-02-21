## 클로저 

> * 함수와 그 함수가 선언된 렉시컬 환경과의 조합이다.

## 렉시컬 스코프  
> * 자바스크립트 엔진은 함수를 어디서 호출했는지가 아니라 함수를 어디에 정의했는지에 따라 상위 스코프를 결정한다.
> * 렉시컬 환경의 외부 렉시컬 환경에 대한 참조에 저장할 참조값, 즉 상위 스코프에 대한 참조는 함수 정의가 평가되는 시점에 함수가 정의된 환경에 의해 결정
>

 ```javascript
const x = 1;

// ①
function outer() {
    const x = 10;
    const inner = function () { console.log(x); }; // ②
    return inner;
}

// outer 함수를 호출하면 중첩 함수 inner를 반환한다.
// 그리고 outer 함수의 실행 컨텍스트는 실행 컨텍스트 스택에서 팝되어 제거된다.
const innerFunc = outer(); // ③
innerFunc(); // ④ 10
```

> * ***외부 함수보다 중첩 함수가 더 오래 유지되는 경우 중첩 함수는 이미 생명 주기가 종료한 외부 함수의 변수를 참조할 수 있다.***
 

> * 클로저는 중첩 함수가 상위 스코프의 식별자를 참조하고 있고 중첩 함수가 외부 함수보다 더 오래 유지되는 경우에 한정


## 클로저의 활용

> * 상태를 안전하게 변경하고 유지하기 위해 사용
>   * 안전하게 은닉하고, 특정 함수에게만 상태 변경 허용


 ```javascript
// 카운트 상태 변경 함수
const increase = (function () {
    // 카운트 상태 변수
    let num = 0;

    // 클로저
    return function () {
        // 카운트 상태를 1만큼 증가 시킨다.
        return ++num;
    };
}());

console.log(increase()); // 1
console.log(increase()); // 2
console.log(increase()); // 3
```

### 캡슐화와 정보 은닉

> * 캡슐화는 객체의 상태를 나타내는 프로퍼티와 프로퍼티를 참조하고 조작할 수 있는 동작을 하나로 묶는 것
> * 객체의 특정 프로퍼티나 메서드를 감출 목적으로 사용하는데 이를 정보 은닉이라고 한다

 ```javascript
const Person = (function () {
    let _age = 0; // private

// 생성자 함수
    function Person(name, age) {
        this.name = name; // public
        _age = age;
    }

// 프로토타입 메서드
    Person.prototype.sayHi = function () {
        console.log(`Hi! My name is ${this.name}. I am ${_age}.`);
    };

// 생성자 함수를 반환
    return Person;
}());

const me = new Person('Lee', 20);
me.sayHi(); // Hi! My name is Lee. I am 20.
console.log(me.name); // Lee
console.log(me._age); // undefined

const you = new Person('Kim', 30);
you.sayHi(); // Hi! My name is Kim. I am 30.
console.log(you.name); // Kim
console.log(you._age); // undefined
```


## 내용 정리 및 생각 요약

> * 클로저는 자신이 선언 되었던 환경의 스코프를 기억하고 유지, 외부 함수가 종료된 후에도 내부 함수가 그 변수를 계속 참조할 수 있는 현상




