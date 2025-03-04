## 배열

>* 자료구조에서의 배열
>  * 동일한 크기의 메모리 공간이 빈틈없이 연속적으로 나열된 자료구조
>  * 밀집 배열
>* 자바스크립트의 배열
>  * 메모리 공간은 동일한 크기를 자기기 않아도 되며, 연속적으로 이어져 있지 않을 수도 있다.
>  * 희소 배열

> * 자바스크립트의 배열은 일반적인 배열의 동작을 흉내 낸 특수한 객체
> * 희소 배열은 length 와 배열 요소의 개수가 일치하지 않는다.
>   * 희소 배열의 length는 희소 배열의 실제 요소 개수보다 언제나 크다.


## 배열 생성

### 1) 배열 리터럴

```javascript
const arr = [1, 2, 3];
console.log(arr.length); 
```

### 2) Array 생성자 함수

```javascript
const arr = new Array(10)
console.log(arr); // [empty × 10]
console.log(arr.length); // 10
```

### 3) Array.of
```javascript
// 전달된 인수가 1개이고 숫자이더라도 인수를 요소로 갖는 배열을 생성한다.
Array.of(1); // -> [1]

Array.of(1, 2, 3); // -> [1, 2, 3]

Array.of('string'); // -> ['string']
```

### 4) Array.from
```javascript
// 유사 배열 객체를 변환하여 배열을 생성한다.
Array.from({ length: 2, 0: 'a', 1: 'b' }); // -> ['a', 'b']

// 이터러블을 변환하여 배열을 생성한다. 문자열은 이터러블이다.
Array.from('Hello'); // -> ['H', 'e', 'l', 'l', 'o']

// Array.from에 length만 존재하는 유사 배열 객체를 전달하면 undefined를 요소로 채운다.
Array.from({ length: 3 }); // -> [undefined, undefined, undefined]

// Array.from은 두 번째 인수로 전달한 콜백 함수의 반환값으로 구성된 배열을 반환한다.
Array.from({ length: 3 }, (_, i) => i); // -> [0, 1, 2]
```

## 배열 참조
```javascript
const arr = [1, 2];
// 인덱스가 0인 요소를 참조
console.log(arr[0]); // 1
// 인덱스가 1인 요소를 참조
console.log(arr[1]); // 2


const arr = [1, 2];

// 인덱스가 2인 요소를 참조. 배열 arr에는 인덱스가 2인 요소가 존재하지 않는다.
console.log(arr[2]); // undefined
```

## 배열 요소의 추가와 갱신
```javascript
const arr = [0];

// 배열 요소의 추가
arr[1] = 1;

console.log(arr); // [0, 1]
console.log(arr.length); // 2

arr[100] = 100;

console.log(arr); // [0, 1, empty × 98, 100]
console.log(arr.length); // 101


// 요소값의 갱신
arr[1] = 10;

console.log(arr); // [0, 10, empty × 98, 100]
```

## 배열 요소의 삭제

```javascript
const arr = [1, 2, 3];

// 배열 요소의 삭제
delete arr[1];
console.log(arr); // [1, empty, 3]

// length 프로퍼티에 영향을 주지 않는다. 즉, 희소 배열이 된다.
console.log(arr.length); // 3


const arr = [1, 2, 3];

// Array.prototype.splice(삭제를 시작할 인덱스, 삭제할 요소 수)
// arr[1]부터 1개의 요소를 제거
arr.splice(1, 1);
console.log(arr); // [1, 3]

// length 프로퍼티가 자동 갱신된다.
console.log(arr.length); // 2
```
