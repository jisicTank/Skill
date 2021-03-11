



# REST API

### API (Application Programming Interface)

<img src="https://user-images.githubusercontent.com/24764210/110079703-c8c3af00-7dcc-11eb-8799-6adf85707e97.png" alt="API-쉽게-알아보기" style="zoom: 80%;" />

> **특정 서버에 접속해서 그 안에 있는 데이터와 서비스를 이용할 수 있게 해주는 소프트웨어 도구**
>
> 응용 프로그램(내가 만든 서비스)에서 사용할 수 있도록, 운영 체제나 프로그래밍 언어(카카오 지도정보, 날씨 정보)가 제공하는 기능을 제어할 수 있게 만든 인터페이스 즉, 프로그램 코드들끼리 서로 소통하도록 도와주는 인터페이스

- `인터페이스` : 컴퓨터 시스템끼리 정보를 교환하는 공유경계

<br>

**API의 기능**

1. 서버와 데이터베이스에 대한 출입구 역할 : 허용된 사람들에게만 접근성을 부여
2. 애플리케이션(어플 or 프로그램)과 기기가 데이터를 원활하게 주고받을 수 있도록 돕는 역할 
3. 모든 접속을 표준화 : 모든 접속을 표준화하기 때문에 기계/운영체제 등과 상관없이 누구나 동일한 액세스를 얻을 수 있다.

<br>

---

### **RESTful API란?**

> REST 아키텍처 스타일을 따르는 API
>
> REST API 설계 가이드에 따라 API를 만들어서 웹 서비스를 제공하면 해당 웹 서비스는 **RESTful하다**고 합니다.
>
> REST : 웹을 위한 아키텍쳐 스타일

`아키텍쳐` : 제약조건의 집합

<br>

---

### **REST API (Representational State Transfer API)**

> **네트워크를 통해서 컴퓨터들끼리 통신할 수 있게 해주는 아키텍처(서비스의 동작 원리) 스타일**
>
> **URI와 HTTP 메소드를 이용해 서버의 객체화된 서비스(json)에 접근하는 것.**
>
> 
>
> 웹상에서 사용되는 여러 리소스를 **HTTP URI로 표현**하고, 해당 리소스에 대한 행위를 **HTTP Method로 정의**하는 **방식**
>
> 자원(resource)의 표현(representation)에 의한 상태 전달(Transfer) 
>
> : 자원을 이름으로 구분하여 해당 자원의 상태(정보)를 주고 받는 것을 의미

<br>

**REST API 구조** (설계 가이드)

