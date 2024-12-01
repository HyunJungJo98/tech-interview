# JWT란

JWT는 웹 표준으로서 두 개체에서 JSON 객체를 사용하여 가볍고 자가수용적(완벽한, 필요한 것들을 모두 충족한)인 방식으로 정보를 안정성 있게 전달해줍니다.

# 등장 배경

전통적인 ‘세션 인증 방식’의 경우 세션 정보를 서버에 저장하기 때문에 서버와 클라이언트 간의 통신 횟수가 많아지고 서버의 과부하를 불러일으킬 수 있다. 이를 해결하기 위해 JWT 토큰이 나오게 되었다.

# 세션 방식과의 차이

세션 방식은 서버에 데이터를 저장한다. 고유의 세션 ID를 발급해서 이 ID를 쿠키에 담아 정보를 주고받는다. 서버에 저장되기 때문에 사용자가 많아지면 서버에 과부하가 걸릴 위험이 크다.

JWT는 필요한 정보를 payload에 담고, 암호화/복호화 데이터를 헤더에 넣어 한 번에 암호화 한다. 서버의 메모리에 따로 저장 공간을 확보할 필요 없이 이 토큰을 클라이언트에게 보내주면 클라이언트는 토큰을 보관하고 있다가 요청을 보낼 때마다 헤더에 토큰을 실어보내면 된다. 서버는 검증 여부만 서버에서 전송하면 되므로 서버에 무리가 덜한다. 하지만 토큰을 탈취 당하면 보안상 문제가 발생할 수 있다.

# 구성요소

`.` 을 구분자로 3가지의 문자열로 구성되어 있다.

aaaa.bbbbb.ccccc의 구조로, 앞부터 헤더(header), 내용(payload), 서명(signature)으로 구성된다.

## 헤더

헤더는 `typ` 과 `alg` 두 가지의 정보를 지니고 있다.

- `typ` : 토큰의 타입을 지정한다. JWT이기에 “JWT”라는 값이 들어간다.
- `alg` : 해싱 알고리즘(암호화 시 사용된 알고리즘 정보)을 지정한다. 기본적으로 HMAC, SHA256, RSA가 사용되면 토큰을 검증할 때 사용되는 signature 부분에서 사용된다.

## 정보(payload)

토큰을 담을 정보가 들어있다. 정보의 한 조각을 클레임(claim)이라고 부르고, 이는 name/value의 한 쌍으로 이루어져 있다. 토큰에는 여러 개의 클레임을 넣을 수 있지만, 너무 많아질 경우 토큰의 길이가 길어질 수 있다.

### 클레임의 종류

1. 등록된(registered) 클레임 : 서비스에서 필요한 정보들이 아닌, 토큰에 대한 정보들을 담기 위해 이름이 이미 정해진 클레임이다. 등록된 클레임의 사용은 모두 선택적이며 이에 포함된 클레임 이름들은 다음과 같다.
   - `iss` : 토큰 발급자(issuer)
   - `sub` : 토큰 제목(subject)
   - `aud` : 토큰 대상자(audience)
   - `exp` : 토큰의 만료 시간(expiration), NumericDate 형식으로 되어있어야 하며 현재 시간보다 이후로 설정되어 있어야 한다.
   - `nbf` : Not before을 의미하며, 토큰의 활성 날짜와 비슷한 개념이다. NumericDate 형식으로 날짜를 지정하며, 이 날짜가 지나기 전까지는 토큰이 처리되지 않는다.
   - `iat` : 토큰이 발급된 시간(issued at), 이 값을 사용하여 토큰의 age가 얼마나 되었는지 판단할 수 있다.
   - `jti` : JWT의 고유 식별자로서, 주로 중복적인 처리를 방지하기 위하여 사용된다. 일회용 토큰에 사용하면 유용하다.
2. 공개(public) 클레임 : 충돌이 방지된(conllision-resistant) 이름을 가지고 있어야 한다. 충돌을 방지하기 위해서는 클레임 이름을 URI 형식으로 짓는다.

   ```
   {
   	"https://chup.tistory.com/jwt_claims/is_admin" : true
   }
   ```

