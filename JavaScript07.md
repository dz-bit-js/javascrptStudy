# JavaScript Study 07
## 7. 배열
### 7.1 배열 만들기
```
var misc = [ 1.1, true, "a", ]   // 서로 다른 종류의 세 원소가 존재
                                 // 쉼표로 끝나는 배열 

var undefs = [,,]                // 두 원소 모두 값은 undefined -> 원소 개수 : 2
```

### 7.6 배열 순회하기
```
// null 이나 undefined 또는 빈 원소를 건너 뛰고 싶을때
for(var i = 0; i< a.length; i++){
    if(!a[i])
        continue;
}

// undefined와 빈 원소들만 건너뛰고 싶을 때 
for( var i = 0 ; i< a.length; i++){
    if( a[i] === undefined)
        continue;
}

// 빈 원소 인덱스는 건너뛰지만 원소 값이 undefined인 경우는 루프 안에서 처리
for( var i = 0 ; i< a.length; i++){
    if( !(i in a))
        continue;
}
```

### 7.8 배열 메서드
#### 7.8.1 join()
> ``` Array.join() ```메서드는 배열의 모든 원소를 문자열로 변환하고, 변환한 문자들을 이어 붙인 결과 반환  
```
var a = [1, 2, 3];
a.join();                // => '1,2,3'
a.join(" ");             // => '1 2 3'
a.join("");              // => '123'
a.join("-");             // => '1-2-3'
```

#### 7.8.3 sort()
> ``` Array.sort() ```메서드는 배열 안의 원소들을 정렬하여 반환한다.
```
var a = new Array("banana","cherry","apple");
a.sort();                    //별도의 전달인자 없이 호출하면 알파벳순으로 정렬
a.join(", ");                // => 'apple, bananan, cherry'


var a = [33, 4, 1111, 222];
a.sort();                       // 알파벳순: 1111, 222, 33, 4
a.sort(function(a,b){           // 번호순: 4, 33, 222, 1111
    return a-b;                 // 0보다 작은 값, 0 또는 0보다 큰 값을 반환
                                // 이떄 반환 값에 따라 정렬이 달라진다.
});
a.sort(function(a,b){
    return b-a;                 // 내림차순으로 정렬
})


a = ['ant', 'Bug', 'cat', 'Dog'];
a.sort();                   // 대소문자를 구분한 정렬: ['Bug', 'Dog', 'ant', 'cat']
```

#### 7.8.5 slice()
> ``` Array.slice() ```메서드는 부분 배열을 반환하는데 여기서 부분 배열은 새 배열이다.
```
var a = [1,2,3,4,5];
a.slice(0,3);               // => [1,2,3]
a.slice(3);                 // => [4,5]
a.slice(1,-1);              // => [2,3,4]
a.slice(-3,-2);             // => [3]
```
#### 7.8.5 splice()
> ``` Array.splice() ```메서드는 부분 배열을 반환하는데 호출 대상 배열을 바로 수정한다.  
```
// 첫 인자는 시작위치, 두 번째 인자는 원소 개수
var a = [1,2,3,4,5,6,7,8];
a.splice(4)                 // => [5,6,7,8]을 반환한다. a == [1,2,3,4]
a.splice(1,2)               // => [2,3]을 반환한다.     a == [1,4]
a.splice(1,1);              // => [4]을 반환한다.       a == [1]

// 3번째 인자부터는 배열에 새롭게 삽입할 원소를 지정하고 첫 번째 위치부터 삽입 수행한다.
var a = [1,2,3,4,5];
a.splice(2,0,'a','b');      // => []를 반환한다.        a == [1,2,'a','b',3,4,5]
a.splice(2,2,[1,2],3);      // => ['a','b']를 반환.     a == [1,2,[1,2],3,3,4,5]
```

### 7.9 ECMAScript5 베열 메서드
#### 7.9.1 foreach()
```
var data = [1,2,3,4,5];
var sum = 0;
data.forEach(function(value) {sum += value; });
sum                                                 // => 15

data.forEach(function(v, i, a) {a[i] = v + 1 });
data                                                // => [2,3,4,5,6]
```
#### 7.9.2 map()
```
a = [1,2,3];
b = a.map(function(x){ return x*x; });              // => b == [1, 4, 9]
```
#### 7.9.3 filter()
```
a = [5, 4, 3, 2, 1];
smallvalues = a.filter( function(x) {return x<3 });     // [2, 1]
everyother = a.filter ( function(x) {return i%2==0 })   // [5, 3, 1]
```
#### 7.9.4 every() some()
```
a = [1,2,3,4,5];
a.every(function(x) { return x < 10;})              // => true 반환
                                        // 모든 값이 10보다 작음

a.every(function(x) { return x % 2 ===0; })         // => false 반환
                                        // 모든 값이 짝수가 아님.

a.some(function(x) { return x % 2 ===0; })          // => true 반환
                                        // 짝수가 존재함.

a.some(isNaN);                          // 배열 a에는 숫자만 있어서 false 반환
```
#### 7.9.5 reduce()와 reduceRight()
>