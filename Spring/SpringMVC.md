# Spring MVC



## 일반적인 MVC Pattern

<img width="523" alt="스크린샷 2021-03-05 오전 12 51 03" src="https://user-images.githubusercontent.com/46706670/109997753-dee15900-7d53-11eb-92cf-2a2662967194.png">



<img width="670" alt="스크린샷 2021-03-05 오전 12 51 34" src="https://user-images.githubusercontent.com/46706670/109997770-e274e000-7d53-11eb-9db7-17de4ba766b1.png">



1. 사용자가 웹사이트에 접속한다
2. Controller는 사용자가 요청한 웹페이지를 제공하기 위해 Model에서 데이터를 호출한다.
3. Model은 데이터베이스나 파일과 같은 데이터 소스를 제어한 후에 그 결과를 리턴한다.
4. Controller는 Model이 return한 결과를 View에 반영한다.
5. 데이터가 반영된 View는 사용자에게 보여진다.

[MVC 모델에서 Service Model의 역할](https://abn-abn.tistory.com/190)

<br><br><br><br>

## Spring MVC

<img width="654" alt="스크린샷 2021-03-05 오전 12 40 52" src="https://user-images.githubusercontent.com/46706670/109997888-0506f900-7d54-11eb-8f41-283c310139a3.png">



<br>

* **DispatcherServlet**

애플리케이션으로 들어오는 모든 Request를 가로채서 받는 관문 Controller. Request를 실제로 처리할 Controller에 전달하고 그 결과값을 받아서 View에게 전달하여 적절한 응답을 생성할 수 있도록 흐름을 제어한다.

> SpringMVC는 DispatcherServlet이 등장함에 따라 web.xml의 역할을 상당히 축소시킴. 기존에는 모든 서블릿에 대해 URL 매핑을 활용하기 위해 모두 web.xml에 등록해주어야 했지만, DispatcherServlet이 해당 애플리케이션으로 들어오는 모든 요청을 핸들링해주면서 작업이 편리해짐. 또, @MVC 를 사용할 수 있음.



* **HandlerMapping**

Request URL이 각각 어떤 Controller method(servlet)이 실제로 처리할 것인지 찾아주는 역할

* **Controller**

Request를 직접 처리(비즈니스 로직)한 후 그 결과를 다시 DispatcherServlet에 돌려줌

* **ModelAndView**

Controller가 처리한 결과와 그 결과를 보여줄 View에 관한 정보를 담고 있는 객체

* **ViewResolver**

View 관련 정보를 갖고 반환해 줄 View를 찾아주는 역할

* **View**

Controller가 처리한 결과를 보여줄 View



# Quiz

* Spring MVC 구성 요소에 대해 설명하시오
* Spring MVC 구조의 처리 과정을 설명하시오

<br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br>

# 출처

* [신입이 준비하는 [Spring] 기술 면접](https://geminihoroscope.tistory.com/90)
* [MVC 패턴 구조](https://newindow.tistory.com/66#:~:text=1.%20MVC%20%EA%B5%AC%EC%A1%B0%EB%9E%80%3F,%EC%88%98%20%EC%9E%88%EB%8B%A4%EB%8A%94%20%EC%9E%A5%EC%A0%90%EC%9D%B4%20%EC%9E%88%EB%8B%A4.)
* [Spring MVC 구조의 처리 과정을 설명해보시오](https://jeong-pro.tistory.com/96)



# Quiz 답안

* [Spring MVC 구성 요소에 대해 설명하시오](https://developsd.tistory.com/106)

<img width="829" alt="스크린샷 2021-03-05 오전 1 40 07" src="https://user-images.githubusercontent.com/46706670/109997934-13edab80-7d54-11eb-984f-b8bef2c9096f.png">



<br><br><br><br><br>

* [Spring MVC 구조의 처리 과정을 설명하시오](https://jeong-pro.tistory.com/96)

<img width="901" alt="스크린샷 2021-03-05 오전 1 39 20" src="https://user-images.githubusercontent.com/46706670/109998018-2bc52f80-7d54-11eb-86a6-3ccfcd745651.png">

