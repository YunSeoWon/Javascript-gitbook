# 연산자

## 연산자

모든 언어에서 사용되는 연산자 말고 나머지 연산만 정리하였다.

### 분할대입 \[ES2015\]

분할 대입은 배열이나 객체를 분해해서 여러 변수에 한방에 대입하는 것을 말한다.

```javascript
let [x1, x2, x3] = [1, 2, 3];

console.log(x1) // 1
```

객체의 경우 배열과 다르게 이름으로 프로퍼티를 개별 변수로 분해한다.

```javascript
let person = { name: 'beer1', age: 27, gender: 'male' };
let { age, name, money } = person

console.log(name); // 'beer1'
console.log(money); // undefined
```

### 등가 연산자\(==\)와 동치 연산자\(===\)

== 연산자는 피연산자의 값이 같은지 여부를 나타낸다. 데이터형을 의식하지 않고 코딩이 가능 \(데이터형을 어느 한쪽에 맞춘 후 값 일치 여부 판단\)

```javascript
console.log('3.14E2' == 314); // true
console.log('0x10' == 16); // true
console.log('1' == 1); // true
```

=== 연산자는 피연산자의 데이터형이 일치하지 않으면 false를 반환한다.

```javascript
console.log('3.14E2' === 314); // false
console.log('0x10' === 16); // false
console.log('1' === 1); // false
```

### delete 연산자

delete 연산자는 피연산자에 지정한 변수나 배열요소, 객체의 프로퍼티를 삭제하는 연산자이다. 삭제에 성공하면 true, 실패하면 false를 반환한다.

```javascript
let array = ['heineken', 'kozel', 'guinness']
console.log(array) // ["heineken", "kozel", "guinness"]
console.log(delete array[0]) // true
console.log(array) // [undefined, "kozel", "guinness"]

let p = { name: 'beer1', age: 27, gender: 'male' };
console.log(p); // { name: 'beer1', age: 27, gender: 'male' }
console.log(delete p.name); // true
console.log(p); // { age: 27, gender: 'male' };
console.log(delete p.name2); // true
```

* 객체에 없는 필드를 지워도 true가 반환된다.

### typeof 연산자

typeof 연산자는 피연산자의 데이터형을 나타내는 문자열을 반환한다.

```javascript
var num = 1;
var str = 'beer1';
var flag = true;
var ary = ['heineken', 'kozel', 'guinness'];
var obj = { name: 'beer1', age: 27, gender: 'male' };

console.log(typeof num); // number
console.log(typeof str); // string
console.log(typeof flag); // boolean
console.log(typeof ary); // object
console.log(typeof obj); // object
```

* 배열과 객체 모두 object이다.

