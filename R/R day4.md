# R day4

## 4. 함수

> R 프로그램에서 특정 작업을 독립적으로 수행하는 프로그램 코드 집합이며, 이 함수를 활용해 반복적인 연산을 효율적으로 할 수 있다.



### 함수의 처리 과정

- 시작(입력): 매개변수를 통해 아규먼트값을 받아온다.
- 실행(연산): 연산, 변환 등...
- 종료(출력): 수행 결과를 데이터셋으로 반환하거나 출력한다.

```R
함수명 <- function([매개변수]){
	수행 명령 문장
	return(리턴값)
}
```

```R
# 함수 호출
변수명 <- 함수명()
변수명 <- 함수명(아규먼트)
함수명()
함수명(아규먼트)
```



- 함수마다 매개변수 사양이 다르다. 이 사양에 맞춰 함수를 호출하자.

  - 기본값이 없는 경우, 매개변수가 존재하지 않는 경우, 기본값이 존재하는 경우 등...

- 리턴값이 없는 함수는 `NULL` 리턴

- `return()`을 통해 리턴값을 설정할 수 있는데, `return()`문이 없다면 마지막 출력 데이터값이 자동으로 리턴된다.

- 타입을 제한하고 싶다면 `is.xxxx()`함수를 활용하자

- 매개변수를 각각 선언해서 처리할 수 있다

  ```R
  > func4 <- function(x=100, y=200, z) {
  +   return(x+y+z)
  + }
  > func4(x=1,y=2,z=3)
  [1] 6
  > func4(y=11,z=22,x=33)
  [1] 66
  ```

- 함수 안에서 만들어지는 변수는 지역변수이기에 함수 안에서만 사용할 수 있다.

  ```R
  > func1 <- function() {
  +   xx <- 10   # 지역변수
  +   yy <- 20
  +   return(xx*yy)
  + }
  > xx
  에러: 객체 'xx'를 찾을 수 없습니다
  ```

- 함수 내에서 전역변수에 값을 저장하기를 원할때는 `<<-`을 활용하자

  ```R
  > x <- 70
  > func5 <- function() {
  +   x <- 10
  +   y <- 20
  +   x <<- 40  # 외부 변수 x 를 수정
  +   return (x+y)
  + }
  > func5()  
  [1] 30
  > x
  [1] 40
  > y
  에러: 객체 'y'를 찾을 수 없습니다
  ```



### 함수를 사용할 때 유용한 요소들

- `invisible()` : 리턴값을 나타내고 싶지 않을 때 활용

  ```R
  > ft.1 <- function(x) return()
  > ft.2 <- function(x) return(x+10)
  > ft.3 <- function(x) invisible(x+10)
  > 
  > ft.1(100)
  NULL
  > ft.2(100)
  [1] 110
  > ft.3(100)
  ```

- `list`는 `vector`에 포함된다.

  ```R
  > testParamType <- function(x){
  +   if(is.vector(x)) print("벡터를 전달했군요!")
  +   if(is.data.frame(x)) print("데이터프레임을 전달했군요!")
  +   if(is.list(x)) print("리스트를 전달했군요!")
  +   if(is.matrix(x)) print("매트릭스를 전달했군요!")
  +   if(is.array(x)) print("배열을 전달했군요!")
  +   if(is.function(x)) print("함수를 전달했군요!")
  + }
  > testParamType(list())
  [1] "벡터를 전달했군요!"
  [1] "리스트를 전달했군요!"
  ```

- `data.frame`은 `list`에 포함된다.

  ```R
  > testParamType(data.frame())
  [1] "데이터프레임을 전달했군요!"
  [1] "리스트를 전달했군요!"
  ```

- `stop(에러 메시지)`: 에러메시지를 반환하며 함수 실행을 종료한다. 리턴값이 없음

  ```R
  > testError1 <- function(x){
  +   if(x<=0)
  +     stop("양의 값이 필요합니다.")
  +   return(rep("테스트",x))
  + }
  > 
  > testError1(5)
  [1] "테스트" "테스트" "테스트" "테스트" "테스트"
  > testError1(0)
  Error in testError1(0) : 양의 값이 필요합니다.
  ```

- `warning(경고 메시지)`: 경고메시지를 반환하지만 함수를 종료하지는 않는다. 따라서 리턴값 존재

  ```R
  > testWarn <- function(x){
  +   if(x<=0)
  +     stop("양의 값이 필요합니다.")
  +   if(x>5){
  +     x<-5
  +     warning("5보다 크기 때문에 5로 처리했습니다.")
  +   }
  +   return(rep("테스트",x))
  + }
  > testWarn(3)
  [1] "테스트" "테스트" "테스트"
  > testWarn(10)
  [1] "테스트" "테스트" "테스트" "테스트" "테스트"
  경고메시지(들): 
  In testWarn(10) : 5보다 크기 때문에 5로 처리했습니다.
  ```

