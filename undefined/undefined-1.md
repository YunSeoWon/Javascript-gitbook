# 제어구문

### if - else if - else

어느 문법이나 거의 국룰.. 

```javascript
if (condition) {
    code
} else if (condition2) {
    code
} 
 ... 
} else {
    code
}
```

블록안에 명령어가 한 줄이면 중괄호를 생략할 수 있다. \(비추\)

```javascript
var x = 1
if (x > 10)
    console.log('x is grater than 10')
else
    console.log('x is less than or equal 10')
```



### switch

이것도 다른 언어와 비

```javascript
var beer = 'guinness'

switch (beer) {
  case 'guinness':
  console.log('made in Ireland');
  break;
  case 'heineken':
  console.log('made in Netherlands');
  break;
  case 'kozel':
  console.log('made in Czech');
  break;
  case 'terra':
  console.log('made in Korea');
  break;
  default:
  console.log("I don't know");
}

 // made in Ireland 
```

* 걸린 case에서 break를 만날 때 까지 switch 명령어가 작동한다.
* switch 식과 case 값은 === 연산자로 비교한다.



### while, do ... while

이것도 다른 언어와 비슷

```javascript
while(condition) {
    loop
}

do {
    loop
} while(condition);
```

### for

이것도 다른 언어와 비슷

```javascript
for(var i = 0; i < 10; i++) {
    console.log(i);
}
```

### for ... in

for ... in은 배열은 인덱스, 객체는 프로퍼티 명이 key로 들어간다.

```javascript
var ary = [1, 2, 3];

for (var key in ary) {
    console.log(ary[key]);
}
```

```javascript
var data = { kakao: 169500, naver: 423500, ncsoft: 825000 };
for (var key in data) {
    console.log(key + "=" + data[key]);
}
```

### for ... of

for ... in은 key\(index\)를 순회하지만 for ... of는 값을 순회한다. \(객체는 불가능 not iterable이라서\)

```javascript
var ary = [1, 2, 3]

for (var element of ary) {
    console.log(element)
}
```



### break, continue도 있다.



### 예외처리는 try - catch - finally

```javascript
try {
    code
} catch (e) {
    code
} finally {
    code    
}
```

* 예외 처리는 오버헤드가 커서 루프내에서는 피해야 한다.

