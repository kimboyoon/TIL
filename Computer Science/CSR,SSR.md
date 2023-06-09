웹 페이지를 렌더링 하는 방식에는 CSR, SSR 두가지 방식이 있다.

# CSR 

- Client Side Rendering
- 클라이언트 즉 브라우저에서 웹페이지를 렌더링 하는 것

<img width="600" src="../Images/CSR.png" alt="CSR">

## 동작 방식

1. 사용자가 웹 페이지를 방문하면 CDN이 HTML파일과 JS로 접근할 수 있는 링크를 클라이언트로 보낸다. 아무것도 화면에서 볼 수 없는 상태.

    - CDN : 유저의 요청에 `물리적으로` 가까운 서버에서 요청에 응답하는 방식

2. 브라우저는 HTML과 JS를 다운로드한다.

3. 다운로드가 완료된 JS가 실행되고, API 요청을 수행한다. 유저는 `placeholders`를 보게 된다.

4. 서버가 API 요청에 응답한다.

5. API로부터 받아온 데이터를 `placeholders` 자리에 넣어준다. 이 단계에서 유저는 **화면을 볼 수 있고 상호작용하는 상태**가 된다.

6. 사용자가 페이지를 이동할 때 서버에 추가적으로 `HTML` 파일을 요청하지 않고 이미 받은 자바스크립트를 이용하여 렌더링한다.



# SSR

- Server Side Rendering
- 서버의 HTML로 렌더링하는 방식

<img width="600" src="../Images/SSR.png" alt="SSR">

## 동작 방식

1. 사용자가 웹 페이지를 방문하면 서버는 즉시 렌더링 가능한 HTML 파일을 만든다.

2. 클라이언트에 전달하는 순간 이미 렌더링 준비가 되었기 때문에 HTML이 즉시 렌더링 된다. 이 단계에서 사용자는 **화면을 볼 수 있게** 된다. (조작은 할 수 없는 상태)

3. 브라우저에서 JS 파일을 다운로드 한다.

4. 다운로드 받는 사이에 사용자의 조작을 기억한다.

5. 브라우저가 JS 프레임워크를 실행한다.

6. JS까지 성공적으로 컴파일 되면 기억하고 있던 사용자 조작이 실행되고 **상호작용이 가능**해진다.

7. 사용자가 페이지를 이동할 경우, 위 동작을 반복한다.



# CSR vs SSR

1. 로딩하는 시간 

- 첫페이지 로딩시간
    - SSR이 빠르다.

- 나머지 로딩시간
    - CSR이 빠르다. (처음에 이미 다 받아놨기 때문)

2. SEO

- SSR이 용이하다.
    - 검색엔진은 자동화된 로봇인 `크롤러`로 웹 사이트를 읽는다. CSR은 JS를 실행시켜야 동적으로 컨텐츠가 생성되므로 JS가 실행되어야 크롤러가 읽을 수 있다.
    - BUT, SSR은 애초에 서버에서 컴파일되어 넘어오기 때문에 크롤러에 대응하기 용이하다.

3. 서버 자원 사용

- SSR이 서버 자원을 더 많이 사용한다. 
    - 매번 서버에 요청하기 때문


# 언제 뭐를 사용해야해?

1. CSR을 사용하자!
    - 네트워크가 빠를 때
    - 서버의 성능이 좋지 않을 때
    - 사용자에게 보여줘야 하는 데이터의 양이 많을 때 (로딩창을 띄울 수 있다)
    - 메인스크립트가 가벼울 때
    - SEO 관심없을 때
    - 사용자와 상호작용할 것들이 많을 때 (아예 렌더링되지 않아서 사용자의 행동을 막는 것이 유리하다)

2. SSR을 사용하자!
    - 네트워크가 느릴때 (페이지마다 나눠서 불러오니까)
    - SEO 필요할 때
    - 최초 로딩이 빨라야하는 사이트를 개발할 때
    - 메인스크립트가 크고 로딩이 느릴 때 (SSR은 한번의 요청에 렌더가 가능한 페이지가 돌아오니까. CSR은 메인스크립트가 로딩이 끝나면 API로 데이터 요청을 또 보낸다)
