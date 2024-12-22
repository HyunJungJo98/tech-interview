# REST

Representational State Transfer의 약자로, 자원을 이름으로 구분하여 해당 자원의 상태를 주고받는 모든 것을 의미한다.

즉 REST란

1. HTTP URI를 통해 자원을 명시하고,
2. HTTP Method를 통해
3. 해당 자원에 대한 CRUD Operation을 적용하는 것을 의미한다.

> 💡 CRUD 연산이란
>
> Create, Read, Update, Delete를 묶어서 일컫는 말로, REST에서의 CRUD Operation 동작 예시는 다음과 같다.
>
> Create : 데이터 생성(POST) </br>
> Read : 데이터 조회(GET) </br>
> Update : 데이터 수정(PUT, PATCH) </br>
> Delete : 데이터 삭제(DELETE) </br>

# REST의 요소

1. Resource(자원)
   - `http://myservice/users` 와 같은 URI
   - 모든 것을 Resource(명사)로 표현하고 세부 Resource에는 id를 붙임
2. Method(자원에 대한 행위)

   | Method | 의미   | Idempotent |
   | ------ | ------ | ---------- |
   | POST   | Create | No         |
   | GET    | Select | Yes        |
   | PUT    | Update | Yes        |
   | DELETE | Delete | Yes        |

3. Message(자원에 대한 행위의 내용)

   - 메시지 포맷이 존재한다. JSON, XML 등이 있다.(최근에는 JSON을 쓴다.)

   ```
   HTTP POST, http://myservice/users/
   {
   	"users" : {
   		"name" : "terry"
   	}
   }
   ```
