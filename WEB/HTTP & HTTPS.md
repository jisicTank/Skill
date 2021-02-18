# HTTP와 HTTPS의 차이

#### **웹 동작 방식**

![3](https://user-images.githubusercontent.com/24764210/108320104-b1e65f80-7205-11eb-8d0e-ee952fbaa7f8.PNG)

- **TCP/IP**: Transmission Control Protocol (전송 제어 규약) 과 Internet Protocol (인터넷 규약) 은 데이터가 어떻게 웹을 건너 여행해야 하는지 정의하는 통신 규약이다.  패킷을 보낸 순서와 받는 순서를 보증하지 않는 IP(인터넷 프로토콜)와 전송 순서를 조절해주는 TCP의 결합을 말한다.

  예시) 차 또는 자전거같은 운송장치 역할

- **DNS**: Domain Name System Servers (도메인 이름 시스템 서버) 는 웹사이트를 위한 주소록과 같다. 사용자가 브라우저에 웹 주소를 입력할 때, 브라우저는 그 웹사이트를 검색하기 전에 DNS 를 살펴본다. 브라우저는 HTTP 메시지를 올바른 장소로 전송하기 위해 그 웹사이트가 있는 서버가 어떤것인지 찾아야 하기 때문이다.

  예시) 상점의 주소를 찾아보는 것

- **HTTP**: Hypertext Transfer Protocol (하이퍼텍스트 전송 규약) 은 텍스트 기반의 통신 규약으로 인터넷에서 데이터를 주고받을 때 이 규약에 맞춰 정보를 교환할 수 있는 프로토콜이다. 즉, Hypertext인 HTML을 전송하기 위한 통신규약(= 통신 형식 = 통신 구조)이다.

  예) 상품을 주문하기 위해 사용하는 언어

- **웹 서버**: 웹 브라우저와 같은 사용자로부터 HTTP를 요청받아 사용자에게 HTML, CSS, JavaScript를 포함한 문서를 전송해주는 서버이다.

<br />

<br />

#### **HTTP와 HTTPS 차이**

![4](https://user-images.githubusercontent.com/24764210/108331008-aac54e80-7211-11eb-8896-a00fbf58ce20.PNG)

TCP/IP 특성상 암호화를 하지 않기 때문에도청이 가능하고 통신 상대를 확인하지 않기 때문에 위장이 가능하다.

그래서 HTTP 메시지를 암호화(SSL,TLS)했는데 이것이 HTTPS이다.

즉, HTTPS는 보안이 강화된 HTTP이다. 

기존 HTTP는 TCP와 직접 통신했지만, HTTPS는 HTTP와 TCP 사이에 SSL, TLS가 끼워져 있다.

-  SSL : 클라이언트와 서버간의 통신을 제3자가 보증해주는 전자화된 보안인증서. 클라이언트가 서버에 접속한 직후에 서버는 클라이언트에게 이 인증서 정보를 전달한다. 클라이언트는 이 인증서 정보가 신뢰할 수 있는 것인지를 검증 한 후에 다음 절차를 수행한다.
- TSL : SSL의 다음 버전. 보안이 더 강화되었으나 보통 SSL이라는 명칭을 주로 쓴다.

<br />

### 면접 질문!

Q. HTTP와 HTTPS의 차이점을 설명하시오.

HTTP : 인터넷 상에서 클라이언트와 서버 간에 요청/응답으로 데이터를 주고받을 수 있는 프로토콜로 Hypertext인 HTML을 전송하기 위한 통신규약이다.

HTTPS : HTTP에 SSL, TSL과 같은 보안 인증서로 암호화한 것이다.

<br />

<br />

<br />

[자료 출처]

https://developer.mozilla.org/ko/docs/Learn/Getting_started_with_the_web/%EC%9B%B9%EC%9D%98_%EB%8F%99%EC%9E%91_%EB%B0%A9%EC%8B%9D

https://velog.io/@kyo3553/Web-01-%EB%8F%99%EC%9E%91-%EA%B3%BC%EC%A0%95

https://brunch.co.kr/@wangho/6