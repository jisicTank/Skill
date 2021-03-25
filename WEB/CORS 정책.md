# CORS 정책

### Origin(출처)?

![uri-structure](https://user-images.githubusercontent.com/24764210/112473513-cf34bd80-8db1-11eb-84fc-612a1dad6c7c.png)

**프로토콜, 호스트, 포트**로 구성된 것

출처가 같다는 것은 두 URL의 **프로토콜, 호스트, 포트** 세 개가 모두 같다는 것

![014](https://user-images.githubusercontent.com/24764210/112458610-50835480-8da0-11eb-87ea-ddc54af170ce.PNG)

`요즘 브라우저에서는 PORT 번호가 다르더라도 같은 origin으로 본다.(익스플로러 제외)`



### SOP(Same-Origin Policy, 동일 출처 정책)

어떤 출처(Origin)에서 불러온 문서나 스크립트가 다른 출처에서 가져온 리소스와 상호작용하는 것을 제한하는 보안 방식

→ 같은 출처의 리소스만 가지고 올 수 있도록 하는 보안 정책

 <img src="https://user-images.githubusercontent.com/24764210/112435140-b1eaf980-8d87-11eb-805f-15dab274704d.PNG" alt="sop" style="zoom: 80%;" />

<img src="C:\Users\15U560-GR5PK\Desktop\012.PNG" alt="012" style="zoom: 80%;" />

#### SOP를 사용하는 이유?

XSS, CSRF 위험을 막기 위해서

1. XSS(Corss Site Scripting)
   유저가 웹 사이트에 접속하는 것으로 정상적이지 않은 요청이 클라이언트(웹 브라우저)에서 실행되는 것을 나타내며, Cookie 내에 Session정보를 탈취 당하는 등의 예시가 있다.
2. CSRF(Cross-Site Request Forgeries)
   웹 어플리케이션의 유저가 의도하지 않은 처리를 웹 어플리케이션에서 실행되는 것을 나타내며, 원래는 로그인한 유저 밖에 실행할 수 없는 처리가 멋대로 되는 등의 예시가 있다.



### Cross Domain(크로스 도메인) 이슈

웹 브라우저는 Javascript(JQuery)를 이용하여 AJAX 등을 통해서 다른 도메인의 서버의 URL 을 호출하여 데이터를 가져오는 경우, 보안 문제를 발생시킨다.

만약 우리 웹 서비스에서만 사용하기 위해 다른 서브 도메인을 가진 API 함수를 제공하는 API 서버를 구축하였는데, 다른 웹 서비스에서 이 API 서버에 접근하여 마음대로 API를 호출하여 사용한다면 문제가 될 수 있다.

그래서 Javascript 는 동일 출처 정책(Same Origin Policy) 라는 정책을 두어 다른 도메인의 서버에 요청하는 것을 보안 문제로 간주하고 이를 차단하지만 다른 도메인 간에 통신이 필요한 경우가 있다.

예를 들어, 외부 서버(API서버, 파일(이미지) 서버, 폰트 서버)를 사용해야 할 땐 다른 도메인의 서버로 접근해야 하기 때문에 SOP를 우회해서 서로 다른 도메인 간에 통신을 할 수 있게 해줄 무언가가 필요했다.

그 당시 개발자들이 몇 가지 만든 해결책이 있는데 **JSONP, Reverse Proxy, Flash Socket** 였으나 문제가 많아 표준을 만들었다.





### CORS(Cross-Origin Resource Sharing)의 등장

W3C에서 권장사항으로 CORS 사양 발표

**웹 브라우저에서 외부 도메인 서버와 통신하기 위한 방식을 표준화한 체계**

프로토콜, 호스트, 포트가 다른 서버의 자원 요청이 가능

서버와 클라이언트가 **정해진 헤더**를 통해 서로 요청이나 응답에 반응할 지 결정하는 방식

<img src="https://user-images.githubusercontent.com/24764210/112457371-09e12a80-8d9f-11eb-9b6a-c18ce2b12ef8.PNG" alt="013" style="zoom:67%;" />

<img src="https://user-images.githubusercontent.com/24764210/112454956-94745a80-8d9c-11eb-816a-0126c8d4b33e.png" alt="CORS_principle" style="zoom: 67%;" />







### CORS 시나리오

HTTP 요청 헤더 : Origin 헤더

HTTP 응답 헤더 : Access-Control-Allow-Origin 헤더

두 헤더가 같으면 같은 출처라고 브라우저가 인식한다.

`Access-Control-Allow-Origin : *` 일 때도 서버가 허락했다는 의미이며 모든 클라이언트를 허가한다.

```javascript
app.get('/data', (req, res) => {
    res.header("Access-Control-Allow-Origin", "*");
    res.send(data);
});
```





### CORS의 동작 방식

<img src="https://user-images.githubusercontent.com/24764210/112470578-2d5fa180-8dae-11eb-938c-75ca1931349f.PNG" alt="015" style="zoom: 80%;" />



- Preflight Requests (사전 요청, 예비 요청)

  >  OPTIONS 메소드로 예비요청을 보내고 본 요청을 보낸다.

  실제 요청 전에 인증 헤더를 전송하여 서버의 허용 여부를 미리 체크한다.

  서버에서 승인이 나면 실제 HTTP 요청 메서드를 이용해 실제 요청을 전송한다.

  예비 요청에선 Origin, Access-Control-Request-Headers, Access-Control-Request-Method 를 보낸다.

  요청에 Origin과 응답의 Access-Control-Allow-Origin를 브라우저가 비교해 출처를 판단하여 다르면 에러를 발생시키고 접근할 수 있는 출처라면 본 요청을 보내 요청을 처리한다.

  

  ![123456](https://user-images.githubusercontent.com/24764210/112481416-56862f00-8dba-11eb-9a3d-3d9e847b1221.png)

  서버 사이드 영역이 아닌 브라우저 영역이기 때문에 CORS 정책을 위반하더라도 해당 서버가 같은 출처에서 보낸 요청만 받겠다는 로직을 가지고 있는 경우가 아니라면 서버는 정상적으로 응답(200 코드)을 하고 이후 브라우저가 이 응답을 분석해서 CORS 정책 위반이라고 판단되면 그 응답을 사용하지 않고 그냥 버린다. 

  <img src="https://user-images.githubusercontent.com/24764210/112471734-95fb4e00-8daf-11eb-8348-b5969e8dcf0b.PNG" alt="016" style="zoom:80%;" />
  
  - 다른 도메인에 데이터를 갱신(PATCH)하는 코드
  
    ```javascript
    let response = await fetch('https://site.com/service.json', {
      method: 'PATCH',
      headers: {
        'Content-Type': 'application/json',
      'API-Key': 'secret'
      }
  });
    ```
  
  - 예비 요청 : 브라우저가 자체적으로 Preflight(요청)메세지를 보냄
  
    ```
     OPTIONS /service.json
     Host: site.com
   Origin: https://javascript.info
     Access-Control-Request-Method: PATCH
     Access-Control-Request-Headers: Content-Type,API-Key
    ```
  
  - Preflight 응답
  
    ```
    200 OK
    Access-Control-Allow-Origin: https://javascript.info
    Access-Control-Allow-Methods: PUT,PATCH,DELETE
    Access-Control-Allow-Headers: API-Key,Content-Type,If-Modified-Since,Cache-Control
    Access-Control-Max-Age: 86400
    ```
  
    `Access-Control-Max-Age` 헤더가 응답으로 오면 preflight 허용 여부가 헤더와 함께 캐싱되기 때문에 브라우저는 헤더 값에 명시한 초동안 preflight 요청을 보내지 않는다. 따라서 86400초 동안 preflight 요청을 전송하지 않고 바로 본 요청이 전송된다.
  
  - 본 요청
  
    ```
    PATCH /service.json
    Host: site.com
    Content-Type: application/json
    API-Key: secret
    Origin: https://javascript.info
    ```
  
  - 실제 응답
  
    ```
    Access-Control-Allow-Origin: https://javascript.info
    ```
  
    



- Simple Requests(간단한 요청)

  > CORS 사전 요청을 발생시키지 않는 요청

  요청 메소드는 GET, HEAD, POST 중 하나여야 한다.

  Accept, Accept-Language, Content-Type, DPR, Downlink, Save-Data, Viewport-Width, Sidth를 제외한 헤어를 사용하면 안 된다.

  만약 Content-Type을 사용하는 경우에는 application/x-www-form-urlencoded, multipart/form-data, text/plain만 허용된다.

  <img src="https://user-images.githubusercontent.com/24764210/112474793-65b5ae80-8db3-11eb-9af0-61c70d81fd20.PNG" alt="017" style="zoom:80%;" />

  

- Credential Requests(인증을 이용하는 요청)

  인증된 요청을 사용하는 방법으로 통신에서 좀 더 보안을 강화하고 싶을 때 사용하는 방법

  자바스크립트로 크로스 오리진 요청을 보내는 경우, 기본적으로 쿠키나 HTTP 인증 같은 자격 증명(credential)이 함께 전송되지 않는다.
  
  HTTP 요청의 경우 대개 쿠키가 함께 전송되는데, 자바스크립트를 사용해 만든 크로스 오리진 요청은 예외이다. 
  
  자격 증명을 함께 전송할 수 있으면 사용자 동의 없이 자바스크립트로 민감한 정보에 접근할 수 있게 되는데 그럼에도 불구하고 서버에서 이를 허용하고 싶다면, 자격 증명이 담긴 헤더를 명시적으로 허용하겠다는 세팅을 서버에 해주면 된다.
  
  이때 요청에 인증과 관련된 정보를 담을 수 있게 해주는 옵션이 바로 `credentials` 옵션이다.
  
  <img src="https://user-images.githubusercontent.com/24764210/112494049-0ad98280-8dc6-11eb-89ab-ef55d9f35f86.PNG" alt="018" style="zoom:67%;" />
  
  - `Access-Control-Allow-Origin`에는 `*`를 사용할 수 없으며, 명시적인 URL이어야한다.
  - 응답 헤더에는 반드시 `Access-Control-Allow-Credentials: true`가 존재해야한다.
  
  ![019](https://user-images.githubusercontent.com/24764210/112497639-26925800-8dc9-11eb-92a7-9cefdab6a867.PNG)
  
  - Javascript
  
    ![021](https://user-images.githubusercontent.com/24764210/112498184-a28ca000-8dc9-11eb-851d-179bb19c2270.PNG)
  
  - Request 헤더
  
  ![020](https://user-images.githubusercontent.com/24764210/112497641-27c38500-8dc9-11eb-95a2-cf9c1d54a1a1.PNG)
  
  - Response 헤더
  
    *자격 증명 정보가 담긴* 요청을 서버에서 받아들이기로 동의했다면 서버는 응답에 `Access-Control-Allow-Origin` 헤더와 함께 `Access-Control-Allow-Credentials: true` 헤더를 추가해서 보낸다.
  
    ```
    200 OK
    Access-Control-Allow-Origin: https://techcourse.woowahan.com
    Access-Control-Allow-Credentials: true
    ```
  
    

### 기타 내용

- 서버 개발자는 프론트 개발자를 위해 응답 헤더에 올바른 Access-Control-Allow-Origin이 내려올 수 있도록 세팅해줘야 한다.

  예시) Preflight Requests 헤더 셋팅

  ```java
  public class CorsFilter implements Filter {
      public void init(FilterConfig filterConfig) throws ServletException {}
      
      public void destroy() {}
      
      public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain) throws IOException, ServletException {
      HttpServletResponse httpServletResponse = (HttpServletResponse) response;
      httpServletResponse.setHeader("Access-Control-Allow-Origin", "http://localhost:8088");
      httpServletResponse.setHeader("Access-Control-Allow-Methods", "OPTIONS");
      httpServletResponse.setHeader("Access-Control-Max-Age", "10");
      httpServletResponse.setHeader("Access-Control-Allow-Headers", "content-type");
      chain.doFilter(request, response);
      }
  }
  ```

  

- Spring의 경우 CORS 정책이 이미 셋팅 되어 있기 때문에 따로 설정해주지 않아도 다른 서버와 연결이 가능하다.





### Q. 면접질문

#### CORS란 무엇이며 이것에 대해서 설명해보세요.

CORS는 웹개발을 하다가 흔히 만날 수 있는 이슈입니다. 대개는 프론트엔드 개발시에 로컬에서 API 서버에 요청을 보낼 때 흔하게 발생합니다.

서로 다른 도메인간에 자원을 공유하는 것을 뜻합니다. 대부분의 브라우저에서는 이를 기본적으로 차단하며, 서버측에서 헤더를 통해서 사용가능한 자원을 알려줍니다.

preflight request는 실제 요청을 보내도 안전한지 판단하기 위해 사전에 보내는 요청입니다. OPTIONS 메서드로 요청하며 CORS를 허용하는지 확인합니다. CORS가 허용된 웹서버라면 사용 가능한 리소스를 헤더에 담아 응답합니다.



#### CORS 이슈 해결 방안

Preflight Request, Simple Request, Credential Requests 방식 서술





[자료 출처]

https://ko.javascript.info/fetch-crossorigin

https://evan-moon.github.io/2020/05/21/about-cors/

https://www.youtube.com/watch?v=7iGIfcEsc2g

https://vvshinevv.tistory.com/61