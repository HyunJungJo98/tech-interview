# 클로저란?

함수가 선언됐을 때의 렉시컬 환경(lexical environment)이다. 즉, 함수가 선언됐을 때의 환경을 저장하여 내부 함수가 외부 함수의 스코프를 접근할 수 있게 해준다.

# 사전 지식

> 💡 **Lexical Environment란?**
>
> 코드를 실행하기 앞서 생성되는 특별한 객체로, 실행할 스코프 범위 안에 있는 변수와 함수를 프로퍼티로 저장하는 객체이다.
>
> 즉, 우리가 소스 코드를 실행하면서 참조가 필요한 변수의 값을 이 Lexical Environment라는 객체에서 식별자 이름을 키로 찾는다.

> 💡 **실행 컨텍스트(execution context)란?**
>
> 실행하고 있는 함수를 트래킹하기 위한 특별한 자료구조이다. 현재 실행하고 있는 함수 내의 현재 변수 상태와 this의 값 등을 저장하고 있고, 현재 실행 중인 line을 기억하고 있다.

# Lexical scoping

함수를 호출할 때가 아니라 함수를 어디에 선언했는지에 따라 스코프가 결정되는 것을 렉시컬 스코핑이라고한다. 따라서 중첩 함수(nested function)에서 내부 함수(inner function)는 부모 함수(parent function)가 return 되었더라도 부모 함수의 스코프를 가지게 된다.

```jsx
function outerFunc() {
  var name = 'Mozilla'; // name은 outerFunc에 의해 생성된 지역 변수이다.
  function innerFunc() {
    // innerFunc() 은 내부 함수이며, 클로저다.
    console.log(name); // 부모 함수에서 선언된 변수를 사용한다.
  }
  innerFunc();
}
outerFunc();
```

`outerFunc` 내에서 지역변수 `name` 과 `innerFunc()` 을 생성한다. `innerFunc()` 은 `outerFunc()` 내부에 정의된 함수이며, `outerFunc()` 함수 내에서만 사용할 수 있다.

이때 `innerFunc()` 의 상위 스코프는 `outerFunc()` , 렉시컬 스코프는 `전역` , `함수 outerFunc` , `자신의 스코프` 이다.

따라서 `innerFunc()` 내부에는 `name` 이라는 지역변수가 없지만, 내부 함수에서는 외부 함수에서의 변수에 접근할 수 있기 때문에 부모 함수인 `outerFunc()` 에 선언된 `name` 에 접근할 수 있다. 만약 `innerFunc()` 이 전역에 선언되었다면 `innerFunc()` 의 상위 스코프는 `전역` 스코프가 된다.

# 참고

- [https://github.com/gyoogle/tech-interview-for-developer/blob/master/Language/[Javascript] Closure.md](https://github.com/gyoogle/tech-interview-for-developer/blob/master/Language/%5BJavascript%5D%20Closure.md)
- https://developer.mozilla.org/ko/docs/Web/JavaScript/Closures
- https://poiemaweb.com/js-closure
