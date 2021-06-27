# 함수

## 함수 정의

주어진 입력에 근거하여 어떤 처리를 실시한 뒤 그 결과를 돌려주는 구조를 함수라고 한다. 

#### function 명령어로 정의하기

```javascript
function func(p1, ...) {
    ...
    return value;
}
```

* 반환값이 없을 때는 return을 생략해도 되는데 이 때는 자동으로 undefined를 리턴한다.
* return을 도중에 개행하지 않는다.

#### Function 생성자로 정의하기

```javascript
var func = new Function(p1, ..., body);
var func = Function(p1, ..., body);
```

* new 연산자를 생략해도 된다.
* Function 생성자는 인수나 함수 본체를 문자열로써 정의할 수 있다. 그래서 스크립트상에서 문자열을 연결하고 인수/함수 본체를 동적으로 생성할 수도 있다. 

```javascript
var add = new Function('a', 'b', 'return a + b;');
console.log(add(1, 2)); // 3
```

#### 함수 리터럴 표현으로 정의하기

```javascript
var func = function(p1, ...) {
    ...
    return value;
}
```

* 함수 리터럴로 정의하면 함수 리터럴을 변수에 대입하고, 어떤 함수에 인수로서 건넬 수 있고, 반환값으로 함수를 건네주는 것이 가능하다.
* 함수 리터럴을 선언한 시점에서는 \(변수에 대입하기 전\) 이름을 가지지 않기 때문에 익명함수 또는 무명함수라고도 불린다.

#### 애로우 함수로 정의하기

```javascript
var func = (p1, ...) => {
    ...
    return value; 
};

var func = (p1, ...) => express;
var func = p1 => express;
var func = () => express;
```

* 함수 바디가 한 줄로 끝나는 경우, 중괄호를 생략할 수 있다.
* 함수 인수가 하나인 경우, 소괄호를 생략할 수 있다.
* 대신 인수가 없는 경우는 소괄호를 생략할 수 없다.

### function 명령과 Function 생성자의 차이

* function 명령에 의해 생성된 함수는 정적인 구조를 선언한다. 그래서 함수 실행이 함수 정의보다 먼저 와도 에러가나지 않는다.
* Function 생성자에 의해 생성된 함수는 생성자 실행 시 함수를 정의하게 되므로 함수 실행이 함수 정의보다 먼저 오면 에러가 발생한다.



### 인수 \[ES2015이전\]

#### Javascript는 인수의 수를 체크하지 않는다.

```javascript
function showParameters(p1, p2, p3) {
  console.log('p1, p2, p3: ' + p1 + ', ' + p2 + ', ' + p3);
}

showParameters(1, 2, 3);
showParameters(1, 2);
showParameters(1, 2, 3, 4, 5);
```

* javascript에서는 인수의 수를 체크하지 않고 순서대로 가인수와 매핑한다.
* 전달받은 파라미터의 수가 가인수 수보다 작을 경우 매핑되지 않는 가인수는 undefined로 된다.
* 전달받은 파라미터의 수가 가인수 수보다 클 경우 매핑되지 않는 파라미터는 무시되지는 않는다.
* 모든 전달받은 파라미터들은 arguments 객체에 저장된다.



#### 인수의 default값을 설정할 수 있는 구문은 없다.

default값을 설정할 수 있는 구문이 없기 때문에 조건문으로 처리해야 한다.

```javascript
function func(p1, p2) {
    if (p1 == undefined) { p1 = 1; }
    if (p2 == undefined) { p2 = 1; }
    ...
}
```



#### 가변길이 인수 사용하기

기본적으로 javascript의 함수는 가변길이 인수를 받는다. \(정의된 인수의 수보다 더 많은 파라미터를 받을 수 있는걸 확인하였다.\) 가변길이 인수는 arguments 변수에 저장되는데 배열처럼 사용하면 된다.

```javascript
function sumAll() {
  let sum = 0

  for (let i = 0; i < arguments.length; i++) {
    sum += arguments[i];
  }

  return sum;
}

console.log(sumAll(1, 10, 100, 1000, 10000)); // 11111
```



### 인수 \[ES2015\]

#### 인수의 default값을 선언할 수 있다.

```javascript
function func(p1 = 1, p2 = 2) {
    ...
}
```

* 디폴트 값이 적용되는 경우는 인수가 명시적으로 건네지지 않았을 경우 뿐이다.
* 디폴트 값을 갖는 가인수는 인수 리스트의 끝으로 가는 것이 좋다.

```javascript
function getTriangle(base = 1, height) {
    return base * height / 2;
}

console.log(getTriangle(10)) // NaN, height = undefined
```

* 여기서 10은 base에 할당되기 때문에 height는 undefined가 된다.
* 그래서 디폴트 값을 갖는 가인수는 인수의 끝으로 가는 것이 좋다.

#### 가변길이 인수 명시하기

ES2015에서는 가인수 앞에 ...을 부여하면 가변길이 인수가 된다. 의미 없는 이름인 arguments 대신 의미있는 이름을 부여할 수 있다.

```javascript
function sumAll(...nums) {
  let sum = 0;

  for (let i = 0; i < nums.length; i++) sum += nums[i];

  return sum;
}

console.log(sumAll(1,2,3,4,5)); // 15

let ary = [1,2,3,4,5]
console.log(sumAll(...ary));
```

* 배열 앞에 ... 연산자를 사용하면 가변인수 파라미터로 전달할 수 있다.

#### 인수 명명해서 전달하기

```javascript
function getTriangle({base = 1, height = 1}) {
  return base * height / 2;
}

console.log(getTriangle({ base: 5, height: 10 }));
```

### 복수의 반환값을 개별 변수에 대입하기

```javascript
function getMinMax(...nums) {
  return [Math.max(...nums), Math.min(...nums)];
}

let [min, max] = getMinMax(1, 2, 3, 4, 5);

console.log(min);
console.log(max);
```



### 고차함수

함수를 인수로 받거나 리턴값으로 돌려주거나 할 수 있는데 이런 방식으로 취급하는 함수를 **고차함수** 라고 한다.

```javascript
function action(array, f) {
  var result = f(array)
  console.log(result)
}

let ary = [1,2,3,4,5]
action(ary, array => Math.min(...array));
```

