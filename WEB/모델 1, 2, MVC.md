# 모델 1, 2, MVC

### 모델 1

> 뷰와 로직을 모두 JSP 페이지 하나에서 처리하는 구조

구성 요소 : **JSP / 자바빈 or 서비스 클래스**

![2650294B56C1BFD515](https://user-images.githubusercontent.com/24764210/114018002-b7783180-98a7-11eb-8d3f-acbff4ac488f.gif)

 JSP 페이지 내에 로직 처리를 위한 자바 코드와 출력을 위한 코드가 함께 섞여 삽입된다. 브라우져에서 요청이 들어오면 JSP 페이지는 자신이 직접 자바빈이나 따로 작성한 서비스 클래스를 이용하여 작업을 처리하고, 그 처리한 정보를 클라이언트에 출력한다. 과거에 가장 많이 사용되었던 아키텍쳐로, 간단한 페이지를 구성할 때 많이 사용된다.

```jsp
<%
	String num = request.getParameter("n");
	...
	if(num%2 != 0)
        model = "홀수";
	else
        model = "짝수";
%>
...
<%=model%>입니다.
```



![222](https://user-images.githubusercontent.com/24764210/114019829-d8418680-98a9-11eb-935f-4c9667817e9d.PNG)

** 자바빈 설명 : https://github.com/jisicTank/Skill/blob/master/WEB/%EC%9E%90%EB%B0%94%EB%B9%88(Java%20Bean).md





### 모델 2

> JSP페이지와 서블릿, 그리고 로직을 위한 클래스가 나뉘어 브라우저 요청을 처리하는 구조

구성 요소 : **서블릿 / JSP / 자바빈 or 서비스 클래스**



![img](https://t1.daumcdn.net/cfile/tistory/2612494F56C1C51932)

요청이 들어오면 요청에 대한 로직 처리는  모델(Model)인 서비스클래스 혹은 자바빈이 담당하고, 요청 결과는 유저에게 결과를 보여줄 뷰(View)단인 JSP에 출력되며, 이를 위한 모든 흐름 제어는 컨트롤러(Controller)인 서블릿에서 담당한다.

![333](https://user-images.githubusercontent.com/24764210/114019833-d8da1d00-98a9-11eb-9c78-2cacbca3b7d3.PNG)









### MVC 패턴

> 모델 2 구조란 MVC(Model-View-Controller) 패턴을 웹 개발에 도입한 구조이며. 모델 2와 MVC 패턴의 형태는 완전히 같은 형태를 가진다.

![994B9C4B5B9690BA33](https://user-images.githubusercontent.com/24764210/114018063-ca8b0180-98a7-11eb-9ad5-843ddceb0627.png)

- 모델 : 비즈니스와 관련된 로직만 처리한다. 비즈니스 로직을 처리가 가능 하다면 모델이 될 수 있다.
- 뷰 : 사용자에게 알맞는 화면을 보여주는 역할이다.
- 컨트롤러 : 사용자의 입력 처리와 흐름 제어를 담당한다. 사용자의 요청에 대해서 알맞은 모델을 사용하고 사용자에게 보여줄 뷰를 선택하면된다.

![11](https://user-images.githubusercontent.com/24764210/114019455-6406e300-98a9-11eb-93c5-d8390f307d1a.PNG)

모델 2는 규모가 큰 프로젝트나 업데이트가 빈번한 프로젝트엔 용이. 유지보수 작업이 쉬워지고 어플리케이션을 쉽게 확장할 수 있다.
모델 1은 규모가 많이 크지 않고 업데이트가 적은 프로젝트일 경우에 용이. 쓸데없이 복잡한 형태로 인해 작업량이 늘어나지 않는다. 



### MVC 흐름

<img src="https://user-images.githubusercontent.com/24764210/114033977-bc91ac80-98b8-11eb-9e98-b1c6979e4995.png" alt="991833505B96952434" style="zoom: 50%;" />

- 해당 서블릿이 끝날 때까지 결과값(정보)은 request 객체에 담겨져서 보내진다.



forward : 현재 작업한 내용을 이어갈 수 있도록 무언가를 공유하는 것

![다운로드 (1)](https://user-images.githubusercontent.com/24764210/114130593-e344f700-993b-11eb-8c6d-e21b6519d98b.png)

redirect : 현재 작업하던 내용과 상관없이 새로운 요청을 하게 만드는 것

코드 예시 : https://pjh3749.tistory.com/117