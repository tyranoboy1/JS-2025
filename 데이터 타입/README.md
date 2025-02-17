## 데이터 타입

```
* 원시 타입 - 숫자, 문자열, 불리언, undefined, null, 심벌(변경 불가능한 값)
* 객체 타입 - 객체, 함수, 배열 ...(변경 가능한 값)
```

## undefined
```javascript
let a;
console.log(a); // undefined

function test() {}
console.log(test()); // undefined

const obj = {};
console.log(obj.prop) // undefined
/** 값이 할당되지 않음 */
/** 변수가 선언되었지만 값이 없는 상태 */
```


## null
```javascript
let b = null;
console.log(b); // null

const user = {
    name: "test",
    age: null, 
};

console.log(user.age); // null
/** 값이 의도적으로 비어 있음 */
/** 명시적으로 빈값을 의미 */
```

```
* JavaScript의 변수는 선언이 아닌 할당에 의해 타입이 결정(타입추론), 재할당에 의해 변수의 타입은 언제든지 동적으로 변할 수 있다.
```


```
* typeof 연산자 => null은 null이 아닌 object 반환(Javascript 버그), 일치연산자(===) 사용하여 확인
```




