---
layout: post
tags: javascript 전역변수 스코프 글로벌변수
---

여러가지 함수 표현식을 알아보고, 각각 어떻게 작동하는지 알아봅시다.


### Javascript는 first-class object 이다. ###
Javascript는 함수를 선언 할 수도 있고, 변수에 할당 할 수도 있습니다. 
후자의 개념은 혼란스럽고도 재미있다고 볼 수 있겠는데, 이러한 개념이 바로 `first-class object` 라고 합니다. 다른 특징들은 다음과 같습니다.

###### first-class object 특징 ######
1. ++변수에 저장할 수 있어야한다. (함수 선언방식과 표현방식)++
2. 함수의 입력 파라미터로 사용할 수 있어야 한다.
3. 함수의 출력 파라미터로 사용할 수 있어야 한다.
4. 자료구조에 저장 가능해야 한다.




###함수선언 방식 vs 함수표현 방식###
선언 방식은 global 객체로 취급되어 가장 먼저 해석되어집니다. (Hosting 이라고 합니다)
함수 내에서 선언이 일어 났다면, 함수내 최상위로, 함수 바깥에서 정의 되었다면 전역 컨텍스트로 올라가는점을 염두하고 읽어 주세요.


######함수선언 방식은 global 객체로 취급된다.######

```javascript
foo();	// 'hello'
function foo() {
    console.log('hello');
}; 
foo();
```  
>1. 자바스크립트 엔진 구동시, global 영역에 있는 선언문인 `function foo`를 먼저 해석 합니다 
>2. 글로벌 변수, 글로벌 함수는 자바스크립트 엔진 구동시 최초로 해석되어 집니다.
>3. 글로벌 선언은 어디에 선언 되어있건 실행 및 참조가 가능합니다.
>4. 너무 많은 글로벌 선언은 당연히 성능에 영향을 주게 됩니다.


  

######함수표현 방식은 변수에 함수를 할당 하는것으로, 런타임에 이루어 진다.######
```Javascript
foo();	// Uncaught TypeError: foo is not a function
var foo = function() {
    console.log('hello');
};
foo();
```
>foo가 선언되기 전에 실행이 되면 에러가 발생합니다.
>1. 할당은 런타임에서 이루어 집니다.
>2. var foo 에 function 이 할당 되기 전에 사용 되었으므로, `foo()` 는 에러를 내뿜는다.


###  즉시 실행 함수 ###
IIFE 라고도 합니다. (Immediately Invoked Function Expressions: "Iffy"라고 발음)
글로벌 스코프를 오염시키지 않기 위해 사용하는 기법중 하나 입니다.

######즉시실행함수 표현식######
```javascript
alert(foo); // "foo" is not defined.
(function foo() {
    console.log('기명 즉시실행 함수표현식');
}());
alert(foo); // "foo" is not defined.

(function() {
    console.log('익명 즉시실행 함수표현식');
}());
```

>참조한 링크
>- [Function Declarations(함수선언) vs Function Expressions(함수표현)](http://insanehong.kr/post/javascript-function/ "")
>- [Javascript : 함수(function) 다시 보기](http://www.nextree.co.kr/p4150/)
>- [[리얼타임] You Don’t Know JS 스코프와 클로저](https://books.google.co.kr/books?id=QxrJCQAAQBAJ&pg=PA35&lpg=PA35&dq=%EC%9D%B5%EB%AA%85%ED%95%A8%EC%88%98+%EA%B8%B0%EB%AA%85%ED%95%A8%EC%88%98%EC%9D%98+%EC%B0%A8%EC%9D%B4&source=bl&ots=qTnfOnm69v&sig=jb6BA9DBoDjE4xuo82BsK5exx6o&hl=ko&sa=X&ved=0ahUKEwjM6r2yn4nKAhUD6KYKHaasAtUQ6AEINTAD#v=onepage&q=%EC%9D%B5%EB%AA%85%ED%95%A8%EC%88%98%20%EA%B8%B0%EB%AA%85%ED%95%A8%EC%88%98%EC%9D%98%20%EC%B0%A8%EC%9D%B4&f=false)


