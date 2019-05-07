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
