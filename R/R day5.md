# R day5

## 5. R 패키지

- R을 가지고 할 수 있는 통계, 분석 그리고 시각화와 관련한 기능을 정의한 함수들의 묶음이 R 패키지이다.
- R 패키지는 기본 패키지가 있고, 필요에 의해 추가로 설치해 사용할 수 있다.
- R 패키지를 다운받고 싶으면 [CRAN](https://cran.r-project.org/)을 활용하자
- R은 일정 규칙에 맞춰 누구나 제작하고 배포할 수 있는 Package를 통해 기능 확장을 유연하게 할 수 있다.



### 패키지 관련 실행문

- `install.packages("패키지명")`: 새로운 R 패키지 설치
- `library()`, `installed.packages()`: 이미 설치된 R 패키지 확인
- `remove.packages("패키지명")`: 설치된 패키지 삭제
- `packageVersion("패키지명")`: 설치된 패키지의 버전 확인
- `update.packages("패키지명")`: 설치된 패키지 업데이트
- `library(패키지명)`, `require(패키지명)`: 설치된 패키지 로드
- `detach("package:패키지명")`: 로드된 패키지 언로드
- `search()`: 로드된 패키지 점검



## 6. 정적 스크래핑(크롤링)

- 웹 스크래핑(Web Scraping): 웹 사이트 상에서 원하는 부분에 위치한 정보를 컴퓨터를 활용해 자동으로
  												 추출하고 수집하는 기술
- 웹 크롤링(Web Crawling): 자동화 된 웹 크롤러가 정해진 규칙에 따라 복수의 웹 페이지를 브라우징

___

- 스크래핑을 위해서는 CSS 선택자를 잘 알아둘 필요가 있다.
  [w3schools](https://www.w3schools.com/cssref/css_selectors.asp)에서 설명해주는 CSS 선택자!

  | Selector             | Example               | Example description                                          |
  | -------------------- | --------------------- | ------------------------------------------------------------ |
  | .class               | .intro                | Selects all elements with class="intro"                      |
  | .class1.class2       | .name1.name2          | Selects all elements with both *name1* and *name2* set within its class attribute |
  | .class1 .class2      | .na1 .na2             | Selects all elements with *na2* that is a descendant of an element with *na1* |
  | #id                  | \#firstname           | Selects the element with id="firstname"                      |
  | *                    | *                     | Selects all elements                                         |
  | element              | p                     | Selects all <p> elements                                     |
  | element.class        | p.intro               | Selects all <p> elements with class="intro"                  |
  | element,element      | div, p                | Selects all <div> elements and all <p> elements              |
  | element element      | div p                 | Selects all <p> elements inside <div> elements               |
  | element>element      | div > p               | Selects all <p> elements where the parent is a <div> element |
  | element+element      | div + p               | Selects all <p> elements that are placed immediately after <div> elements |
  | element~element      | p ~ ul                | Selects every <ul> element that are preceded by a <p> element |
  | [attribute]          | [target]              | Selects all elements with a target attribute                 |
  | [attribute=value]    | [target=_blank]       | Selects all elements with target="_blank"                    |
  | [attribute~=value]   | [title~=flower]       | Selects all elements with a title attribute containing the word "flower" |
  | [attribute\|=value]  | [lang\|=en]           | Selects all elements with a lang attribute value starting with "en" |
  | [attribute^=value]   | a[href^="https"]      | Selects every <a> element whose href attribute value begins with "https" |
  | [attribute$=value]   | a[href$=".pdf"]       | Selects every <a> element whose href attribute value ends with ".pdf" |
  | [attribute*=value]   | a[href*="w3schools"]  | Selects every <a> element whose href attribute value contains the substring "w3schools" |
  | :active              | a:active              | Selects the active link                                      |
  | ::after              | p::after              | Insert something after the content of each <p> element       |
  | ::before             | p::before             | Insert something before the content of each <p> element      |
  | :checked             | input:checked         | Selects every checked <input> element                        |
  | :default             | input:default         | Selects the default <input> element                          |
  | :disabled            | input:disabled        | Selects every disabled <input> element                       |
  | :empty               | p:empty               | Selects every <p> element that has no children (including text nodes) |
  | :enabled             | input:enabled         | Selects every enabled <input> element                        |
  | :first-child         | p:first-child         | Selects every <p> element that is the first child of its parent |
  | ::first-letter       | p::first-letter       | Selects the first letter of every <p> element                |
  | ::first-line         | p::first-line         | Selects the first line of every <p> element                  |
  | :first-of-type       | p:first-of-type       | Selects every <p> element that is the first <p> element of its parent |
  | :focus               | input:focus           | Selects the input element which has focus                    |
  | :hover               | a:hover               | Selects links on mouse over                                  |
  | :in-range            | input:in-range        | Selects input elements with a value within a specified range |
  | :indeterminate       | input:indeterminate   | Selects input elements that are in an indeterminate state    |
  | :invalid             | input:invalid         | Selects all input elements with an invalid value             |
  | :lang(*language*)    | p:lang(it)            | Selects every <p> element with a lang attribute equal to "it" (Italian) |
  | :last-child          | p:last-child          | Selects every <p> element that is the last child of its parent |
  | :last-of-type        | p:last-of-type        | Selects every <p> element that is the last <p> element of its parent |
  | :link                | a:link                | Selects all unvisited links                                  |
  | :not(selector)       | :not(p)               | Selects every element that is not a <p> element              |
  | :nth-child(n)        | p:nth-child(2)        | Selects every <p> element that is the second child of its parent |
  | :nth-last-child(n)   | p:nth-last-child(2)   | Selects every <p> element that is the second child of its parent, counting from the last child |
  | :nth-last-of-type(n) | p:nth-last-of-type(2) | Selects every <p> element that is the second <p> element of its parent, counting from the last child |
  | :nth-of-type(n)      | p:nth-of-type(2)      | Selects every <p> element that is the second <p> element of its parent |
  | :only-of-type        | p:only-of-type        | Selects every <p> element that is the only <p> element of its parent |
  | :only-child          | p:only-child          | Selects every <p> element that is the only child of its parent |
  | :optional            | input:optional        | Selects input elements with no "required" attribute          |
  | :out-of-range        | input:out-of-range    | Selects input elements with a value outside a specified range |
  | ::placeholder        | input::placeholder    | Selects input elements with the "placeholder" attribute specified |
  | :read-only           | input:read-only       | Selects input elements with the "readonly" attribute specified |
  | :read-write          | input:read-write      | Selects input elements with the "readonly" attribute NOT specified |
  | :required            | input:required        | Selects input elements with the "required" attribute specified |
  | :root                | :root                 | Selects the document's root element                          |
  | ::selection          | ::selection           | Selects the portion of an element that is selected by a user |
  | :target              | #news:target          | Selects the current active #news element (clicked on a URL containing that anchor name) |
  | :valid               | input:valid           | Selects all input elements with a valid value                |
  | :visited             | a:visited             | Selects all visited links                                    |



### 스크래핑

- 네이버 영화 사이트 댓글 정보를 스크래핑해보자

  > 네이버 영화 사이트의 데이터 중 영화제목, 평점, 리뷰만을 추출하여 CSV 파일의 정형화된 형식으로 저장한다.

  1. 스크래핑하려는 웹페이지의 URL 구조와 문서 구조를 파악해야 한다.

     - \- URL 구조 : http://movie.naver.com/movie/point/af/list.nhn?page=1
     - 크롬의 개발자도구를 활용하면 쉽게 확인할 수 있다.

  2. `rvest`패키지를 통해 스크래핑을 하자

     - `read_html(url, encoding="인코딩")`: url의 html을 인코딩으로 읽는다
     - `html_nodes(text, "selector")`: selector의 조건에 따라 태그 포함한 한 줄을 가져온다.
       ex:) <p>안녕하세요</p>
     - `html_text(nodes)`: nodes로 가져온 한 줄에서 콘텐츠 부분만 추출한다.
     - `write.csv(data.frame, ".csv")`: 데이터 프레임을 csv 파일로 저장한다
     - [Xpath](https://ko.wikipedia.org/wiki/XPath): [W3C](https://ko.wikipedia.org/wiki/W3C)의 표준으로 [확장 생성 언어](https://ko.wikipedia.org/wiki/XML) 문서의 구조를 통해 경로 위에 지정한 구문을 사용하여 항목을 배치하고 처리하는 방법을 기술하는 언어이다.

     ```R
     install.packages("rvest") # rvest 패키지 설치
     library(rvest) # rvest 패키지 로드
     
     url<- "http://movie.naver.com/movie/point/af/list.nhn?page=1"
     text <- read_html(url,  encoding="CP949")
     text
     
     # 영화제목
     nodes <- html_nodes(text, ".movie")
     title <- html_text(nodes)
     title
     # 영화평점
     nodes <- html_nodes(text, ".title em")
     point <- html_text(nodes)
     point
     # 영화리뷰 
     nodes <- html_nodes(text, xpath="//*[@id='old_content']/table/tbody/tr/td[2]/text()")
     nodes <- html_text(nodes, trim=TRUE)
     nodes
     review <- nodes[nchar(nodes) > 0] 
     review
     review <- c(review, '')
     page <- data.frame(title, point, review)
     write.csv(page, "movie_reviews.csv")
     ```

     - XPath 쉽게 추출하는 법: 크롬-> 개발자 도구-> Elements 에서 특정 코드 오른쪽 버튼 -> Copy
       										   -> Copy XPath