- `try(함수)`: 에러가 발생해도 함수 연산이 멈추지 않게 한다.

  ```R
  > test1 <-function(p){
  +   cat("안녕\n")
  +   testError1(-1)
  +   cat("하세요\n")
  + }
  > test1() # try 없는 경우
  안녕
  Error in testError(-1) :양의 값이 필요합니다.
  
  > test2 <- function(p){
  +   cat("안녕\n")
  +   try(testError(-1))
  +   cat("하세요\n")
  + }
  > test2() # try가 있는 경우
  안녕
  Error in testError(-1) :양의 값이 필요합니다.
  하세요 
  ```

- `tryCatch(실행문, warning = 경고문, error= 에러문, finally= 항상 실행문)`

  ```R
  > testAll <-function(p){
  +   tryCatch({
  +     if(p=="오류테스트"){
  +       testError1(-1)
  +     }else if (p =="경고테스트"){
  +       testWarn(6)
  +     }else{
  +       cat("에러, 경고가 없습니다\n")
  +       print(testError1(2))
  +       print(testWarn(3))
  +     }
  +   },warning = function(w){
  +     print(w)
  +     cat(":(\n")
  +   },error = function(e){
  +     print(e)
  +     cat(":^(\n")
  +   },finally ={
  +     cat("오류, 경고와 상관없이 항상 수행합니다.\n")
  +   })
  + }
  
  > testAll("오류테스트")
  <simpleError in testError1(-1): 양의 값이 필요합니다.>
  :^(
  오류, 경고와 상관없이 항상 수행합니다.
      
  > testAll("경고테스트")
  <simpleWarning in testWarn(6): 5보다 크기 때문에 5로 처리했습니다.>
  :(
  오류, 경고와 상관없이 항상 수행합니다.
      
  > testAll("아무거나")
  에러, 경고가 없습니다
  [1] "테스트" "테스트"
  [1] "테스트" "테스트" "테스트"
  오류, 경고와 상관없이 항상 수행합니다.
  ```

- `any(조건)`: 한개라도 존재한다면 TRUE 값을 반환한다.

  ```R
  > abc <- c("a","b",NA)
  > any(is.na(abc))
  [1] TRUE
  ```

- `all(조건)`: 모든 값이 조건이어야 TRUE 값을 반환.

  ```R
  > f.case3 <- function(x) {
  +   if(all(is.na(x))) 
  +     return("모두 NA임")
  +   else
  +     return("모두 NA인 것은 아님")
  + }
  
  > f.case3(c(NA, NA, NA))
  [1] "모두 NA임"
  
  > f.case3(c(NA, NA, 10))
  [1] "모두 NA인 것은 아님"
  ```

- `Sys.sleep(초시간)`: 결과값 출력에 딜레이를 주고 싶을 때

  ```R
  > testSleep <- function(x) {
  +   for(data in 6:10) {       
  +     cat(data,"\n")
  +     if(x)
  +       Sys.sleep(1)
  +   }
  +   return()
  + }
  > testSleep(FALSE)
  6 
  7 
  8 
  9 
  10 
  NULL
  > testSleep(TRUE)
  6
  7 # 1초후
  ...
  ```

- 가변형 인자는 안에서 벡터등으로 따로 지역변수를 설정해야한다.

  ```R
  > funcArgs <- function(...) {
  +   p <- c(...) # 가변형인자를 벡터로 설정한다.
  +   data <- 1:10
  +   #opts <- ifelse(length(p)>0, p, "")
  +   if(length(p) > 0)
  +     opts <- p
  +   else
  +     opts <- ""
  +   print(p)
  +   print(opts)
  +   if(opts[1] == "")
  +     print(data)
  +   else 
  +     for(opt in opts) {
  +       switch(EXPR=opt,
  +              SUM=, Sum=, sum= print(sum(data)),
  +              MEAN=, Mean=, mean= print(mean(data)),
  +              DIFF=, Diff=, diff= print(max(data) - min(data)),
  +              MAX=, Max=, max= print(max(data)),
  +              MIN=, Min=, min= print(min(data)),
  +              SORT=, Sort=, sort= print(sort(data))
  +       )
  +     }
  + }
  > 
  > funcArgs()
  NULL
  [1] ""
   [1]  1  2  3  4  5  6  7  8  9 10
  > funcArgs("SUM", "mean", "Min")
  [1] "SUM"  "mean" "Min" 
  [1] "SUM"  "mean" "Min" 
  [1] 55
  [1] 5.5
  [1] 1
  ```

  

