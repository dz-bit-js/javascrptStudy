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
```

### 6.7 프로퍼티 속성
> writable : 프로퍼티 값을 변경 가능 여부  
> enumerable : 열거될 수 있는지 여부  
> configurable : configurable 속성, writable 속성, enumerable 속성 값의 변경 가능 여부  
> * 프로토타입 객체에 메서드를 추가할 수 있고, 추가된 메서드를 내장 메서드처럼 열거할 수 없게 만들수 있음.  
> * 변경하거나 삭제할 수 없는 프로퍼티를 정의하여, 객체를 고정 시킬수 있음.  

객체가 가진 특정 프로퍼티에 대한 프로퍼티 객체는 ``` Object.getOwnPropertyDescriptor()``` 을 통해 얻음.  

```
// {value:1 , writable:true, enumerable:true, configurable:true}반환
Object.getOwnPropertyDesciptor({x:1}, "x");
```
프로퍼티의 속성을 설정하거나 임의의 속성으로 새 프로퍼티를 만들기 위해 ```Object.defineProperty()``` 호출  
```
var o = {};

Object.defineProperty(o, "x", { value : 1,
                                wirtable: true
                                enumerable: false
                                configurable: true});

o.x;            //=> 1
Object.keys(o)  //=> []
```
여러 개의 프로퍼티를 만들거나 수정하고 싶을 때 ```Object.defineProperties```
```
var p = Object.defineProperties({}, {
    x: { value: 1, writable: true, enumerable: true, configurable: true},
    y: { value: 1, writable: true, enumerable: true, configurable: true},
    r: { 
        get: function() { return Math.sqrt(this.x*this.x + this.y*this.y)},
        enumerable:true,
        configurable:true
    }
});
```

> ```Object.create()``` 함수의 첫 인자로는 객체의 프로토타입 객체 ,두 번째는 defineProperties() 인자  

### 6.8 객체 속성
#### 6.8.1 prototype 속성
> prototype 속성은 객체가 만들어지는 시점에서 설정된다.  
> * 객체 리터럴을 통해 만든 객체는 Object.prototype을 프로토타입으로 설정  
> * Object.create() 메서드로 만든 객체는 첫 인자가 프로토타입 속성의 값  
>> 하지만 Object.create()로 생성된 객체는 정확한 프로토타입을 참조하지 않음.  

...
### 6.9 객체 직열화하기
> JSON 데이터 교환형식
```
o = { x:1, y:{z:[false,null,""]}};
s = JSON.stringify(o);      // s는 '{' 'x':1, 'y':{'z':[false,null,""]}}'문자열이다
p = JSON.parse(s);          // p는 객체 o를 복사한 객체다.
```

### 6.10 객체 메서드
#### 6.10.4 valueOf()
> 자바스크립트가 객체를 숫자와 같은 다른 원시 타입으로 변환하려 할 때 호출된다.

