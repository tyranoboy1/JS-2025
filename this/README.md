## this

> * 자신이 속한 객체 또는 자신이 생성할 인스턴스를 가리키는 자기 참조 변수
> * this를 통해 자신이 속한 객체 또는 자신이 생성할 인스턴스의 프로퍼티나 메서드를 참조

>* ***this가 가리키는 값, this 바인딩은 함수 호출 방식에 의해 동적으로 결정된다.***

```javascript
// this는 어디서든지 참조 가능하다.
// 전역에서 this는 전역 객체 window를 가리킨다.
console.log(this); // window

function square(number) {
// 일반 함수 내부에서 this는 전역 객체 window를 가리킨다.
    console.log(this); // window
    return number * number;
}
square(2);

const person = {
    name: 'Lee',
    getName() {
// 메서드 내부에서 this는 메서드를 호출한 객체를 가리킨다.
        console.log(this); // {name: "Lee", getName: ƒ}
        return this.name;
    }
};
console.log(person.getName()); // Lee

function Person(name) {
    this.name = name;
// 생성자 함수 내부에서 this는 생성자 함수가 생성할 인스턴스를 가리킨다.
    console.log(this); // Person {name: "Lee"}
}

const me = new Person('Lee');
```

## 함수 호출 방식

### 일반 함수 호출

>* this -> 전역 객체
>* ***화살표 함수의 this는 상위 스코프의 this를 가짐***
### 메서드 호출

>* this -> 메서드를 호출한 객체


### 생성자 함수 호출
>* this -> 생성자 함수가 생성할 인스턴스

### apply , call, bind에 의한 간접 호출
>* 메서드에 첫번째 인수로 전달한 객체