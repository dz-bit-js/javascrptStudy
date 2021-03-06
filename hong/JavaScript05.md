# JavaScript Study 05
## 5. 문장
### 5.5 루프
#### 5.5.3 for
> 연결리스트 자료구조를 순회하고, 리스트의 마지막 객체(next 속성을 갖지 않는 첫 번째 객체)를 반환하기 위한 for문
```
function tail(o){
    for (; o.next; o = o.next)
        ;                       // 빈 문장
    return o;
}
```

#### 5.5.4 for / in (다시 공부하기...)
```
for (변수 in 객체)
    문장
```
여기서 변수는 좌변 값으로 평가되는 표현식이거나, 단일 변수를 선언하는 var 문일 수도 있다.

```
for(var i = 0; i < a.length ; i++){
    console.log(a[i])       // 원소의 값을 출력한다.
}
                            // for / in 루프는 원소를 출력한다.
for(var i in a){            // 변수 i에 객체 a가 가진 프로퍼티 이름을 할당한다.
    console.log(i);         // 객체 o가 가진 각 프로퍼티의 값을 출력한다.
                            // => "x"           "y"           "z"
}
```

for / in 문을 실핼하기 위해서 자바스크립트는 인터프리터는 먼저 객체 표현식을 평가한다.  
이때 표현식이 null이나 undefined로 평가 되면 인터프리터는 해당 루프를 중단하고 다음 문장을 실행한다.  

> for/in 루프에서 사용하는 '변수'로는 할당 표현식의  좌변에 적합한 문건가로 평가되는 임의의 표현식을 사용할 수 있다.

```
// 주어진 객체의 모든 프로퍼티 이름을 배열에 복사하는 코드
var o = { x:1 , y:2 , z:3 };
var a =[], i = 0;
for(a[i++] in o)
    console.log(a);         // =>["x"] 
                            // =>["x", "y"] 
                            // =>["x", "y", "z"]
```

### 5.6 점프문
자바스크립트 인터프리터가 점프문을 만나면 소스 내의 특정 위치로 건너뛴다.  
예를들면 인터프리터가 break문을 만나면 루프나 다른 문장의 끝으로 건너뛰고  
continue문을 만나면 나머지 루프 몸체에 있는 문장들을 생략하고 새 루프 시작점으로 거넌뛴다.
#### 5.6.1 레이블
어떤 문장에라도 그 앞에 식별자 이름과 콜론(:)을 넣음으로써 레이블을 붙일 수 있다.
```
mainloop: while(token != null){
    // 코드 생략..
    continue mainloop;      // 주어진 mainloop의 다음 반복으로 건너뛴다.
    // 코드 생략..
    break mainloop;         // 주어진 mainloop를 끝낸다.
    // 코드 생략..
}
```
> 레이블이 속한 이름공간(namespace)은 변수나 함수의 이름공간과는 다르다. 따라서 변수나 함수이름과 같은 식별자를 레이블로 사용할 수 있다.  
> 어떤 문장이든 열러 개의 레이블을 가질 수 있다.  

### 5.7 기타
#### 5.7.1 with
with문은 유효범위 체인을 임시로 확장할 때 쓰인다.  
with문은 사용하지 않는게 좋다. 최적화하기 힘들고 with문을 사용하지 않는 코드에 비해 현저히 느리기 때문.
```
with(객체)
    문장

with(document.forms[0]){
    name.value = "";
    address.value = "";
    email.value = "";
}
```

#### 5.7.2 debugger
debugger문은 코드의 중단점과 같이 동작한다.
```
function f(o){
    if( o === undefined) debugger; 
}

함수 f() 인자 없이 호출되거나 인자 값이 undefined일 경우 코드 실행이 중단되고 디버거가 실행됨
```

#### 5.7.3 "use strict"
**엄격 모드..**