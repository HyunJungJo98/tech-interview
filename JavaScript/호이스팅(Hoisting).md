`hoist` 라는 단어의 사전적 정의는 끌어올리기 라는 뜻이다. 자바스크립트에서는 `var` 키워드로 선언된 모든 **변수 선언**은 호이스트 된다. 호이스트란 변수의 정의가 그 범위에 따라 선언과 할당으로 분리되는 것을 의미한다. 즉, 변수가 함수 내에서 정의되었을 경우, **선언**이 함수의 최상위로, 함수 바깥에서 정의되었을 경우, 전역 컨텍스트의 최상위로 변경이 된다.

# 변수의 호이스팅

```jsx
function getX() {
  console.log(x); // undefined
  var x = 100;
  console.log(x); // 100
}
getX();
```

다른 언어에서는 변수 x를 선언하지 않고 출력하려 한다면 오류를 발생시킬 것이다. 하지만 자바스크립트에서는 `var x;` 를 호이스팅하기 때문에 `undefined` 를 출력한다. 위 코드는 아래 코드와 동일한 작동 순서를 갖는다.

```jsx
function getX() {
  var x;
  console.log(x);
  x = 100;
  console.log(x);
}
getX();
```

**할당은 런타임 과정에 이루어지기 때문에 호이스팅되지 않는다.**

# 함수의 호이스팅

**함수 선언문** 형태로 정의한 함수의 유효범위는 전체 코드의 맨 처음부터 시작한다. 함수 선언이 함수 실행 부분보다 뒤에 있더라도 자바스크립트 엔진이 함수 선언을 끌어올린다. 함수 호이스팅은 함수를 끌어올리지만 변수의 값은 끌어올리지 않는다.

```jsx
foo( );
function foo( ){
  console.log(‘hello’);
};
// console> hello
```

foo 함수를 호이스팅하여 global 객체에 등록시키기 때문에 `hello` 가 제대로 출력된다.

```jsx
foo( );
var foo = function( ) {
  console.log(‘hello’);
};
// console> Uncaught TypeError: foo is not a function
```

함수 표현식으로 함수를 정의했다. 함수 리터럴을 할당하는 구조이기 때문에 호이스팅되지 않으며 런타임 환경에서 Type Error를 발생시킨다.

# var로 선언한 변수 호이스팅

var 키워드는 선언과 함께 `undefined` 로 초기화되어 메모리에 저장된다.

```jsx
console.log(name); // undefined
var name = 'James';
console.log(name); //James
```

따라서 `var name = "James";` 이 작성되기 전 `console.log(name);` 은 `undefined` 로 출력된다.

# const, let으로 선언한 변수 호이스팅

const, let은 선언과 초기화가 동시에 일어나지 않고, 선언만 메모리에 저장된다.

```jsx
console.log(name); // ReferenceError
const name = 'James';
console.log(name); // ReferenceError
let name = 'James';
```

초기화되지 않으면 변수를 참조할 수 없기 때문에 참조 에러를 일으킨다.

```jsx
let foo = 1;
{
  console.log(foo);
  let foo = 2;
}
```

const와 let은 블록 레벨 스코프이기 때문에 블록 내에서는 `foo` 변수가 초기화되지 않은 상태이다.

# TDZ(Temporal Dead Zone)

자바스크립트의 모든 선언에는 호이스팅이 일어난다.

함수 표현식과 const, let, class를 이용한 선언문은 호이스팅이 발생하지 않는 것처럼 동작한다. 하지만 실제로는 호이스팅되어 선언이 끌어올려진 것이 맞다.(선언이 코드 실행 전 메모리에 저장되었다.) 다만 접근만 하지 못하게 된 것이다.

```jsx
console.log(name); // ReferenceError
let name = 'James';
```

여기서 `console.log(name);` 가 작성된 라인, 해당 zone을 일시적으로 죽은 구역이라고 표현한다. `name` 의 선언문이 나오기 전까지는 `name` 에 접근할 수 없다는 의미이다.

# 참고

- https://github.com/JaeYeopHan/Interview_Question_for_Beginner/tree/main/JavaScript#hoisting
- [https://velog.io/@saemileee/Javascript-호이스팅-클로져](https://velog.io/@saemileee/Javascript-%ED%98%B8%EC%9D%B4%EC%8A%A4%ED%8C%85-%ED%81%B4%EB%A1%9C%EC%A0%B8)
- [https://hanamon.kr/javascript-호이스팅이란-hoisting/](https://hanamon.kr/javascript-%ED%98%B8%EC%9D%B4%EC%8A%A4%ED%8C%85%EC%9D%B4%EB%9E%80-hoisting/)
