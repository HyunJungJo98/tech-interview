자바스크립트는 프로토타입 기반 언어이다. 프로토타입을 이용하여

객체 지향 언어의 클래스를 흉내낼 수 있다.

# 프로토타입 객체

## 프로토타입 객체의 생성과 멤버

`함수` 가 정의되고 파싱 단계에 들어가면 내부적으로 수행되는 작업이 있다.

**첫 번째, 해당 함수에 Constructor(생성자) 자격 부여**

Constructor 자격이 부여되면 new를 통해 객체를 만들어낼 수 있게 된다. 따라서 함수만 new 키워드를 사용할 수 있다.

**두 번째, 해당 함수의 Prototype Object(프로토타입 객체) 생성 및 연결**

`함수` 의 멤버로 `프로토타입 속성` 이 있다. 이 `프로토타입 속성` 은 함수 이름으로 되어있는 `프로토타입 객체`를 참조한다. `프로토타입 객체` 는 `constructor` 속성을 멤버로 가지고 있다. 이 `constructor` 는 `함수` 를 참조한다.

![image](https://github.com/user-attachments/assets/5372bab8-db49-49f7-b2ac-5058052266d7)

```jsx
function Person() {}
```

`Person 함수` 가 정의되고 파싱 단계에 들어가면 `Person 함수` 의 `Prototype` 속성은 `Person 프로토타입 객체` 를 참조한다. `Person 프로토타입 객체` 의 멤버인 `constructor` 는 `Person 함수` 를 참조한다.

만약 new 연산자를 통해 Person 함수를 원형으로 하는 객체들이 만들어졌다면, 이 객체들은 모두 `Person 프로토타입 객체` 를 참조한다.

![image](https://github.com/user-attachments/assets/a5663afd-dab7-46e9-933b-cadd2acb2fb5)

```jsx
function Person() {}

let joon = new Person();
let jisoo = new Person();
```

그렇다면 이 프로토타입 객체는 무엇인가?

## 프로토타입 객체란?

함수를 정의했을 때 생성되는 객체로, 자신이 다른 객체의 원형이 되는 객체이다. 기본적인 속성으로 `constructor` 와 `__proto__` 를 가지고 있다.

프로토타입 객체도 런타임에 동적으로 속성을 추가할 수 있으며, 같은 프로토타입 객체를 가진 모든 객체는 해당 속성을 공통으로 사용할 수 있다.

```jsx
function Person() {}

let joon = new Person();
let jisoo = new Person();

Person.prototype.eyes = 2;

console.log(joon.eyes); // 2
console.log(jisoo.eyes); // 2
```

프로토타입 객체에 멤버를 추가, 수정, 삭제할 때는 함수 안의 prototype 속성을 사용해야 한다.

```jsx
function Person() {}

let joon = new Person();
let jisoo = new Person();

joon.age = 25;

console.log(joon.age); // 25
console.log(jisoo.age); // undefined
```

# 프로토타입

자바스크립트에서는 기본 데이터 타입(boolean, number, string)을 제외한 모든 것이 객체이다.(특별한 값인 null, undefined도 제외한다.) 객체는 자신을 만드는 데에 사용된 원형인 프로토타입 객체를 이용하여 만들어진다. 이때 만들어진 객체 안에 `__proto__` 속성이 자신을 만들어낸 원형을 의미하는 프로토타입 객체를 참조하는 숨겨진 링크가 있다. 이 숨겨진 링크를 프로토타입이라고 정의한다.

![image](https://github.com/user-attachments/assets/dccf3e29-f998-429a-ab87-a57ca167334e)

```jsx
function Person() {}

let joon = new Person();
```

![image](https://github.com/user-attachments/assets/78b1d6e1-80dd-4416-8d62-bf2359a76959)

여기서 `joon` 은 함수가 아닌 인스턴스이기 때문에 prototype 자체가 존재하지 않는다.

![image](https://github.com/user-attachments/assets/e91ffe47-6bf6-4963-8cfb-75c5b2599f92)

# 프로토타입 체인(chain)

```jsx
function Person() {}

let joon = new Person();

Person.prototype.eyes = 2;

console.log(joon.eyes); // 2
```

`joon` 객체는 eyes를 직접 가지고 있지 않기 때문에 eyes 속성을 찾을 때까지 상위 프로토타입을 탐색한다. 최상위인 객체의 프로토타입 객체까지 도달했는데도 찾지 못했을 경우 undefined를 반환한다.

이렇게 `__proto__` 속성을 통해 상위 프로토타입과 연결되어 있는 형태를 프로토타입 체인이라고 한다.

![image](https://github.com/user-attachments/assets/4e18982d-ecb5-4350-950c-c07c84ceaac0)

이러한 구조 때문에 모든 객체는 Object의 자식이라고 불리고, Object Prototype Object에 있는 모든 속성을 사용할 수 있다.

Object Prototype Object의 대표적인 속성으로 toString 함수가 있다. 프로토타입 체이닝 덕분에 아무 변수에 바로 toString 함수를 적용할 수 있다.

```jsx
joon.toString();
```

![image](https://github.com/user-attachments/assets/db765a23-ba83-42c1-b51c-a9673d2961ce)

# 참고

- https://www.nextree.co.kr/p7323/
- [https://inpa.tistory.com/entry/JS-📚-Prototype-완전-정복-❗](https://inpa.tistory.com/entry/JS-%F0%9F%93%9A-Prototype-%EC%99%84%EC%A0%84-%EC%A0%95%EB%B3%B5-%E2%9D%97)
