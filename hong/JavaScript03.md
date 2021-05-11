# JavaScript Study 03
## 3. 타입, 값, 변수
### 3.1 숫자
> 정수 리터럴 
>> 0    10000   3  

> 16진수 리터럴
>> 0Xff // 15*16 + 15 = 255  
>> 0XCAFE911  

> 부동소수점 리터럴
>> [''digits''] [.''digits'']   [   (E |   e)  [(+  |   -)] ''digits'']  
>> 3.14  
>> .333333333333333
>> 6.02e23 //   6.02 X 10^23  
>> 1.473822E-32     //  1.473822 x 10^-32 

> 자바스크립트는 산술 연산의 결과가 표현할 수 있는 값보다 더 크다면 ```Infinity``` 라고 표현이 출력한다.  
> 반대로 산술 연산의 결과가 가장 작은 음수 값보다 더 작은 값은 ```-Infinity```로 출력한다.  
>
> 0을 0으로 나누는 것, 무한대를 무한대로 나누는 경우와 음수 값에 루트를 씌우는 경우 등등  
그 결과로는 숫자가 아닌 특수한 값 ```NaN```을 출력한다.  

### 3.2 텍스트
> 역슬래시 문자(\)는 자바스크립트 문자열에서 특별한 목적을 위해 사용한다.  
>> 'You\\'re right, it can\\'t be a quote'  =>  'You\'re right, it can\'t be a quote'

### 3.3 불리언 값
```
undenfined      null        0       -0       NaN        "" //빈 문자열
```
위의 값 모두 불리언 false 값으로 변한다.
```
if (o !== null) 대신  if(o)로 대체하여 사용할 수 있다.
```

### 3.4 null 과 undefined
**```null```** 은 '객체가 없음'을 뜻하는 특수한 객체 값으로 생각할 수 있다.  
**```undefined```** 는 null보다도 심한 부재 상태를 나타낸다.  
typeof 연산자를 **```null```** 에 사용하면 "object"를 반환하지만 **```undefined```** 은  "undefined"가 반환된다.  
**```null```** 과 **```undefined```** 를 동치 연산자 == 사용하면 두 값이 같다고 간주하지만  
엄격한 동치 연산자 ===를 사용하면 false로 판정된다.

###  시스템 수준에서 예기치 않은 상황에 발생한, 오류성 값 부재를 표한할 때는 **```undefined```**  
### 예상 가능한 값 부재 상황은 **```null```**

### 3.8 타입 변환
자바스크립트가 숫자를 원한다면 숫자가 올 자리에 다른 어떤 값이 오더라도 숫자로 변환될 것이다.  
그러나 의미 있는 변환을 할 수 없다면 NaN으로 변환될 것이다.  
```
10 + " objects"         // => "10 objects"
"7" * "4"               // => 28
var n = 1 - "x"         // => NaN
n + " objects"          // => "NaN objects"
```

>>>>>>>>**57page 표 3-2 자바스크립트 타입 변환 보기**  

#### 3.8.1 변환과 동치

```
null == undefined       // =>true
"0" == 0                // =>true
0 == false              // =>true
"0" == false            // =>true
```

### 3.10 변수의 유효범위
전역 변수와 지역 변수가 같은 이름을 갖는 경우 함수 내부에서 지역 변수가 우선된다.
```
var scope = "global";
function checkScope(){
    var scope = "local";
    return scope;
}
checkScope()        // => "local"
```
전역 변수에 var문을 사용하지 않고 전역 변수를 선언한 경우
```
scope = "global";
function checkScope2(){
    scope = "local";
    myscope = "local";
    return [scope, myscope];
}

checkscope2()       // => ["local", "local"]
scope               // => "local"
myscope             // => "local"
```

지역 유효범위도 여러 단계로 중첩될 수 있다.
```
var scope = "global scope";

function checkscope(){
    var scope = "local scope";
    function nested(){
        var scope = "nested scope";
        return scope;
    }
    return nested();
}

checkscope()        // => "nested scope"
```

#### 3.10.1 함수 유효범위와 끌어올림 (hoisting)