클라이언트가 웹서버에게 요청하는 목적 및 그 종류를 알리는 수단을 말한다.

| HTTP Method | 요청 body 유무 | 응답 body 유무 | 안전 | 멱등성(idempotent) | 캐시 |
| ----------- | -------------- | -------------- | ---- | ------------------ | ---- |
| GET         | optional       | O              | O    | O                  | O    |
| HEAD        | X              | X              | O    | O                  | O    |
| POST        | O              | O              | X    | X                  | O    |
| PUT         | O              | O              | X    | O                  | X    |
| PATCH       | O              | O              | X    | X                  | X    |
| DELETE      | X              | O              | X    | O                  | X    |
| CONNECT     | O              | O              | X    | X                  | X    |
| OPTIONS     | optional       | O              | O    | O                  | X    |
| TRACE       | X              | O              | O    | O                  | X    |

- GET
  - 데이터 조회
  - URL(URI) 형식으로 서버 측에 리소스를 요청한다.
- HEAD
  - 메시지 헤더 정보 요청
  - GET과 유사하지만 HEAD는 실제 문서 요청이 아닌 문서에 대한 정보 요청이다. 즉, Resonse 메시지를 받았을 때 Body는 비어있고 Header 정보만 들어있다.
- POST
  - 내용 및 파일 전송을 하기 위함
  - 클라이언트에서 서버로 어떤 정보를 제출하기 위해 사용한다. 요청 데이터를 Body에 담아 웹 서버로 전송한다.
- PUT
  - 데이터 덮어쓰기
  - POST와 유사하나, 기존 데이터를 갱신할 때 사용한다. 데이터가 없으면 POST와 같이 새로 생성한다.
- PATCH
  - 데이터의 일부분만 갱신
  - PUT과 유사하나, 모든 데이터를 갱신하는 것이 아닌 데이터의 일부분만 수정할 때 쓰인다.
- DELETE
  - 데이터 삭제
  - 웹 서버측에 요청한 데이터를 삭제할 때 사용한다.
- CONNECT
  - 클라이언트와 서버 사이의 중간 경유를 위함
  - 보통 Proxy를 통해 SSL 통신을 하고자할 때 사용한다.
- OPTIONS
  - 서버 측 제공 메소드에 대한 질의를 하기 위함
  - 웹 서버 측에서 지원하고 있는 메소드가 무엇인지 알기 위해 사용한다.
- TRACE
  - 요청 데이터가 수신되는 경로를 보기 위함
  - 웹 서버로부터 받은 내용을 확인하기 위해 loop-back 테스트를 할 때 사용한다.

# ❓멱등성

연산을 여러 번 적용하더라도 결과가 달라지지 않는 성질을 의미한다.

- GET : 여러 번 수행하더라도 결과가 달라지지 않으므로 멱등하다.
- PUT : 동일한 데이터를 계속 덮어쓰기 때문에 멱등하다.
- DELETE : 삭제되었다는 사실이 변하지 않으므로 멱등하다.
- POST : 데이터를 새로 생성하거나, 쿼리를 요청하는 경우 동일한 명령이 여러 번 발생되면 결과가 달라진다.
  같은 내용의 요청을 `/payments`로 3번 보내면 `/payments/1`, `/payments/2`, `/payments/3`와 같이 똑같은 데이터를 가진 리소스 3개가 생성된다.
  ex) 결제가 여러 번 됨, 게시글이 여러 번 작성
- PATCH : 데이터의 일부만 수정하기 때문에 멱등성이 보장될 수도 있다.

# 참고

- [https://github.com/gyoogle/tech-interview-for-developer/blob/master/Web/HTTP Request Methods.md](https://github.com/gyoogle/tech-interview-for-developer/blob/master/Web/HTTP%20Request%20Methods.md)
- [https://inpa.tistory.com/entry/WEB-🌐-HTTP-메서드-종류-통신-과정-💯-총정리](https://inpa.tistory.com/entry/WEB-%F0%9F%8C%90-HTTP-%EB%A9%94%EC%84%9C%EB%93%9C-%EC%A2%85%EB%A5%98-%ED%86%B5%EC%8B%A0-%EA%B3%BC%EC%A0%95-%F0%9F%92%AF-%EC%B4%9D%EC%A0%95%EB%A6%AC)
