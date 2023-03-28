# RESTful API란?

REST 아키텍처 스타일을 따르는 API

# REST란?

- Representational State Transfer 약자
- 자원을 이름으로 구분하여 해당 자원의 상태(정보)를 주고 받는 모든 것
- 웹의 기존 기술과 HTTP 프로토콜을 그대로 활용하므로 웹의 장점을 최대한 활용할 수 있는 아키텍처 스타일
- 네트워크 상에서 클라이언트와 서버 사이의 통신 방식 중 하나

## 구체적으로 말해봐

- HTTP URI를 통해 Resource를 명시하고, HTTP Method(POST, GET, PUT, DELETE)를 통해 해당 자원에 대한 CRUD를 적용하는 것

    - URI vs URL ?
        - URL(Uniform Resource Locator)은 인터넷 상 자원의 위치를 의미한다. 반면, URI(Uniform Resource Identifier)는 인터넷 상의 자원을 식별하기 위한 문자열의 구성으로 URI가 포괄적인 범위이다.

    - CRUD ?
        - Create(POST), Read(GET), Update(PUT), Delete(DELETE), HEAD

## REST 장점

- HTTP 프로토콜의 인프라를 그대로 사용하므로 별도의 인프라를 구축할 필요가 없다.
- HTTP 표준 프로토콜을 따르는 모든 플랫폼에서 사용 가능
- REST API 메시지가 의도하는 바를 명확하게 나타낸다.
- 서버와 클라이언트의 역할을 명확하게 분리한다.

## REST 단점

- REST에는 표준이 없다. 공식화된 레퍼런스가 없어서 사람마다 해석하는게 다를 수 있다.
- 사용가능한 Method 형태가 제한적이다.


## REST 특징

1. Server-Client (서버-클라이언트 구조)
    각각의 역할이 명확해지고 서로 간 의존성이 줄어든다.
2. Stateless (무상태)
    작업을 위한 상태정보를 따로 저장하고 관리하지 않기 때문에 API 서버는 들어오는 요청만 단순히 처리하면 된다. => 자유도 높고 구현이 단순해짐
3. Cacheable (캐시 처리 가능)
    HTTP 라는 웹 표준을 그대로 사용하므로 웹에서 사용하는 기존 인프라를 그대로 활용 가능
4. Layered System (계층화)
    다중 계층으로 구성될 수 있고 중간매체를 사용할 수 있는 등의 유연한 상태
5. Uniform Interface (인터페이스 일관성)
    특정 언어나 기술에 종속되지 않고 모든 플랫폼에 사용할 수 있다.


# REST API 란?

REST의 원리를 따르는 API로 지켜야 할 규칙이 있다.

## 규칙

1. URI는 동사보다는 명사를, 대문자보다 소문자를 사용
2. 마지막에 슬래시(/)를 포함하지 않는다
3. 언더바(_) 대신 하이픈(-) 사용
4. 파일 확장자는 URI에 포함하지 않는다
5. 행위를 포함하지 않는다

# RESTful 이란?

REST의 원리를 따르는 시스템으로 REST API의 설계 규칙을 올바르게 지킨 시스템을 말한다.

모든 CRUD 기능을 POST로 처리하는 API 혹은 API 설계 규칙을 지키지 않은 API는 REST API를 사용하였지만 RESTful 하지는 못한 시스템이다.