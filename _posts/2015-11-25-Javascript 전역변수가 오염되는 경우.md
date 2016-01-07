---
layout: post
tags: javascript 전역변수 오염 스코프 글로벌변수
---

호이스팅이라던지, 함수와 블럭에서의 this 라던지.. 전역변수를 어지럽히는 경우가 많습니다.
이러한 경우들을 정리하여, 협업시을 할 때나 모듈을 제공할 때 프로그램이 오작동 하지 않도록 주의 해야겠습니다.


### 전역변수 ###
전역변수와 지역변수 개념은 Javascript 에서도 예외 없이 사용되는 개념이지만, 이를 정확히 숙지하지 못한 경우 이해할 수 없는 결과물을 받아보게 될 수 있습니다.

######전역변수 선언방법######
```Javascript
var myName = "Rechrd";	
firstName = "Rechard";	
name = "Rechard";		

console.log("myName" in window);	// true
console.log("firstName" in window);	// true
console.log("name" in window);		// true
```
>모든 전역객체는 window 객체 안에 포함되어 있으므로 3가지 변수의 console 결과가 true 로 출력 되는것을 확인 할 수 있습니다.
 

Java의 블럭 수준 (block-level) 범위와 달리 Javascript는 함수 수준 (functoin-level) 범위를 지원 합니다. 이러한 개념의 차이로, Javascript에서 전역 객체를 다른 프로그래밍 언어처럼 사용 했을 경우, 의도치 않게 전역변수를 오염시키는 경우 입니다.

###### 전역객체를 오염시키는 경우 1 ######
```Javascript
function abc(){
	age = "90";
    this.sex = "M";
}
abc();
console.log("age" in window );	// true
console.log("sex" in window );	// true

var name = "Richard"; // 전역변수
if (name) {
     name = "Jack";	// 전역변수를 오염시킴
}
console.log(name); // Jack
```
>var 키워드를 사용하지 않은경우 자동으로 전역 컨텍스트에 추가됩니다.
>반드시 var 키워드를 사용하여 스코프를 제한하는 습관을 가져야 합니다.



###### 전역객체를 오염시키는 경우 3 ######

```javascript
var firstName = "Richard"; // 전역변수
{
     var firstName = "Bob";	// 전역변수를 오염시킴 (선언을 했음에도..)
}
console.log(firstName); // Bob
```
>{..} 블럭 안에 var 키워드를 사용 했음에도 불구하고 전역객체를 오염시키고 있습니다.
>함수 수준 (functoin-level) 범위 임을 다시한번 기억해야 합니다.
>이러한 점으로 미루어 보아, ++변수의 네이밍에도 신경을 써야한다++ 는 것을 알 수 있습니다.


###### 전역객체를 오염시키는 경우 5 ######
```Javascript
for (var i=1; i<=10; i++) {
     console.log(i); // 1~10까지 출력
}

// 변수 i는 전역 변수입니다. 그러므로, 아래 함수 호출시 i는 for문에서 실행된 후 마지막 값을 가르키게 됩니다.
function aNumber() {
     console.log(i);
}

aNumber(); // 11
```
###### 전역객체를 오염시키는 경우 6 ######
```Javascript
// setTimeout 함수내에서 사용된 "this"객체는 myObj가 아니라, window객체를 참조합니다.
var highValue = 200;
var constantVal = 2;
var myObj = {
     highValue: 20,
     constantVal: 5,
     calculateIt: function() {
          setTimeout(function() {
               console.log(this.constantVal * this.highValue);
          }, 2000);
     }
}

// 전역변수인 highValue와 constantVal을 사용하여 계산됩니다. 200*2.
myObj.calculateIt(); //400
```


>참조한 링크
>- [자바스크립트의 변수범위와 호이스팅](http://chanlee.github.io/2013/12/10/javascript-variable-scope-and-hoisting/)

