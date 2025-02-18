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