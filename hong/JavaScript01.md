# JavaScript Study 01

## 1 자바스크립트 소개
### 1.1 자바스크립트 코어
> 자바스크립트는 다양한 타입의 값을 지원한다.
```
var x;                  // var 키워드로 선언하여
x = 1;                  // 숫자
x = 0.1;                // 정수나 실수
x = "hello world";      // 문자열
x = true;               // 참 혹은 거짓
x = null;               // null값
x = undefined;          // 정의되지 않은 값 등등 타입 관계없이 아무거나 넣을 수 있다.
```
> 자바스크립트 에서 가장 중요한 데이터 타입은 객체이다.
>> 객체는  이름 - 값 쌍( name-value pair )의 모음이다.

```
var book = {
    topic : "javaScript"    // topicdml 프로퍼티의 값은 "javaScript"이고
    fat : true              // fat 프로퍼티의 값은 true이다.
}

// 여기서 객체의 프로퍼티는 .와 []를 사용하여 접근할 수 있다.
book.topic                  // => javaScript
book["fat"]                 // => true
book.author ="Flanagan"     // 새 프로퍼티를 생성할 수 도 있다.
book.contents = {
    title: "JAVASCRIPT THE.."
};                          // book의 객체 안에 새로운 객체를 넣을 수 있다.
                            // => book = {
                                    topic: "javaScript"
                                    fat: true
                                    author: "Flanagan"
                                    contents: {
                                        title: "JAVASCRIPT THE.."
                                    }
                                }
```
>> 배열과 객체는 각각 원소와 프로퍼티의 값으로 배열과 객체를 가질 수 있다.
```
var points = [
    {x:0, y:0},         // 배열에 두 원소는 각각 객체이다.
    {x:1, y:1}
]

points[0].x             // => 0
points[1].y             // => 1

var data = {
    trial1: [[1,2], [3,4]],     //각 프로퍼티의 값은 배열이고, 배열의 각 원소는 배열이다
    trial2: [[2,3], [4,5]]
}

data.trial1[0].[0]              // => 1 /* 확실하진 않지만 이런식으로 사용할듯하다 */
```
>> 함수도 객체의 프로퍼티로 사용할 수 있다. 이때 함수는 객체의 메서드가 된다.
```
function plus1(x){
    return x+1;
}

var square = function(x){
    return x*x;
}

square(plus1(3))               // => 16; plus 함수에서 3+1을 리턴하고 square 4*4
```

### ~~1.2 클라이언트 측 자바스크립트 (생략)~~