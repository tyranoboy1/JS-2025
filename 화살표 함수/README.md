## 화살표 함수

>* function 키워드 대신 화살표를 사용하여 기존의 함수정의 방식보다 간략하게 함수를 정의
>* 콜백 함수 내부에서 this가 전역 객체를 가리키는 문제를 해결하기 위한 대안으로 유용

### 함수 정의
 ```javascript
const multiply = (x, y) => x * y;
multiply(2, 3); // -> 6
```

### 매개변수 선언

 ```javascript
// 매개변수가 여러개 인 경우
const arrow = (x, y) => { ... };
```

 ```javascript
// 매개변수가 한 개인 경우
const arrow = x => { ... };
```

 ```javascript
// 매개변수가 없는 경우 소괄호 생략 x
const arrow = () => { ... };
```

### 함수 몸체 정의

 ```javascript
// concise body
const power = x => x ** 2;
power(2); // -> 4

// 위 표현은 다음과 동일하다.
// block body
const power = x => { return x ** 2; };
```

 ```javascript
const arrow = () => const x = 1; // SyntaxError: Unexpected token 'const'
// 위 표현은 다음과 같이 해석된다.
const arrow = () => { return const x = 1; };

const arrow = () => { const x = 1; };
```

 ```javascript
const create = (id, content) => ({ id, content });
create(1, 'JavaScript'); // -> {id: 1, content: "JavaScript"}

// 위 표현은 다음과 동일하다.
const create = (id, content) => { return { id, content }; };

// { id, content }를 함수 몸체 내의 쉼표 연산자문으로 해석한다.
const create = (id, content) => { id, content };
create(1, 'JavaScript'); // -> undefined
```


## 화살표 함수 vs 일반 함수

 ```javascript
const Foo = () => {};
// 화살표 함수는 생성자 함수로서 호출할 수 없다.
new Foo(); // TypeError: Foo is not a constructor
```
>* 화살표 함수는 인스턴스를 생성할 수 없는 non-constructor 이다.


 ```javascript
function normal(a, a) { return a + a; }
console.log(normal(1, 2)); // 4
```
>* 중복된 매개변수 이름을 선언할 수 없다.
>  * 일반 함수는 중복된 매개변수 이름을 선언해도 에러 발생 x

>* 화살표 함수는 함수 자체의 this, arguments, super, new.target 바인딩을 갖지 않는다.
>  * 화살표 함수 내부에서 this, arguments, super, new.target을 참조하면 스코프 체인을 통해 상위 스코프의 this, arguments, super, new.target을 참조


## 화살표 함수에서의 this

 ```javascript
class Prefixer {
    constructor(prefix) {
        this.prefix = prefix;
    }

    add(arr) {
        return arr.map(item => this.prefix + item);
    }
}

const prefixer = new Prefixer('-webkit-');
console.log(prefixer.add(['transition', 'user-select']));
// ['-webkit-transition', '-webkit-user-select']
```

> * ***화살표 함수는 함수 자체의 this 바인딩을 갖지 않는다. 따라서 함수 내부에서 this를 참조하면 상위 스코프의 this를 그대로 참조***
> * 이를 ***lexical this*** 라고 한다.
