# R day2

> R day1에 이어서

## 2. R의 데이터셋

### 5. 팩터(factor)

> 범주값(level) 만으로 구성되는 벡터

#### 팩터 생성

- `factor(벡터, levels=c(레벨))`

  ```R
  > fscore <- factor(c(1,3,2,4,2,1,3,5,1,3,3,3))
  > class(f_score)
  [1] "factor"
  
  > f_score
   [1] 1 3 2 4 2 1 3 5 1 3 3 3
  Levels: 1 2 3 4 5
  
  > summary(f_score)
  1 2 3 4 5 
  3 2 5 1 1 
  
  > levels(f_score)
  [1] "1" "2" "3" "4" "5"
  ```

  - `summary`를 확인하면 각 레벨 당 몇개의 값을 가지고 있는지 확인 가능

  - `plot()`함수를 통해 자료를 시각화 할 수 있는데, __vector__과 __factor__의 차이를 확인할 수 있다.

    - __vector__은 각 인덱스당 값을 표현하는데, __factor__은 각 레벨당 몇개의 값을 가지는지 표현한다. 

  - 만약 `level=` 을 생성할 때 벡터에 있는 값을 제외하면, 그 제외된 값은 `<NA>`로 표현된다.

    ```R
    > btype <- factor(
    +   c("A", "O", "AB", "B", "O", "A"), 
    +   levels=c("A", "B", "O"))
    
    > btype
    [1] A    O    <NA> B    O    A   
    Levels: A B O
    
    > summary(btype)
       A    B    O NA's 
       2    1    2    1 
    
    > levels(btype)
    [1] "A" "B" "O"
    ```

    



### 6. 데이터 프레임(data.frame)

> 2차원의 벡터, 서로 다른 타입의 데이터들로 구성 가능 (열단위)

#### 데이터 프레임 생성

- `data.frame(벡터들)`, `data.frame(열이름=벡터, ...)`

  ```R
  > no <- c(1,2,3,4)
  > name <- c('Apple','Banana','Peach','Berry')
  > qty <- c(5,2,7,9)
  > price <- c(500,200,200,500)
  > fruit <- data.frame(no, name, qty, price)
  > fruit
    no   name qty price
  1  1  Apple   5   500
  2  2 Banana   2   200
  3  3  Peach   7   200
  4  4  Berry   9   500
  ```

#### 데이터 프레임 관련

- 모든 열의 데이터 개수는 __동일__해야 한다.

  ```R
  > data.frame(c(1, 2, 3), c(4, 5, 6), c(7, 8))
  Error in data.frame(c(1, 2, 3), c(4, 5, 6), c(7, 8)) : 
    arguments imply differing number of rows: 3,2
  ```

- `str(data.frame)`: 데이터 프레임의 구조 확인

  ```R
  > str(fruit)
  'data.frame':	4 obs. of  4 variables:
   $ no   : num  1 2 3 4
   $ name : chr  "Apple" "Banana" "Peach" "Berry"
   $ qty  : num  5 2 7 9
   $ price: num  500 200 200 500
  ```

- `colnames(data.frame)`: 열의 level 확인

- `rownames(data.frame)`: 행의 level 확인

- `dim(data.frame)`: 데이터 프레임의 __행__, __열__ 을 벡터로 표현

  ```R
  > colnames(fruit)
  [1] "no"    "name"  "qty"   "price"
  > rownames(fruit)
  [1] "1" "2" "3" "4"
  > dim(fruit)
  [1] 4 4
  ```



#### 데이터 프레임의 인덱싱

- 기존의 행렬과 인덱싱을 하는 방법은 기본적으로 동일하다.

