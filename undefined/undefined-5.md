# 스코프

자바스크립트에서의 스코프는 총 세가지가 있다. 

* Golbal Scope: 스크립트 전체에서 참조할 수 있는 스코프
* Local Scope: 정의된 함수 안에서만 참조할 수 있는 스코프
* Block Scope: 블록 내에서만 참조할 수 있는 스코프 \[ES2015 이후\]

### var 명령어

변수 선언에서 var 명령어는 Local Scope에서 변수를 정의할 때 사용한다. var를 생략하면 Global Scope에서 변수를 정의한다.

### 호이스팅

호이스팅\(Hoisting\)이란 함수 안에 있는 선언된 변수들을 모두 끌어올려서 해당 함수의 Local Scope에 미리 변수를 정의하는 것을 말한다.

```javascript
var scope = 'Global Variable';

function getValue() {
    // var scope; caused by hoisting
    console.log(scope);
    var scope = 'Local Variable';
    return scope;
}

console.log(getValue()); // LocalVariable
console.log(scope); // Global Variable
```

* function 내에서 정의되는 변수 scope는 사실상 함수 생성 시 맨 먼저 정의된다. \(console.log를 찍기전에 정의\) 그래서 scope는 undefined로 먼저 정의된다.
* 이러한 성질 때문에 로컬 변수는 함수의 선두에 선언하는 것이 좋다.

### 가인수의 스코프

가인수는 로컬 변수로 처리된다. 대신 가인수가 기본형이냐 참조형이냐에 따라 예상되는 시나리오와 다를 수 있다는 점을 염두하자.

#### 기본형 가인수

```javascript
var value = 10

function decrement(value) {
  value--;
  return value;
}

console.log(decrement(value)); // 9
console.log(value); // 10
```

* 가인수인 함수 파라미터 value는 로컬 변수기 때문에 가인수 value를 조작해도 함수 밖에 있는 value는 변하지 않는다.



#### 참조형 가인수

```javascript
var value = [1,2,3,4]

function decrement(value) {
  value.pop();
  return value;
}

console.log(decrement(value)); // [1, 2, 3]
console.log(value); // [1, 2, 3]
```

* 참조형 변수는 값 자체를 가지고 있는 것이 아닌 주소값을 가지고 있는 변수를 의미한다.
* 그래서 실제 값은 참조형 변수가 가지고 있는 주소에 저장되어있다.
* 가인수 함수 파라미터 value를 참조형으로 받는다면 주소값을 복사해서 가져오기 때문에 함수 밖에서 함수로 전달한 변수의 값에 영향이 있을 수 있다.



## 블록 스코프

블록 스코프는 블록 단위의 스코프로 ES2015이전에는 없던 스코프이다.

### ES2015 이전은 블록 스코프가 없다.

```javascript
if (true) {
  var i = 5;
}
console.log(i); //
```

* if 블록 내에 변수를 선언하고 블록 밖에서 호출을 해도 올바르게 동작한다.
* 블록 스코프를 지원하는 다른 언어에서는 동작이 안되지만 javascript에서는 동작한다.

### 블록 스코프 처럼 사용하기 - 즉시함수

로컬 스코프가 함수에 의해 결정되는 스코프기 때문에 함수를 스코프의 틀로서 이용하면 블록 스코프처럼 사용할 수 있다. 함수를 선언하고 바로 호출하여서 블록 스코프처럼 사용할 수 있는데 이러한 기술을 **즉시함수**라고 부른다.

```javascript
(function() {
    var i = 5;
})()
  
console.log(i); // error: Uncaught ReferenceError: i is not defined
```

### ES2015 - let 명령어로 블록스코프에서 변수 선언하기

ES2015에서 추가된 let 명령어는 블록스코프에 대응하는 변수를 선언한다.

```javascript
if (true) {
  let i = 5;
}

console.log(i); // error: Uncaught ReferenceError: i is not defined
```

* 블록스코프에서 변수를 선언할 수 있기 때문에 굳이 즉시함수를 사용할 필요는 없다.

#### switch 블록에서의 let 선언은 주의가 필요하다.

switch는 조건 분기 전체로서 하나의 블록이기 때문에 case 구문의 단위로 let을 선언하는 경우에 중복 선언 에러가 발생한다. 이러한 경우에 switch 블록 밖에서 변수를 선언하자.

```javascript
let x = 1;

// 이렇게 하지말
switch(x) {
  case 0:
  let value = 'x:0';
  break;
  case 1:
  let value = 'x:1'; // 빨간줄 발
  break;
  default:
  let value = 'other'
}

// 이렇게 하자.
let value;
switch(x) {
  case 0:
  let value = 'x:0';
  break;
  case 1:
  let value = 'x:1'; // 빨간줄 발
  break;
  default:
  let value = 'other'
}
```

###  