3. 비공개(private) 클레임 : 등록된 클레임도, 공개 클레임도 아닌 클레임이다. 양 측 간에(보통 클라이언트와 서버) 합의 하에 사용되는 클레임 이름들이다. 공개 클레임과는 달리 이름이 중복되어 충돌될 수 있으니 유의해야 한다.

## 서명(signature)

헤더의 인코딩 값과 정보의 인코딩 값을 합친 후 주어진 비밀 키로 해시를 하여 생성한다. 이렇게 만든 해시를 `base64` 형태로 나타낸다.

# 암호화 방식과 보안

JWT는 양방향 암호화이다. 즉, 복호화가 되는 암호화를 사용한다. 따라서 토큰을 해킹당하면 정보를 열람할 수 있기 때문에 중요한 데이터는 JWT 토큰에 넣으면 안 된다.

<aside>
💡 단방향 암호화 : 암호화는 되지만 복호화는 안 된다.(민감한 정보를 저장할 때 사용)
양방향 암호화 : JWT 토큰처럼 복호화가 되는 암호화이다.

</aside>

# 로그인 인증 시 JWT 사용

## Refresh Token의 등장 배경

유효기간이 짧은 토큰을 발급하게 되면 사용자 입장에서 자주 로그인을 해야 하기 때문에 번거롭다. 반대로 유효기간이 긴 토큰을 발급하게 되면 제 3자에게 토큰을 탈취당할 경우 보안에 취약하다는 단점이 있다. 이러한 점을 보완하기 위해 Refresh Token을 사용하게 되었다.

## Refresh Token

Refresh Token은 Access Token과 마찬가지로 JWT이다. Access Token의 유효기간이 만료되었을 때 Refresh Token으로 새로 발급해줄 수 있다.

Refresh Token의 유효기간이 1주, Access Token의 유효기간이 1시간이라고 한다면, 사용자는 Access Token으로 1시간 동안 API 요청을 하다가 시간이 만료되면 Refresh Token을 이용하여 새로운 Access Token을 발급해준다.

이 방법도 Access Token이 탈취당하면 정보가 유출될 수 있지만, 더 짧은 유효기간을 가지기 때문에 탈취 가능성을 낮춘다.

Refresh Token 또한 유효기간이 만료되었다면 사용자는 새로 로그인해야 한다. Refresh Token도 탈취될 가능성이 있기 때문에 적절한 유효기간 설정이 필요하다.

# Access Token + Refesh Token 인증 과정

![](https://github.com/user-attachments/assets/3d3d818c-6492-4f48-8302-9f19ba3f40f7)

출처 : https://tansfil.tistory.com/59

1. 사용자가 로그인한다.
2. 서버에서 회원 DB 값과 비교한다.
3. Access Token과 Refresh Token을 발급한다. 일반적으로 Refresh Token은 회원 DB에 저장해둔다.
4. 사용자는 Refresh Token을 안전한 저장소에 저장 후, Access Token을 헤더에 실어 요청을 보낸다.
5. Access Token을 검증하여 데이터를 보낸다.
6. 시간이 지나 사용자가 Access Token이 만료된 채로 헤더에 실어 요청을 보낸다.
7. 서버는 Access Token이 만료된 것을 확인하고 권한없음 신호로 응답한다.
8. 사용자는 Refresh Token과 Access Token을 함께 서버로 보낸다.
9. 서버는 Access Token이 조작되지 않았는지 확인한 후, Refresh Token과 사용자의 DB에 저장되어 있던 Refresh Token을 비교한다.
10. Token이 동일하고 유효기간이 지나지 않았다면 새로운 Access Token을 발급해준다.
11. 서버는 새로운 Access Token을 헤더에 실어 다시 API 요청을 보낸다.

# 참고

- [https://github.com/gyoogle/tech-interview-for-developer/blob/master/Web/JWT(JSON Web Token).md](<https://github.com/gyoogle/tech-interview-for-developer/blob/master/Web/JWT(JSON%20Web%20Token).md>)
- https://tansfil.tistory.com/59
- https://devjem.tistory.com/13