- `data.frame[행, 열]`

  - 특정 값을 지정하거나, 행 값을 설정하지 않는 경우 __벡터__로 구성된다.

    ```R
    > fruit[1,1]
    [1] 1
    > str(fruit[1,1])
     num 1
    > fruit[, 2]
    [1] "Apple"  "Banana" "Peach"  "Berry" 
    > str(fruit[, 2])
     chr [1:4] "Apple" "Banana" "Peach" "Berry"
    ```

  - 행 값을 불러오는 경우 __데이터 프레임__으로 구성된다.

    ```R
    > fruit[1,]
      no  name qty price
    1  1 Apple   5   500
    > str(fruit[1,])
    'data.frame':	1 obs. of  4 variables:
     $ no   : num 1
     $ name : chr "Apple"
     $ qty  : num 5
     $ price: num 500
    ```

  - `data.frame[[col]]`, `data.frame[col]`: 둘의 차이는 후자가 데이터 프레임 형식을 __유지__한다.

    ```R
    > fruit[[3]]
    [1] 5 2 7 9
    > fruit[3]  # 데이터 프레임 형식 유지
      qty
    1   5
    2   2
    3   7
    4   9
    ```

  - `data.frame$이름`을 통해서도 인덱싱이 가능하다. 단 이 경우에는 벡터 형식으로 출력한다.

    ```R
    > fruit$qty
    [1] 5 2 7 9
    ```



#### 데이터 프레임의 데이터 추가

- `rbind(data.frame, 벡터)`: 행 벡터를 추가한다

- `cbind(data.frame, 이름=벡터)`: 열 벡터를 추가한다.

  ```R
  > fruit_1 <- rbind(fruit, c(5, 6, 7, 8))
  > fruit_1
    no   name qty price
  1  1  Apple   5   500
  2  2 Banana   2   200
  3  3  Peach   7   200
  4  4  Berry   9   500
  5  5      6   7     8
  
  > fruit_2 <- cbind(fruit, test=c(5, 6, 7, 8))
  > fruit_2
    no   name qty price test
  1  1  Apple   5   500    5
  2  2 Banana   2   200    6
  3  3  Peach   7   200    7
  4  4  Berry   9   500    8
  ```

- `data.frame$이름 <- 벡터` 를 통해 이름을 가진 열 벡터를 추가할 수 있다.

  ```R
  > fruit_2$test2 <- price *2
  > fruit_2
    no   name qty price test test2
  1  1  Apple   5   500    5  1000
  2  2 Banana   2   200    6   400
  3  3  Peach   7   200    7   400
  4  4  Berry   9   500    8  1000
  ```

  이 경우 데이터 프레임이 실시간으로 변화한다. 기존 `cbind`나 `rbind`는 새로운 변수에 설정해야 했지만, `data.frame$이름 <- 벡터`를 사용하는 경우 기존 데이터프레임에 바로 영향을 준다.



#### 데이터 프레임의 조건

- 위의 내용을 활용해 우리는 조건을 활용해 열 벡터를 추가할 수 있다.

- `ifelse(test, TRUE값, FALSE값)`

  ```R
  > fruit$title <- ifelse(fruit$name=="Apple", "사과", "사과 아님")
  > fruit
    no   name qty price     title
  1  1  Apple   5   500      사과
  2  2 Banana   2   200 사과 아님
  3  3  Peach   7   200 사과 아님
  4  4  Berry   9   500 사과 아님
  ```

  - 이처럼 새로 생성한 열들은 __factor__을 활용해 데이터를 깔끔하게 처리할 수 있다.

    ```R
    > fruit$title = factor(fruit$title)
    > str(fruit)
    'data.frame':	4 obs. of  5 variables:
     $ no   : num  1 2 3 4
     $ name : chr  "Apple" "Banana" "Peach" "Berry"
     $ qty  : num  5 2 7 9
     $ price: num  500 200 200 500
     $ title: Factor w/ 2 levels "사과","사과 아님": 1 2 2 2
    ```



#### 데이터 프레임의 데이터 추출

- __인덱싱__을 활용해 데이터 프레임에서 데이터를 추출할 수 있다.

  ```R
  > fruit[, c("name", "title")]
      name     title
  1  Apple      사과
  2 Banana 사과 아님
  3  Peach 사과 아님
  4  Berry 사과 아님
  
  > fruit[1:2,]
    no   name qty price     title
  1  1  Apple   5   500      사과
  2  2 Banana   2   200 사과 아님
  ```

