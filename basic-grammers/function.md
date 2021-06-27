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





