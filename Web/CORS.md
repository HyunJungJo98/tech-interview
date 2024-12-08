# CORS

Cross-Origin-Resource-Sharing의 약자로, 교차 출처 리소스 공유라는 의미이다.

![출처 : https://docs.tosspayments.com/resources/glossary/cors](https://github.com/user-attachments/assets/dc1fc6cc-1a98-42e9-a4f1-0a058dbeb23e)

출처 : https://docs.tosspayments.com/resources/glossary/cors

여기서 말하는 출처는 프로토콜, 도메인(호스트 이름), 포트로 구성되며 이 중 하나라도 다르면 CORS 에러를 만나게 된다.

- SOP : 서로 다른 출처일 때 리소스 요청과 응답을 차단하는 정책
- CORS : 서로 다른 출처이더라도 리소스 요청과 응답을 허용할 수 있도록 하는 정책

# CORS 에러 대응

1. 서버에서 `Access-Control-Allow-Origin` 응답 헤더 설정하기

   해당 헤더를 이용하여 요청을 수락할 출처를 명시적으로 지정한다.

2. 프록시 서버 사용하기
   - [`http://example.com`](http://example.com) 이라는 주소의 웹 애플리케이션이 [`http://api.example.com`](http://api.example.com) 이라는 리소스에서 데이터를 요청하는 상황을 가정한다.
   - 웹 애플리케이션이 직접적으로 리소스에 요청하는 대신 [`http://example-proxy.com`](http://example-proxy.com) 이라는 프록시 서버에 요청을 보낸다.
   - 프록시 서버가 [`http://api.example.com`](http://api.example.com) 으로 요청을 전달하고 응답을 다시 웹 애플리케이션에 반환한다.

# 참고

- https://docs.tosspayments.com/resources/glossary/cors
