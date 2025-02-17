## 객체

```
* 객체는 프로퍼티와 메서드로 구성된 집합체
프로퍼티 - 객체의 상태를 나타내는 값(data), 키와 값으로 구성된다.
메서드 - 프로퍼티를 참조하고 조작할 수 있는 동작

* 식별자 네이밍 규칙을 따르지 않는 이름에는 반드시 따옴표를 사용해야 한다.
```


```javascript
var counter = {
    num: 0, // 프로퍼티
    increase: function () {  // 메서드
        this.num++
    }
}
```
## 프로퍼티 접근
```
* 마침표 프로퍼티 접근 연산자(.)를 사용하는 마침표 표기법
* 대괄호 프로퍼티 접근 연산자([...])를 사용하는 대괄호 표기법
* 객체에 존재하지 않는 프로퍼티에 접근하면 undefined를 반환
```

```javascript
var person = {
    name: 'Lee'
}

// 마침표 표기법
console.log(person.name)

// 대괄호 표기법
console.log(person['name'])

// undefined 반환
console.log(person.age)
```

## 원시값과 객체의 비교
```
* 원시값은 값이 복사되어 전달 -> 값에 의한 전달(변경이 불가능한 값)
* 참조값은 참조값이 복사되어 전달 -> 참조에 의한 전달(변경이 가능한 값)
```

## 불변성
```
* 원시값은 변경이 불가능하기 때문에 값을 재할당하면 새로운 메모리 공간 확보, 재할당한 값 저장후, 변수가 참조하는 메모리 공간 주소 변경하는 특징
* 불변성을 갖는 원시 값을 할당한 변수는 재할당 이외에 변수 값을 변경할 수 있는 방법이 없다.
```

```javascript
var score = 80;

// copy 변수에는 score 변수의 값 80이 복사되어 할당된다.
var copy = score;

console.log(score, copy);    // 80  80
console.log(score === copy); // true

// score 변수와 copy 변수의 값은 다른 메모리 공간에 저장된 별개의 값이다.
// 따라서 score 변수의 값을 변경해도 copy 변수의 값에는 어떠한 영향도 주지 않는다.
score = 100;

console.log(score, copy);    // 100  80
console.log(score === copy); // false
```

```
* 값의 의한 전달 => 값을 전달하는 것이 아닌 메모리 주소를 전달 
// 단 전달된 메모리 주소를 통해 메모리 공간에 접근하면 값을 참조할 수 있다. 
* 두 변수의 원시 값은 서로 다른 메모리 공간에 저장된 별개의 값이 되어 값을 변경하더라도 서로 간섭할 수 없다.
```

## 얕은 복사와 깊은 복사

```
* 객체를 프로퍼티 값으로 갖는 객체의 경우 얕은 복사는 한단계만 복사, 깊은 복사는 객체의 중첨되어있는 객체 까지 모두 복사
```


```javascript
const o = { x: { y: 1 } };

// 얕은 복사
const c1 = { ...o }; // 35장 "스프레드 문법" 참고
console.log(c1 === o); // false
console.log(c1.x === o.x); // true

// lodash의 cloneDeep을 사용한 깊은 복사
// "npm install lodash"로 lodash를 설치한 후, Node.js 환경에서 실행
const _ = require('lodash');
// 깊은 복사
const c2 = _.cloneDeep(o);
console.log(c2 === o); // false
console.log(c2.x === o.x); // false
```