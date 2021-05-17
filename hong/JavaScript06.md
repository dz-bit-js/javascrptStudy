# JavaScript Study 06
## 6. 객체
> 자바스크립트 객체는 객체가 가진 고유 프로퍼티를 유지하는 것 외에 '프로토타입'이라고 하는 다른객체의 프로퍼티를 상속받는다.  

> ``` var y = x;```  실행될 때 변수 y는 x와 같은 객체를 참조하며, 객체 자체를 복사하지 않는다.

#### 6.1.3 프로토타입
> new Object()로 생성된 객체는  Object.prototype 상속받음.  
> new Array()로 생성된 객체는 Array.prototype을 상속받음.  
> new Date()로 생성된 객체는 Date.prototype을 상속받는다.  
>> Object.prototype은 아무런 프로퍼티도 상속받지 않는다.

#### 6.2.1 연관 배열로서의 객체
```
function getValue(portfolio){
    var total = 0.0;
    for(stock in portfolio){
        var shares = portfolio[stock];
        var price = getquote(stock);
        total += shares * price;
    }
    return total;
}
```

#### 6.2.2 상속
```
var o = {}
o.x =1;
var p = inherit(o);
p.y = 2;
var q = inherit(p);
q.z = 3;
var s = q.toString(); //q는 Object.prototype을 상속받음
q.x + q.y             // => 3
```
> 객체의 프로퍼티에 값을 설정할 때는 해당 프로퍼티에 값을 설정할 수 있는지를 알아보기 위해 프로토차입 체인을 검사하게 된다.  
> 프로토타입 체인은 결코 변경되지 않는다.
```
var unitcircle = { r:1 };
var c = inherit(unitcircle);
c.x = 1; c.y = 1;
c.r = 2;
unitcircle.r;           // => 1
```

### 6.3 프로퍼티 삭제하기
```
o = {x:1};
delete o.x;
delete o.x;             // x가 존재하지 않기 때문에 아무 일도 하지 않고 true를 반환.
delete o.toString();    // o의 고유 프로퍼티가 아니기 때문에 아무 일도 하지 않고 true
delete 1;               // true반환
```

### 6.4 프로퍼티 검사하기
```
var o = { x:1 };
"x" in o;
"y" in o;               // false
"toString" in o;        // true

o.hasOwnProperty("x");          // true
o.hasOwnProperty("y");          // false
o.hasOwnProperty("toString");   // false
```
> ```propertyIsEnumerable()```는  객체에 주어진 이름의 고유 프로퍼티가 존재하고, 열거할 수 있는 프로퍼티인 경우만 true를 반환한다. (에시 생략)  

>>>>>>> undefined
```
var o = { x:1 };
o.x !== undefined;
o.y !== undefined;
o.toString !== undefined;       // true

var o = { x: undefined };
o.x !== undefined;              // false
o.y !== undefined;              // false
"x" in o;                       // true
"y" in o;                       // false
```

### 6.5 프로퍼티 열거하기
```
for(p in o){
    if(!o.hasOwnProperty(p))
        continue;               // 상속받은 프로퍼티는 생략
}

for(p in o){
    if(typeof o[p] === "function")
        continue;               // 해당 프로퍼티가 메서드면 생략
}

/* 등등 page 159쪽에 객체 프로퍼티 열거하는 유용한 함수들 있음. */
```

### 6.6 프로퍼티 Getter과 Setter
```
var o = {
    data_prop = value,

    // 한 쌍의 함수로 정의된 접근자 프로퍼티
    get accessor_prop() { /* 함수 몸체 */},
    set accessor_prop(value) { /* 함수 몸체 */}
};