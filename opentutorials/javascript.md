### Object Model
Window 객체는 모든 객체가 소속된 객체로 전역객체이며, 창이나 프레임을 의미함

window객체의 하위 객체 들
- BOM
- DOM
- JavaScript


### BOM
alert

confirm
- 확인/취소 popup 생성
- 확인 : true 리턴
- 취소 : false 리턴

prompt
- 값을 입력받음

location
- location.href : 현재주소
- location.host : 호스트 식별자



























## 기본

### 정규표현식
#### 정규표현식 생성
```javascript
// 스크립트를 불러올때 컴파일 (이미 정해진 상수를 사용할 경우 성능향상에 유리)
var pattern = /a/;

// 정규식의 실행 시점에 컴파일 (패턴변경, 유저 입력 등 다른 출처에서 패턴 가져올 경우 사용)
var pattern = new RegExp('a');
```

#### RegExp.exec() / RegExp.test()
- exec()는 조건을 만족하는 문자열을 리턴
- test()는 조건을 만족하는 문자열이 있으면 true, 아니면 false를 리턴

#### 옵션
i : 대소문자 구분하지 않음
```javascript
var oi = /a/i;
console.log("Abcde".match(oi));     //["A"]
```

g : 검색된 모든 결과 리턴
```javascript
var og = /a/g;
console.log("abcdea".match(og));    //["a", "a"]
```

응용(캡쳐)
```javascript
var pattern = /(\w+)\s(\w+)/;
var str = "coding everybody";
var result = str.replace(pattern, "$2, $1");
console.log(result);    // everybody, coding
```

응용2(치환)
```javascript
var urlPattern = /\b(?:https?):\/\/[a-z0-9-+&@#\/%?=~_|!:,.;]*/gim;
var content = '생활코딩 : http://opentutorials.org/course/1 입니다. 네이버 : http://naver.com 입니다. ';
var result = content.replace(urlPattern, function(url){
    return '<a href="'+url+'">'+url+'</a>';
});
console.log(result);
// 생활코딩 : <a href="http://opentutorials.org/course/1">http://opentutorials.org/course/1</a> 입니다. 네이버 : <a href="http://naver.com">http://naver.com</a> 입니다. 
```


## 함수
### 유효범위

#### 전역, 지역변수
```javascript
var vscope = 'global';
function fscope(){
    vscope = 'local';
    alert('함수안'+vscope);
}
fscope();
alert('함수밖'+vscope);

// 함수안local
// 함수밖local
```
fscope의 지역변수를 var을 사용하지 않고 정의하였기 때문에 <code>전역변수</code>로 선언 됨

#### 전역변수를 써야 한다면..
하나의 객체를 전역변수로 만든 후 객체의 속성으로 관리하는 것이 좋음
```javascript
MYAPP = {}
MYAPP.calculator = {
    'left' : null,
    'right' : null
}
MYAPP.coordinate = {
    'left' : null,
    'right' : null
}
 
MYAPP.calculator.left = 10;
MYAPP.calculator.right = 20;
function sum(){
    return MYAPP.calculator.left + MYAPP.calculator.right;
}
document.write(sum());

```

아니면 전체를 함수로 감싼 후 바로 실행하는 방법도 있음
```javascript
(function(){
    ...
}())
```

#### lexical scoping
- 정적 유효범위(scoping)
- 정의 될 때의 변수를 따름


### 값으로서의 함수와 콜백
#### 값으로서의 함수
```javascript
function a() { ... }
// 는 아래와 같다
var a = function() { ... }
```


#### 비동기 처리
Ajax : asynchronous javascript and XML


#### 클로져(closure)
- 내부함수가 외부함수의 맥락에 접근할 수 있는 것
- private변수를 만든다?
  - 전역변수의 사용을 지양하는 것처럼
  - 변수에 대한 접근을 제한(get, set 등을 통해)함으로써 의도치 않은 변경을 제한
    - set에서 type체크를 할 수도 있고... and so on.
    
#### arguments
```javascript
function one(arg1){
    console.log(
        'one.length', one.length,
        'arguments', arguments.length
    );
}

one('val1', 'val2'); // one.length 1 arguments 2
```

#### 함수의 호출
```javascript
function sum(arg1, arg2) {
    return arg1+arg2;
}
//호출방법
sum(1, 2);
sum.apply(null, [1,2]);    // 첫번째 인자(null)은 함수가 실행되는 맥락.
```

apply
- 주어진 'this' Object와 배열로 함수를 호출

call
- apply와 거의 동일
- 여러 배열을 파라미터로 넘길 수 있음
    - 함수명.call(this, name, price)
```javascript
function Product(name, price) {
  this.name = name;
  this.price = price;
}
function Food(name, price) {
  Product.call(this, name, price);
  this.category = 'food';
}
console.log(new Food('cheese', 5).name);
// expected output: "cheese"
```

bind
- 파라미터로 넘겨받은 value를 호출한 함수의 this에 대입하여 함수 생성



## 객체 지향
### 생성자와 new
자바스크립트는 **prototype-based programming**

#### 생성자
new 함수명();
- 비어있는 객체를 만들고 반환

```javascript
function Persion(){ }
var p = new Person();
```

### 상속
Prototype
- [참고1 : 오승환님의 프로토타입 이해하기 블로그 글](https://medium.com/@bluesh55/javascript-prototype-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-f8e67c286b67)
- [참고2 : Insanehone님의 프로토타입 이해하기 블로그 글](http://insanehong.kr/post/javascript-prototype/)
- Prototype Object : 함수 선언과 동시에 생성
    - constructor와 __proto__로 구성
    - constructor : Prototype Object 생성을 야기한 함수
    - __proto__ : Prototype Link
        - Prototype Link : 객체 생성시 조상이었던 함수의 Prototype Object를 가리킴
        - new 함수명(); 을 통해 객체를 생성한 경우라면 '함수명'의 Prototype Object임.
        
        
## Object
Object.xxx vs Object.prototype.xxx 
- Object.xxx : Object.xxx()를 통해 사용
- Object.prototype.xxx : 생성한 객체가 바로 사용

Object.prototype.XXX = function... 을 통해 사용자 정의 함수를 Object를 추가
- for loop에서 정의한 function이 나와버림.
- 기존 Object.prototype은 built in 이라 괜찮지만
- 사용자 정의 property는 순환에 포함 됨
```javascript
Object.prototype.contain = function(param) {
...
}
```

## 데이터 타입
### 원시 데이터 타입
숫자, 문자열, 불리언, null, undefined

### 래퍼 객체
- 숫자 -> Number
- 문자열 -> String
- 불리언 -> Boolean
- null, undefined -> 없음


