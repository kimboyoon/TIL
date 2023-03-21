# login 로직

 현재 let's GIT it 서비스는 github에서 code를 받아와서 로그인하고 있음. 
 AccessToken으로만 관리하고 있으며 만기가 30분이나 현재는 제한해두지 않음. 
 localStorage에 개인정보가 담긴 token을 저장하여 탈취가 쉬움.
 결론적으로 현재 방법은 보안에 취약하다는 단점이 있음.

## 기존의 로그인 로직

1. 클라이언트에서 로그인 시도

    => github code를 담아 서버에 post 요청

2. 서버에서 JWT 생성
    
    => 받은 code로 github AccessToken을 받고 유저 정보가 DB에 있는 정보인지 비교. 등록되어 있는 유저면 JWT 생성.

3. AccessToken 반환

4. 클라이언트에서 localStorage에 저장

5. Authorization이 필요한 리소스에 접근할 때마다 header에 담아서 서버에 요청

6. 서버에서는 유효성 검사를 하고 권한을 부여


## 개선한 로그인 로직

Refresh Token과 AccessToken을 같이 사용하여 리팩토링해보자.

### Access Token 과 Refresh Token 

Access Token : 접근에 관여하는 토큰
Refresh Token : 재발급에 관여하는 토큰으로 자동로그인, 로그인 유지할 때 사용됨

Access Token은 탈취의 위험이 있기 때문에 유효기간을 짧게 메모리에 저장한다. 짧은 시간 저장함으로써 보안을 강화했다고 할 수 있지만, 잦은 토큰 만료로 인해 사용자 입장에서 재로그인이 빈번하기 되어 좋은 서비스 환경이라고 할 수는 없다. 따라서 RT와 함께 사용하여 단점을 보완할 수 있다.
Refresh Token은 유효기간을 길게 설정하여 HttpOnly Cookie에 저장한다.

HttpOnly Cookie 는 자바스크립트 환경에서 접근할 수 없으므로 토큰 누출이 되지 않기 때문에 이곳에 저장하는 것을 권한다.

혹시나 AT가 탈취되더라도 유효기간이 짧기 때문에 사용할 수 없다. 또한, 정상적인 클라이언트는 유효기간이 지나더라도 RT를 사용하여 새로운 AT를 생성하여 사용하게 된다.

### Access Token 은 어디에 저장해야 할까?

1. Storage

기존에는 브라우저의 storage에 저장하여 사용했다. 
스토리지에 저장하게 되면 **XXS 공격에 취약** 하다는 단점이 있다. 또한 JS 내에서 글로벌 변수로 읽기/쓰기가 가능하다. 이를 이용하여 API를 위조할 수 있기 때문에 좋지 않다.

2. Cookie

쿠키는 JS로 접근이 불가능하므로 스토리지에 비해 XSS 공격에 덜 취약하다. 또한 `httpOnly` 와 `secure` 옵션을 사용한다면 JS에 있어서 더욱 안전할 수 있다.
쿠키는 CSRF 공격에 취약하다. CSRF 공격을 간단하게 말하자면, 로그인한 상태로 특정 위험한 동작을 하게 만든다는 의미이다. (토큰값 자체를 가져오는 것은 아님)

3. JavaScript private 변수로 저장

React 는 SPA이기 때문에 페이지 이동해도 private 변수를 유지 가능함
but, 새로고침하면 변수가 날아감
추가로 Refresh Token 만 가지고 AT 만들어주는 API 로직 필요

마지막 방법이 CSRF 공격으로부터 안전하고, XSS 노출에 대해서도 조금 더 낫다. 







