# REST API

### API (Application Programming Interface)

![API-쉽게-알아보기](https://user-images.githubusercontent.com/24764210/110079703-c8c3af00-7dcc-11eb-8799-6adf85707e97.png)

> 응용 프로그램(내가 만든 서비스)에서 사용할 수 있도록, 운영 체제나 프로그래밍 언어(카카오 지도정보, 날씨 정보)가 제공하는 기능을 제어할 수 있게 만든 인터페이스 즉, 프로그램 코드들끼리 서로 소통하도록 도와주는 인터페이스
>
> 특정 사이트에서 특정 데이터를 공유할 경우 어떠한 방식으로 정보를 요청해야 하는지, 어떠한 데이터를 제공받은 수 있을지에 대한 규격들
>
> 리소스에 대한 액세스 권한을 제공하고 보안과 제어를 유지할 수 있게 해주며 액세스 권한을 어떻게 누구에게 제공할 지 여부를 결정.

API는 손님(프로그램)이 주문할 수 있게 메뉴(명령 목록)를 정리하고, 주문(명령)을 받으면 요리사(응용프로그램)와 상호작용하여 요청된 메뉴(명령에 대한 값)를 전달한다.

- `인터페이스` : 컴퓨터 시스템끼리 정보를 교환하는 공유경계



**API의 기능**

1. 서버와 데이터베이스에 대한 출입구 역할 : 허용된 사람들에게만 접근성을 부여
2. 애플리케이션(어플 or 프로그램)과 기기가 데이터를 원활하게 주고받을 수 있도록 돕는 역할 
3. 모든 접속을 표준화 





### **REST API (Representational State Transfer API)**

> **URI와 HTTP 메소드를 이용해 객체화된 서비스(json)에 접근하는 것.**
>
> 웹상에서 사용되는 여러 리소스를 **HTTP URI로 표현**하고, 해당 리소스에 대한 행위를 **HTTP Method로 정의**하는 **방식**
>
> 자원(resource)의 표현(representation)에 의한 상태 전달(Transfer) 
>
> : 자원을 이름으로 구분하여 해당 자원의 상태(정보)를 주고 받는 것을 의미

-  어떤 자원에 대해 CRUD(Create, Read, Update, Delete) 연산을 수행하기 위해 URI(Resource)로 요청을 보내는 것
  - CRUD Operation
    - Create(생성) : POST/PUT
    - Read(조회) : GET
    - Update(수정) : PUT
    - Delete(삭제) : DELETE



**REST API 구조**

- 자원(Resource) : URI
- 행위(Verb) : HTTP METHOD(GET, POST, PUT, DELETE)
- 표현(Represetation of resource) : 데이터의 형태(Json, xml, text, ...)

예) /users GET      

​	  /users/{id} GET     

​	  /users PUT



**URI 과 URL의 차이점은?**

![URI](https://user-images.githubusercontent.com/24764210/109989626-03d1ce00-7d4c-11eb-8d8b-b094331f9ec7.jpg)

URL은 Uniform Resource Locator로 인터넷 상 자원의 위치를 의미합니다. 자원의 위치라는 것은 결국 어떤 파일의 위치를 의미합니다. 반면에 URI는 Uniform Resource Identifier로 인터넷 상의 자원을 식별하기 위한 문자열의 구성으로, URI는 URL을 포함하게 됩니다. 그러므로 URI가 보다 포괄적인 범위라고 할 수 있습니다.





### **RESTful API란?**

> REST 아키텍처의 제약 조건을 준수하는 웹 API
>
> REST API 설계 가이드에 따라 API를 만들어서 웹 서비스를 제공하면 해당 웹 서비스는 **RESTful하다**고 합니다.





**REST의 특징**

**1. Uniform Interface(일관된 인터페이스)**

Resource(URI)에 대한 요청을 통일되고, 한정적으로 수행하는 아키텍처 스타일을 의미합니다. 이것은 요청을 하는 Client가 플랫폼(Android, Ios, Jsp 등) 에 무관하며, 특정 언어나 기술에 종속받지 않는 특징을 의미합니다. 이러한 특징 덕분에 Rest API는 HTTP를 사용하는 모든 플랫폼에서 요청가능하며, Loosely Coupling(느슨한 결함) 형태를 갖게 되었습니다.



 **2. Stateless(무상태성)**

서버는 각각의 요청을 별개의 것으로 인식하고 처리해야하며, 이전 요청이 다음 요청에 연관되어서는 안됩니다. 그래서 Rest API는 세션정보나 쿠키정보를 활용하여 작업을 위한 상태정보를 저장 및 관리하지 않습니다. 이러한 무상태성때문에 Rest API는 서비스의 자유도가 높으며, 서버에서 불필요한 정보를 관리하지 않으므로 구현이 단순합니다. 이러한 무상태성은 서버의 처리방식에 일관성을 부여하고, 서버의 부담을 줄이기 위함입니다.



 **3. Cacheable(캐시 가능)**

Rest API는 결국 HTTP라는 기존의 웹표준을 그대로 사용하기 때문에, 웹의 기존 인프라를 그대로 활용할 수 있습니다. 그러므로 Rest API에서도 캐싱 기능을 적용할 수 있는데, HTTP 프로토콜 표준에서 사용하는 Last-Modified Tag 또는 E-Tag를 이용하여 캐싱을 구현할 수 있고, 이것은 대량의 요청을 효울척으로 처리할 수 있게 도와줍니다.

- `캐시` : 웹 캐시는 자주 쓰이는 문서의 사본을 자동으로 보관하는 HTTP 장치이다. 웹 요청이 캐시에 도착했을 때, 캐시된 로컬 사본이 존재한다면, 그 문서는 원 서버가 아니라 그 캐시로부터 제공된다.
- `E-Tag` : 브라우저가 캐시된 파일을 이용할 것인지 아니면 서버로부터 다시 가져와야할지을 결정하게 하는 헤더



 **4. Client-Server Architecture (서버-클라이언트 구조)**

Rest API에서 자원을 가지고 있는 쪽이 서버, 자원을 요청하는 쪽이 클라이언트에 해당합니다. 서버는 API를 제공하며, 클라이언트는 사용자 인증, Context(세션, 로그인 정보) 등을 직접 관리하는 등 역할을 확실히 구분시킴으로써 서로 간의 의존성을 줄입니다.



 **5. Self-Descriptiveness(자체 표현)**

Rest API는 요청 메세지만 보고도 이를 쉽게 이해할 수 있는 자체 표현 구조로 되어있습니다. 아래와 같은 JSON 형태의 Rest 메세지는 http://localhost:8080/insertBoardInfo 로 게시글의 제목, 내용을 전달하고 있음을 손쉽게 이해할 수 있습니다.

```
HTTP POST , http://localhost:8080/insertBoardInfo

{

    "boardVO":{

    "title":"제목",

    "content":"내용"

    }

}
```



 **6. Layered System(계층 구조)**

Rest API의 서버는 다중 계층으로 구성될 수 있으며 보안, 로드 밸런싱, 암호화 등을 위한 계층을 추가하여 구조를 변경할 수 있습니다. 또한 Proxy, Gateway와 같은 네트워크 기반의 중간매체를 사용할 수 있게 해줍니다. 하지만 클라이언트는 서버와 직접 통신하는지, 중간 서버와 통신하는지 알 수 없습니다.





Q. 면접 질문

- API 란?

  : 응용 프로그램에서 사용할 수 있도록 운영체제 혹은 프로그래밍 언어에게 제공하는 인터페이스(규격)

- REST 하다는 건 뭔가?



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