- 자원(Resource) : URI

  - HTTP 메소드가 동사를 표현하므로 URI의 모든 것(Resource)은 **명사**로 표현

  - URI 마지막 문자로 슬래시(/)를 포함하지 않는다.

    ![레](https://user-images.githubusercontent.com/24764210/110667156-55c39980-820d-11eb-90cd-8b912c74e9fe.PNG)

  - 하이픈(-)은 URI 가독성을 높이는데 사용

  - 밑줄(_)은 URI에 사용하지 않는다.

  - 파일 확장자는 URI에 포함시키지 않는다.(.jpg 등) 

    Accept header를 사용한다.

    ```
    GET / members/soccer/345/photo HTTP/1.1 Host: restapi.example.com Accept: image/jpg
    ```

    <br>

- 행위(Verb) : HTTP METHOD(GET, POST, PUT, DELETE)

  | METHOD | 역할                                                         |
  | :----: | :----------------------------------------------------------- |
  |  POST  | POST를 통해 해당 URI를 요청하면 리소스를 생성합니다.         |
  |  GET   | GET를 통해 해당 리소스를 조회합니다. 리소스를 조회하고 해당 도큐먼트에 대한 자세한 정보를 가져온다. |
  |  PUT   | PUT를 통해 해당 리소스를 수정합니다.                         |
  | DELETE | DELETE를 통해 리소스를 삭제합니다.                           |

  <br>

- 표현(Represetation of resource) : 데이터의 포맷이 있음(Json, xml, text, ...)

  ```
  HTTP POST , http://localhost:8080/insertBoardInfo
  
  {
  
      "boardVO":{
  
      "title":"제목",
  
      "content":"내용"
  
      }
  
  }
  ```

  <br>

<br>

**URI 과 URL의 차이점은?**

![URI](https://user-images.githubusercontent.com/24764210/109989626-03d1ce00-7d4c-11eb-8d8b-b094331f9ec7.jpg)

URL은 Uniform Resource Locator로 인터넷 상 자원의 위치를 의미합니다. 자원의 위치라는 것은 결국 어떤 파일의 위치를 의미합니다. 반면에 URI는 Uniform Resource Identifier로 인터넷 상의 자원을 식별하기 위한 문자열의 구성으로, URI는 URL을 포함하게 됩니다. 그러므로 URI가 보다 포괄적인 범위라고 할 수 있습니다.

<br>

<br>

**REST의 특징**

**1. Uniform Interface(일관된 인터페이스)**

HTTP 표준만 맞으면 어떤 언어나 플랫폼(C, Java, Python, IOS, 네이버, 카카오톡, 구글, 페이스북 등)에서나 사용이 가능하다. 보통 REST API의 정의를 HTTP + JSON으로 한다.

`플랫폼` : 프로그램을 작동 시킬 때 기반이 되는 환경

<br>

 **2. Stateless(무상태성)**

Rest API는 세션정보나 쿠키정보와 같은 상태정보를 저장 및 관리하지 않으므로 상태 정보를 유지하지 않는다. 각 요청이 분리되어 있고 서로 연결되어 있지 않다.

<br>

 **3. Cacheable(캐시 가능)**

Rest API는 결국 HTTP라는 기존의 웹표준을 그대로 사용하기 때문에, 웹의 기존 인프라를 그대로 활용할 수 있습니다. 그러므로 Rest API에서도 캐싱 기능을 적용할 수 있는데, HTTP 프로토콜 표준에서 사용하는 Last-Modified Tag 또는 E-Tag를 이용하여 캐싱을 구현할 수 있고, 이것은 대량의 요청을 효울척으로 처리할 수 있게 도와줍니다.

- `캐시` : 웹 캐시는 자주 쓰이는 문서의 사본을 자동으로 보관하는 HTTP 장치이다. 웹 요청이 캐시에 도착했을 때, 캐시된 로컬 사본이 존재한다면, 그 문서는 원 서버가 아니라 그 캐시로부터 제공된다.
- `E-Tag` : 브라우저가 캐시된 파일을 이용할 것인지 아니면 서버로부터 다시 가져와야할지을 결정하게 하는 헤더

<br>

 **4. Client-Server Architecture (서버-클라이언트 구조)**

요청이 HTTP를 통해 관리되는 클라이언트-서버 아키텍처이다.

<br>

★ **5. Self-Descriptiveness(자체 표현)**

Rest API는 ''메세지''만 보고도 이를 쉽게 이해할 수 있는 자체 표현 구조로 되어있다. 아래와 같은 JSON 형태의 Rest 메세지는 게시글의 id와 제목을 전달하고 있음을 손쉽게 이해할 수 있다.

서버나 클라이언트가 변경되더라도 오고가는 메시지는 언제나 self-descriptive하므로 언제나 해석이 가능하다.

- Content-Type : Media type을 명시
- profile link relation

```json
GET /todos HTTP/1.1
Host: example.org

HTTP/1.1 200 OK
★Content-Type: application/vnd.todos+json
★Link: <https://example.org/docs/todos>; rel="profile"
{
	{"id": 1, "title": "집에 가기"},
	{"id": 2, "title": "회사 가기"}
}
```

<br>★**6. HATEOAS** 

애플리케이션의 상태는 Hyperlink를 이용해 전이되어야한다.

- data에 하이퍼링크를 표현

```json
GET /todos HTTP/1.1
Host: example.org

HTTP/1.1 200 OK
★Content-Type: application/vnd.todos+json
Link: <https://example.org/docs/todos>; rel="profile"
{
	{★"link": "https://example.org/docs/todos/1", "title": "집에 가기"},
	{"id": "https://example.org/docs/todos/2", "title": "회사 가기"}
}
```

- HTTP 헤더(Link, Location)로 링크를 표현
```json
POST /todos HTTP/1.1
Content-Type: application/json
{
	{"title": "집에 가기"}
}

HTTP/1.1 200 OK
★Location: /todos/1
★Link: </todos/>; rel="collection"
```

<br>

### Q. 면접 질문

#### API 란?

 특정 서버에 접속해서 그 안에 있는 데이터와 서비스를 이용할 수 있게 해주는 소프트웨어 도구로 두 개의 소프트웨어가 서로 통신을 주고받을 때, 접근성을 제어하고 모든 접속을 표준화하여 기계나 운영체제에 상관없이 동일한 액세스가 가능하도록 한다.

<br>

#### RESTful API란?

REST API 설계 가이드를 따라 API를 만든것이다.

<br>

#### REST란?

네트워크를 통해서 컴퓨터들끼리 통신할 수 있게 해주는 아키텍처 스타일로 **정보의 자원을 표현**하는 URI와 **자원에 대한 행위를 표현**하는HTTP 메소드로 설계해서 서버의 서비스에 접근하며 주로 json형태의 데이터 포맷을 사용한다. 

**self-descriptive**와 **HATEOAS**를 만족시켜야 진정한 REST이다.  





[자료 출처]

https://dydrlaks.medium.com/api-%EB%9E%80-c0fd6222d34c

https://meetup.toast.com/posts/92

http://blog.wishket.com/api%EB%9E%80-%EC%89%BD%EA%B2%8C-%EC%84%A4%EB%AA%85-%EA%B7%B8%EB%A6%B0%ED%81%B4%EB%9D%BC%EC%9D%B4%EC%96%B8%ED%8A%B8/

https://blog.naver.com/leejjoo112/222236457178

https://blog.naver.com/pjok1122/221610282758

https://sarc.io/index.php/miscellaneous/749

https://blog.npcode.com/2017/04/03/rest%EC%9D%98-representation%EC%9D%B4%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%B8%EA%B0%80/

https://gmlwjd9405.github.io/2018/09/21/rest-and-restful.html

https://meetup.toast.com/posts/92

http://blog.wishket.com/soap-api-vs-rest-api-%EB%91%90-%EB%B0%A9%EC%8B%9D%EC%9D%98-%EA%B0%80%EC%9E%A5-%ED%81%B0-%EC%B0%A8%EC%9D%B4%EC%A0%90%EC%9D%80/

https://velog.io/@taeha7b/api-restapi-restfulapi