# SPA 란 무엇인가?
## MDN
- https://developer.mozilla.org/en-US/docs/Glossary/SPA

### What?
- 하나의 문서만 로드하는 것.
- 문서의 컨텐츠를 Javascript 를 사용해서 업데이트 하는 것. 
- Fetching 이 필요한 경우, XMLHttpRequest 를 사용하는 것. 

### 장, 단점
- 장
  - 페이지를 완전히 업데이트 하지 않아도 사용 가능하다
  - 퍼포먼스가 상대적으로 좋다
  - 보다 동적인 사용자 경험을 준다

- 단
  - SEO? 에서 불리하다
  - 상태관리를 해야 한다
  - navigation 을 구현해야 한다

### 상태관리를 해야 한다?
Javascript 로 문서를 업데이트한다는 말이 상태변화를 내포한다.
변화는 변화를 규정짓는 값을 필요로 한다.  

## Wikipedia
https://en.wikipedia.org/wiki/Single-page_application

> A single-page application (SPA) is a web application or website that **interacts with the user by dynamically rewriting** the current web page with new data from the web server, instead of the default method of a web browser loading entire new pages. The goal is **faster transitions** that make the website feel more **like a native app**.

마치 네이티브 앱처럼 느껴지는 사용자 경험. 빠른 전환. 

> In a SPA, a page refresh never occurs; instead, all necessary HTML, JavaScript, and CSS code is either retrieved by the browser with **a single page load**,[1] or the **appropriate resources are dynamically loaded and added to the page as necessary**, usually **in response to user actions**. The page does not reload at any point in the process, nor does it transfer control to another page, although the location hash or the HTML5 History API can be used to provide the perception and navigability of separate logical pages in the application.[2]

단 한 번의 페이지 로드. 사용자 action에 따른 응답으로 적절한 내용으로 업데이트.

## 나의 생각
### SPA 란?
Web application 의 일종. 단 한번의 페이지 로드가 특징. 
이후의 동작은 사용자 동작에 따라서 동적으로 업데이트함. 경우에 따라서, 
데이터 페칭이 필요할 수도 있는데, 이것 역시 스크립트언어를 통해 동적으로 수행. 
사용자 동작에 따른 동적변화는 상태변화를 뜻하므로, 이를 관리할 수 있는 도구가 필요.

### action 이름에 대한 생각
Redux 를 사용하면서, setTodos 와 같은 네이밍은 적절하지 않다.
정말로 어플리케이션의 동적 변화(상태 변화라고 해도 괜찮을듯) 를 일으키는 동인을 써주는 것이 훨씬 적절하다. SPA 의 의미를 생각해보자. 

## 추가로 공부할 것들
- SEO
- XMLHttpRequest
- SSR
- SPA 의 역사

