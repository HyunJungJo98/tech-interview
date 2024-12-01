# OAuth

구글, 페이스북, 트위터와 같은 다양한 플랫폼의 특정한 사용자 데이터에 접근하기 위해 제 3자 클라이언트(우리 서비스)가 사용자의 **접근 권한을 위임**받을 수 있는 표준 프로토콜이다.

즉, 우리 서비스 유저의 타사 플랫폼 정보에 접근하기 위해 타사 플랫폼으로부터 접근 권한을 위임받는 것이다.

# 필요성

- 다양한 클라이언트 기기들의 인증을 간단히 할 수 있다.
- 직접 ID, Password를 입력받아 우리 서비스의 회원으로 만들 수도 있겠지만, 이런 방식은 데이터 관리와 보안 측면에서 부담스러울 수 있다.

# 구성 요소

- **Resource Owner(사용자)** : 웹 서비스를 이용하려는 유저, 자원을 소유하는 자
- **Client(소비자)** : 자사 또는 개인이 만든 애플리케이션 서버
- **Authorization Server** : 권한을 부여해주는 서버
  - 사용자는 이 서버로 ID, PW를 넘겨 Authorization Code를 발급 받을 수 있다.
  - Client는 이 서버로 Authorization Code를 넘겨 Token을 발급 받을 수 있다.
- **Resource Server(서비스 제공자)** : 사용자의 개인 정보를 가지고 있는 애플리케이션
  ex) 네이버, 카카오, 구글
  - Client는 이 서버로 Token을 넘겨 개인 정보를 응답 받을 수 있다.
- **Access Token** : 자원에 대한 접근 권한을 Resource Owner가 인가하였음을 나타내는 자격증명
- **Refresh Token** : Client는 Authorization Server로 부터 access token(비교적 짧은 만료기간을 가짐) 과 refresh token(비교적 긴 만료기간을 가짐)을 함께 부여 받는다.
  access token은 보안상 만료 기간이 짧고, 만료되면 사용자는 다시 로그인을 시도해야 한다. refresh token을 통해 access token을 재발급 받아 재 로그인할 필요 없게 한다.

# 인증 과정

1. 소비자가 서비스 제공자에게 요청 토큰을 요청한다.
2. 서비스 제공자가 소비자에게 요청 토큰을 발급해준다.
3. 소비자가 사용자를 서비스 제공자로 이동시킨다. 여기서 사용자 인증이 수행된다.
4. 사용자가 로그인하면 서비스 제공자가 사용자를 소비자로 이동시킨다.
5. 소비자가 접근 토큰을 요청한다.
6. 서비스 제공자가 접근 토큰을 발급한다.
7. 발급된 접근 토큰을 이용해서 소비자에게 사용자 정보에 접근한다.

# 참고

- https://github.com/gyoogle/tech-interview-for-developer/blob/master/Web/OAuth.md
- [https://inpa.tistory.com/entry/WEB-📚-OAuth-20-개념-💯-정리](https://inpa.tistory.com/entry/WEB-%F0%9F%93%9A-OAuth-20-%EA%B0%9C%EB%85%90-%F0%9F%92%AF-%EC%A0%95%EB%A6%AC)
