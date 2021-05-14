# JavaScript Study 04
## 4. 표현식과 연산자
### 4.4 프로퍼티 접근 표현식
> 표현식 . 표현식  
> 표현식[표현식]
```
var o = {x:1,y:{z:3}}; 
var a = [o,4,[5,6]];
o.x                 // => 1
o.y                 // => {z:3}
o.y.z               // => 3
o["x"]              // => 1
a[1]                // => 4
a[2]["1"]           // => 6
a[0].x              // => 1
a[0].y              // => {z:3}
a[0].y.z            // => 3
```

### 4.8 산술 표현식
#### 4.8.1 덧셈 연산자 +
```
1 + 2                       // => 3
"hello" + " " + "there"     // => 'hello there'
"1" + "2"                   // => '12'
1 + {?}                     // => "1[Object object]"
true + true                 // => 2
2 + null                    // => 2
2 + undefined               // => NaN
```
#### 비트 단위 연산자
> 비트 단위 XOR (^)  
>> 0xFF00 ^ 0xF0F0          // => 0x0FF0 /* OR과 다르게 둘다 true가 아닐시에 결과가 true가 된다. */

> 0으로 채우면서 오른쪽으로 이동 (>>>)
>> (>>>) 연산자는 >> 연산자와 비슷하지만 >>> 연산자는 부호와 관계없이 무조건 0이다.  
>> 예를 들어, -1 >> 4 의 결과는 -1이지만, -1 >>> 4의 결과는 0x0FFFFFFF이다.

### 4.9 관계형 표현식
#### 4.9.1 동치와 부등치 연산자

> ```==``` 동치 연산자는 타입을 가리지 않고 주어진 값이 같으면 true, 다르면 false  
> ```===``` 동치 연산자는 두 값이 일치하는 판단할 때는 다음의 규칙을 따르며, 타입 변환은 히지 않는다.  
>> 두 값 모두 null 일 경우 혹은 undefined이면 일치한다.  
>> 두 값 모두 false일 경우 혹은 true이면 일치한다.  
>> 두 값 모두 문자열이고, 같은 위치에 정확히 같은 16비트 값을 가지고 있다면 일치한다.  
>> 두 값이 모두 같은 객체나 배열 또는 함수를 참조하고 있으면, 두 값은 일치한다. 등등   

#### 4.9.3 in 연산자
```
var point = { x:1, y:1 };
"x" in point                // => true
"z" in point                // => false
"toString" in point         // => true : 상속된 프로퍼티
var data = [7, 8, 9];
"0" in data                 // => true
1 in data                   // => true
3 in data                   // => false
```
#### 4.9.4 instanceof 연산자
```
var d = new Date();
d instanceof Date;          // => true;
d instanceof Object;        // => true;
d instanceof Number;        // => false;
var a = [1, 2, 3]
a instanceof Array;         // => true;
a instanceof Object;        // => true;
a instanceof RegExp;        // => false;
```

### 4.10 논리 표현식
#### 4.10.1 논리 AND (&&)
```
if ( a == b ) stop();
(a == b) && stop();         // 위의 코드와 작동은 같다.
```

#### 4.10.2 논리 OR (||)
```
// 이 코드는 여러 값 중에 최초로 true로 평가 되는 값을 선택하는 경우에 사용된다.
var max  = max_width || preference.max_width || 500;


function copy(o, p){
    p = p || {?};       //만약 p가 null이라면(false), 새롭게 객체를 생성한다. 
    ...
}
```

### ~~4.12 평가 표현식 ( eval() ) 생략~~
### 4.13 기타 연산자들
#### 4.13.1 조건부 연산자 ( ? : )
```
let a = 10;
a == 10 ? true : false ;

if(a == 10){                //위 3항 연산자와 같은 작동을 하는 코드
    return true;
}else{ 
    return false; 
}
```

#### 4.13.2 typeof 연산자
```
x = undefined           typeof(x)       // => "undefined"
x = null                typeof(x)       // => "null"
x = true || false       typeof(x)       // => "boolean"
x = digits || NaN       typeof(x)       // => "number"
x = 문자열               typeof(x)       // => "string"
x = 함수                 typeof(x)       // => "function"
x = 함수가 아닌 객체      typeof(x)       // => "object"
x = 호스트 객체(..?)     typeof(x)       
    // => "undefined"나 "boolean", "number","string"을 제외한 구현부 정의 문자열
```
switch문 혹은 3항 연산자와 함께 사용하면 유용하다.
```
let userInput = ...;
switch (typeof(userInput)){
    case "string" : console.log(이름)
        break;
    case "number" : console.log(전화번호)
        break;
    case "object" : console.log(userInput.conutry +"\n" +userInput.city +"시\n");
        break;
    default : console.log(이런식으로?)
}
```
> null 값은 object로 반환하여 구분하고 싶으면 명시적으로 null인지 테스트하는게 좋다.

#### 4.13.3 delete 연산자
```
var o = { x:1 , y:2};
delete o.x;                 // => true
"x" in o                    // => false

var a = [1,2,3];
delete a[2];                // 배열의 마지막 원소를 지움.
2 in a                      // => false
a.length                    // => 3 /* 배열 길이는 변하지 않음에 유의하라! */
```