- `subset(data.frame, select=추출을 원하는 범위, subset=조건)`함수를 활용해서도 추출 가능!

  ```R
  > subset(fruit, select=c("name", "price"), subset=title=="사과 아님")
      name price
  2 Banana   200
  3  Peach   200
  4  Berry   500
  
  > subset(fruit, select=c("name", "price"), subset=qty>5)
     name price
  3 Peach   200
  4 Berry   500
  ```

##### `subset`을 비롯한 함수에서 활용하기 너무 좋은 연산자들!

![image-20200908214916292](C:\Users\동화\TIL\R\image-20200908214916292.png)

```
> num1 <- 11 # c(11)
> num2 <- 3  # c(3)
> num1 / num2
[1] 3.666667
> num1 %% num2
[1] 2
> num1 %/% num2
[1] 3
> num1 != num2
[1] TRUE
> num1 == num2
[1] FALSE
```





## + `print` 그리고 `cat`

> `print`와 `cat`은 둘다 출력을 담당하는 함수지만 서로 차이가 있다.
>
> `print`는 데이터 구조를 유지하며 출력, `cat`은 내용 그 자체를 출력한다는 차이!

- `cat`이 내용 그 자체를 출력하기 때문에 개행이 일어나지 않는다! 개행은 "\n"으로 설정해야함

  ```R
  > cat(100, 200); cat(1, 2)
  100 2001 2
  > cat(100, 200, "\n"); cat(1, 2)
  100 200 
  1 2
  ```

- `cat`은 `chr`을 출력할 경우`""` 역시 표시하지 않고 출력한다.

  ```R
  > v1 <- c("사과", "바나나", "포도")
  > print(v1)
  [1] "사과"   "바나나" "포도"  
  > cat(v1)
  사과 바나나 포도
  ```

  - `print(내용, quote=F)`을 통해 cat과 비슷한 효과를 낼 수 있다.

    ```R
    > print(v1, quote=F)
    [1] 사과   바나나 포도  
    ```



## ++ 파일을 읽고 저장하자

- `scan("file 위치")`로 파일을 읽을 수 있다.

  ```R
  > nums <- scan("data/sample_num.txt")
  Read 7 items
  > nums
  [1]  10  30  40 100  20  40  70
  ```

  - 단 `scan`으로 파일을 읽을 경우 숫자 데이터를 입력한 파일이 아닌 경우 오류가 발생한다. 이 때 `what`을 통해 오류를 해결할 수 있다.

    ```
    > word_ansi <- scan("data/sample_ansi.txt",what="")
    Read 6 items
    > word_ansi
    [1] "aaa"    "가나다" "123"    "bbb"    "ccc"    "ddd"   
    ```

  - `encoding`을 통해 특정 방식으로 인코딩해 파일을 읽을 수 있다.

    ```R
    > words_utf8 <- scan("data/sample_utf8.txt", what="")
    Read 6 items
    > words_utf8
    [1] "aaa"                  "媛\u0080<eb>굹<eb>떎" # 글자 깨짐
    [3] "123"                  "bbb"                 
    [5] "ccc"                  "ddd"                 
    > words_utf8 <- scan("data/sample_utf8.txt", what="",encoding="UTF-8")
    Read 6 items
    > words_utf8
    [1] "aaa"    "가나다" "123"    "bbb"    "ccc"    "ddd"   
    ```

- `read.csv(file.choose())`, `read.csv("디렉토리.csv")` 을 통해 csv 파일도 읽을 수 있다.

  ```R
  > score <- read.csv("data/score.csv")
  > score
     id class math english science
  1   1     1   50      98      50
  2   2     1   60      97      60
  3   3     1   45      86      78
  
  > emp <- read.csv(file.choose()) # 직접 파일을 선택해야 한다.
  ```

- 지금까지 작업한 변수를 저장하고 싶으면 `save(list=ls(), file="이름.rda")`을 활용하자

- 저장한 __rda 파일__은 `load("file이름")`을 통해서 불러 올 수 있다.

- `ls()`는 지금까지 작업하고 저장했던 변수들 (Rstudio 기준 Environment에 저장되어있음)을 보여준다.

- 이 저장 된 변수들을 `rm(list=ls())`을 활용해 지울 수도 있다.