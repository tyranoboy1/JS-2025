## 스코프

> * 모든 식별자가 자신이 선언된 위치에 의해 다른 코드가 식별자 자신을 참조할 수 있는 유효 범위

```javascript
var x = 'global x';
var y = 'global y'


function outer() {
    var z = "outer`s local z"
    
    console.log(x) // global x
    console.log(y) // global y
    console.log(z) // outer`s local z
    
    function inner() {
        var x = "inner`s local x"

        console.log(x) // inner`s local x
        console.log(y) // global y
        console.log(z) // outer`s local z
    }
    
    inner()
}
outer()
console.log(x) // global x
console.log(y) // Refernce Error z is not defined
```

## 지역과 지역 스코프

>* 지역 -> 함수 몸체 내부
>* 지역변수는 자신의 지역 스코프와 하위 지역 스코프에서 유효하다.


## 스코프 체인

>* 스코프가 함수의 중첩에 의해 계층적 구조로 연결된 것
>* 변수를 참조할 때 변수를 참조하는 코드의 스코프에서 시작하여 상위 스코프 방향으로 이동하여 선언된 변수를 검색


## 블록, 함수  레벨 스코프
> * 블록 레벨 스코프 => 함수, 모든 코드 블록은 지역 스코프를 만든다.
> * 함수 레벨 스코프 => var 변수는 오로지 함수의 코드 블록만을 지역 스코프로 인정


```javascript
var i = 10;

// for 문에서 선언한 i는 전역 변수다. 이미 선언된 전역 변수 i가 있으므로 중복 선언된다.
for (var i = 0; i < 5; i++) {
    console.log(i); // 0 1 2 3 4
}

// 의도치 않게 변수의 값이 변경되었다.
console.log(i); // 5
```


## 렉시컬 스코프
```javascript
var x = 1;

function foo() {
    var x = 10;
    bar();
}

function bar() {
    console.log(x);
}

foo(); // ?
bar(); // ?
```

> * ***함수를 어디서 호출했는지가 아니라 함수를 어디서 정의 했는지에 따라 상위 스코프를 결정한다.***
> 
> 
> * ***함수가 호출된 위치는 상위 스코프 결정에 어떠한 영향도 주지 않는다.***
>   * 함수의 상위 스코프는 언제나 자신이 정의된 스코프다.
> 
> 
> * ***함수의 상위 스코프는 함수 정의가 실행될 때 정적으로 결정***
> 
> 
> * ***함수 정의(함수 선언문 또는 함수 표현식)가 실행되어 생성된 함수 객체는 이렇게 결정된 상위 스코프를 기억한다.***
>   * 함수가 호출될 때마다 함수의 상위 스코프를 참조할 필요가 있기 때문에


## 지역 변수
```javascript
function foo() {
    var x = 'local';
    console.log(x); // local
    return x;
}

foo();
console.log(x); // ReferenceError: x is not defined
```

> * 지역 변수의 생명 주기는 함수의 생명 주기와 일치
> * 전역 변수의 생명 주기는 전역 객체의 생명 주기와 일치


## 호이스팅

```javascript
var x = 'global';

function foo() {
    console.log(x); // ①
    var x = 'local';
}

foo();
console.log(x); // global
```

> * 스코프를 단위로 동작
> * 변수 선언이 스코프의 선두로 끌어 올려진 것처럼 동작하는 자바스크립트 고유 특징


## 전역 변수 문제점

> * 모든 코드가 전역 변수를 참조하고 변경할 수 있는 암묵적 결합을 허용
> * 생명 주기가 길어 메모리 리소스 낭비
> * 스코프 체인 상 종점에 위치 => 검색 속도가 가장 느리다.
> * 파일이 분리되어도 하나의 전역 스코프를 공유하는 => 네임 스페이스 오염


## 전역 변수 억제

> * 변수의 스코프는 좁을수록 좋다 => 지역 변수 사용
> * 모든 코드를 즉시 실행 함수로 감싸면 모든 변수는 즉시 실행 함수의 지역 변수
> * 네임 스페이스 객체 => 담당할 객체를 생성하고 전역 변수로 사용하고 싶은 요소를 프로퍼티로 추가



## let, const


> * 이름이 같은 변수의 중복 선언 불가능
> * 모든 코드 블록을 지역 스코프로 인정하는 블록 레벨 스코프를 따른다.

### let
```javascript
let foo = 1; // 전역 변수

{
    let foo = 2; // 지역 변수
    let bar = 3; // 지역 변수
}

console.log(foo); // 1
console.log(bar); // ReferenceError: bar is not defined
```

> * ***let 변수는 선언단계와 초기화 단계가 분리되어 진행된다.***
> * ***스코프의 시작 지점부터 초기화 시작 지점까지 변수를 참조할 수 없는 구간을 TDZ라고 부른다***
> * ***모든 선언은 호이스팅을 하고 let도 호이스팅을 하지만 발생하지 않는 것처럼 동작한다.***

```javascript
let foo = 1; // 전역 변수

{
    console.log(foo); // ReferenceError: Cannot access 'foo' before initialization
    let foo = 2; // 지역 변수
}
```

### const
 
 ```javascript
{
    // 변수 호이스팅이 발생하지 않는 것처럼 동작한다
    console.log(foo); // ReferenceError: Cannot access 'foo' before initialization
    const foo = 1;
    console.log(foo); // 1
}

// 블록 레벨 스코프를 갖는다.
console.log(foo); // ReferenceError: foo is not defined
```

 ```javascript
// 재할당 금지
const foo = 1;
foo = 2; // TypeError: Assignment to constant variable.


// 재할당 금지 => 불변을 의미하는 것은 X
const person = {
    name: 'Lee'
};

// 객체는 변경 가능한 값이다. 따라서 재할당없이 변경이 가능하다.
person.name = 'Kim';

console.log(person); // {name: "Kim"}
```
> * ***반드시 선언과 동시에 초기화해야된다.***
> * ***모든 선언은 호이스팅을 하고 const도 호이스팅을 하지만 발생하지 않는 것처럼 동작한다.***
> * ***재할당이 금지된 상수***
> * ***const 변수에 원시값을 할당한 경우 값을 변경할 수 없다***
>   * 하지만 객체를 할당한 경우 값을 변경할 수 있다.