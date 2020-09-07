# R day1

> 통계 계산과 그래픽을 위한 프로그래밍 언어

## 1. R의 자료형과 리터럴

- 문자형(character): 문자, 문자열
  - "가나다", '가나다', "", '', '123', "abc"
- 수치형(numeric): 정수(integer), 실수(double)
  - 100, 3.14, 0
- 복소수형(complex): 실수+허수
- 논리형(logical): 참값(TRUE), 거짓값(FALSE)
  - TRUE(T), FALSE(F) __대문자__
- NULL: 데이터 셋이 비어있음
- NA: 데이터 셋의 내부에 값이 존재하지 않음
- Nan: 숫자가 아님(not a number)
- Inf(무한대값)



### 자동형변환 룰

> R에서 여러 형태를 조합해서 사용한다면 문자형>복소수형>수치형>논리형 순으로 형태가 결정된다



### 기본 함수

- 타입체크 함수들

  - `is.character(x)`, `is.logical(x)`, `is.numeric(x)`, `is.double(x)`, `is.integer(x)`, `is.null(x)`, `is.na(x)`, `is.nan(x)`, `is.finite(x)`, `is.infinite(x)`

- 강제형변환 함수

  - `as.character(x)`, `as.complex(x)`, `as.numeric(x)`, `as.double(x)`, `as.integer(x)`, `as.logical(x)`

- 자료형 또는 구조 확인 함수

  - `class(x)`

    ```R
    > class("Hello")
    [1] "character"
    ```

  - `str(x)`

    ```R
    > str(123)
    num 123
    > str("Hello")
    chr "Hello"
    ```

  - `mode(x)`

    ```R
    > mode(123)
    [1] "numeric"
    > mode("Hello")
    [1] "character"
    ```

  - `typeof(x)`

    ```R
    > typeof("Hello")
    [1] "character"
    > typeof(123)
    [1] "double"
    ```

- `rm(x)`: 변수 x를 삭제



## 2. R의 데이터셋

### 1. 스칼라(Scala)

> 구성인자가 한개로 되어 있는 데이터 셋으로 1차원으로 사용된다.

### 2. 벡터(Vector)

> R에서 다루는 가장 기본적인 데이터셋, 1차원으로 사용하며, 하나의 값인 스칼라도 벡터로 취급

- 동일 타입의 데이터만으로 구성된다.



#### R은 변수를 어떻게 설정할까?

- `<-`를 활용하여 설정

  ```R
  > v1 <- c(1, 5, 8); v1
  [1] 1 5 8
  
  > c("가","나","다") -> v3; v3
  [1] "가" "나" "다"
  ```

- `=`을 활용하여 설정

  ```R
  > v1 = c(1, 2, 3); v1
  [1] 1 2 3
  ```

  

#### 벡터 생성 방법

- `c()`: 규칙이 없는 벡터를 생성할 때 좋음.

  ```R
  > c(1, 5, 7, 44)
  [1]  1  5  7 44
  ```

- `seq(from, to, by)`: 규칙이 존재하는 벡터를 생성

  ```R
  > seq(1,10,3)
  [1]  1  4  7 10
  ```

- `rep(x, times or each)`: 특정 문자를 반복하는 벡터를 생성

  ```R
  > rep(1:3, times=5)
   [1] 1 2 3 1 2 3 1 2 3 1 2 3 1 2 3
   
   > rep(1:3, each=5)
   [1] 1 1 1 1 1 2 2 2 2 2 3 3 3 3 3
  ```

- `sample(범위, 개수, replace=F)`: 벡터 범위에서 개수만큼 랜덤으로 추출, `replace`가 `F`이면 중복 없이, `T`면 중복 포함해서 벡터를 생성

  ```R
  > sample(1:20, 3)
  [1] 17  9  1
  
  > sample(1:5, 4, replace=T)
  [1] 5 1 5 5
  ```

  

#### 내장 상수 벡터

- `LETTERS`, `letters`: 영대,소문자

  ```R
  > LETTERS
   [1] "A" "B" "C" "D" "E" "F" "G" "H" "I" "J" "K" "L" "M" "N" "O" "P"
  [17] "Q" "R" "S" "T" "U" "V" "W" "X" "Y" "Z"
  
  > letters
   [1] "a" "b" "c" "d" "e" "f" "g" "h" "i" "j" "k" "l" "m" "n" "o" "p"
  [17] "q" "r" "s" "t" "u" "v" "w" "x" "y" "z"
  ```

- `month.name`, `month.abb`: 월 이름, 축약형

  ```R
  > month.name
   [1] "January"   "February"  "March"     "April"     "May"      
   [6] "June"      "July"      "August"    "September" "October"  
  [11] "November"  "December" 
  
  > month.abb
   [1] "Jan" "Feb" "Mar" "Apr" "May" "Jun" "Jul" "Aug" "Sep" "Oct" "Nov"
  [12] "Dec"
  ```

- `pi`: 파이

  ```R
  > pi
  [1] 3.141593
  ```

  

#### 벡터 관련 주요 함수

- `length()`: 벡터의 길이

  ```R
  > length(LETTERS)
  [1] 26
  ```

- `sort(x, decreasing=FALSE)`: 벡터 정렬 __하지만 정렬해서 출력할 뿐 벡터 자체를 바꾸지 않는다!!__

  ```R
  > v1 = c(1, 5, 2, 4, 7); sort(v1); v1
  [1] 1 2 4 5 7
  [1] 1 5 2 4 7
  ```

- `rev(x)`: 벡터 `x`를 역순으로, __역시 벡터를 바꾸지 않는다!!__

  ```R
  > rev(v1)
  [1] 7 4 2 5 1
  ```

- `range(x)`: 벡터 `x`의 범위를 나타냄

  ```R
  > range(v1)
  [1] 1 7
  ```

- `order(x, decreasing=FALSE)`: 정렬한 __인덱스__를 보여준다

  ```R
  > v1 = c(1, 5, 2, 4, 7); order(v1); v1
  [1] 1 3 4 2 5
  [1] 1 5 2 4 7
  ```

  > 벡터 1, 5, 2, 4, 7을 정렬하면 1, 2, 4, 5, 7을 출력한다. 여기에서 1은 기존 벡터에서 인덱스가 1이고, 2는 3이다. 이를 반복하면 order는 `1 3 4 2 5`의 값을 얻을 수 있다.

  ##### 인덱스란?

  > 벡터에서 순서값을 나타내는 표시로 `x[처음:끝]`, `x[인덱스]`로 출력 할 수 있다.

  ```R
  > v1 = c(1, 5, 2, 4, 7); v1[1:3]; v1[5]
  [1] 1 5 2
  [1] 7
  ```

- `which(변수의 조건)`: 벡터 중 조건을 충족하는 __인덱스__를 출력한다.

  ```R
  > v1
  [1] 1 5 2 4 7
  > which(v1>3)
  [1] 2 4 5
  ```

  > 3을 초과하는 값은 5, 4, 7 이며 이 각 값의 인덱스인 2, 4, 5가 출력된다

- `paste(x, y, ..., sep=)`: 각 값을 문자 그대로 합치며, `sep`를 통해 사이에 들어가는 값을 설정할 수 있다. 또한 벡터를 결합할 수 있다. 사이에 들어가는 값을 아무것도 없는 값으로 설정하는 방법은`sep=''`을 사용하거나, `paste0()` 함수를 사용한다.

  ```R
  > paste("I'm","Duli","!!")
  [1] "I'm Duli !!"
  > paste("I'm","Duli","!!", sep="")
  [1] "I'mDuli!!"
  > paste0("I'm","Duli","!!")
  [1] "I'mDuli!!"
  > 
  > fruit <- c("Apple", "Banana", "Strawberry")
  > food <- c("Pie","Juice", "Cake")
  > paste(fruit, food)
  [1] "Apple Pie"       "Banana Juice"    "Strawberry Cake"
  ```

  

#### 벡터의 계산

> 기존 벡터에서 특정 값을 연산해 벡터를 표시할 수 있고, 최대값, 최소값, 평균, 총 합을 구할 수 있다.

- 벡터의 연산

  ```R
  > v1
  [1] 1 5 2 4 7
  
  > v1 + 2
  [1] 3 7 4 6 9
  
  > v1 * 3
  [1]  3 15  6 12 21
  ```

- 최대값 `max(x)`, 최소값 `min(x)`, 평균 `mean(x)`, 총합 `sum(x)`, `summary(x)`

  ```R
  > max(v1)
  [1] 7
  
  > min(v1)
  [1] 1
  
  > mean(v1)
  [1] 3.8
  
  > sum(v1)
  [1] 19
  
  > summary(v1)
     Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
      1.0     2.0     4.0     3.8     5.0     7.0 
  ```

#### 벡터의 특정 값 추출

> 인덱스, 벡터, 논리값, 조건을 활용해 벡터에서 특정 값을 추출 할 수 있다

```R
> v1; v1[c(2,4)]; v1[3]; v1[c(F, T, T, F, T)]; v1[v1 > 3]
[1] 1 5 2 4 7
[1] 5 4
[1] 2
[1] 5 2 7
[1] 5 4 7
```

##### &와 |

> &은 and, |는 or의 의미를 가지며 &&, ||는 벡터 중 처음 값에 대해서만 적용한다

```R
> c(T, T, F, F) & c(T, F, T, F);
[1]  TRUE FALSE FALSE FALSE
> c(T, T, F, F) | c(T, F, T, F);
[1]  TRUE  TRUE  TRUE FALSE
> c(T, T, F, F) && c(T, F, T, F);
[1] TRUE
> c(T, T, F, F) || c(T, F, T, F)
[1] TRUE
```



#### 벡터의 이름

> `names(x)`함수를 통해 벡터의 각 값에 이름을 줄 수 있으며, `NULL`을 활용해 이름을 제거할 수 있다.

```R
> v1
[1] 1 5 2 4 7
> names(v1) <- LETTERS[1:5]
> v1
A B C D E 
1 5 2 4 7 
> names(v1) <- NULL
> v1
[1] 1 5 2 4 7
```



### 3. 행렬 (matrix)

> 2차원의 벡터, 동일한 타입의 데이터로만 저장 가능

#### 행렬 생성 방법

- `matrix(data=벡터, nrow=행의 개수, ncol=열의 개수, byrow=T or F)`

  > 기본적으로 행렬은 열 단위로 벡터를 생성되지만 byrow 옵션을 통해 행 단위로 벡터를 생성할 수 있다.

  ```R
  > chars <- letters[1:10]
  > matrix(chars, nrow=5)
       [,1] [,2]
  [1,] "a"  "f" 
  [2,] "b"  "g" 
  [3,] "c"  "h" 
  [4,] "d"  "i" 
  [5,] "e"  "j" 
  > matrix(chars, nrow=5, byrow=T)
       [,1] [,2]
  [1,] "a"  "b" 
  [2,] "c"  "d" 
  [3,] "e"  "f" 
  [4,] "g"  "h" 
  [5,] "i"  "j" 
  > matrix(chars, ncol=5)
       [,1] [,2] [,3] [,4] [,5]
  [1,] "a"  "c"  "e"  "g"  "i" 
  [2,] "b"  "d"  "f"  "h"  "j" 
  > matrix(chars, ncol=5, byrow=T)
       [,1] [,2] [,3] [,4] [,5]
  [1,] "a"  "b"  "c"  "d"  "e" 
  [2,] "f"  "g"  "h"  "i"  "j" 
  > matrix(chars, nrow=3, ncol=5)
       [,1] [,2] [,3] [,4] [,5]
  [1,] "a"  "d"  "g"  "j"  "c" 
  [2,] "b"  "e"  "h"  "a"  "d" 
  [3,] "c"  "f"  "i"  "b"  "e" 
  ```

  > 기본적으로 행렬을 만들기 위해서는 벡터는 행*열의 값만큼 개수를 가지고 있는 것이 좋으나, 벡터의 개수가 부족한 경우에는 벡터의 처음 값부터 다시 채워 넣는다.

- `rbind()`, `cbind()`: 행 단위로, 열 단위로 벡터를 결합해 행렬을 만든다.

  ```R
  > vec1 <- c(1,2,3)
  > vec2 <- c(4,5,6)
  > vec3 <- c(7,8,9)
  > mat1 <- rbind(vec1,vec2,vec3); mat1
       [,1] [,2] [,3]
  vec1    1    2    3
  vec2    4    5    6
  vec3    7    8    9
  > mat2 <- cbind(vec1,vec2,vec3); mat2
       vec1 vec2 vec3
  [1,]    1    4    7
  [2,]    2    5    8
  [3,]    3    6    9
  ```

#### 행렬의 이름

> 행렬의 이름은 행, 열 단위로 설정할 수 있으며 각각 `rownames`, `colnames`를 활용해 설정 가능

```R
> rownames(mat1) <- c("row1","row2","row3")
> mat1
     [,1] [,2] [,3]
row1    1    2    3
row2    4    5    6
row3    7    8    9

> colnames(mat1) <- c("col1","col2","col3")
> mat1
     col1 col2 col3
row1    1    2    3
row2    4    5    6
row3    7    8    9
```



#### 행렬의 계산

> 행렬 역시 벡터와 동일하게 연산자, `mean`, `sum`, `min`, `max`, `summary`를 활용 가능하며 각 행과 열의 합인 `rowSums`, `colSums`역시 활용할 수 있다.

- `apply(행렬, 1 or 2, 계산값)`

  > apply 함수를 통해 각 행, 열의 계산값을 쉽게 도출 할 수 있으며 1은 행을 의미하고 2는 열을 의미한다

  ```R
  > x2
       [,1] [,2] [,3]
  [1,]    1    4    7
  [2,]    2    5    8
  [3,]    3    6    1
  > apply(x2, 1, max)
  [1] 7 8 6
  > apply(x2, 2, max)
  [1] 3 6 8
  ```

  

### 4. 배열(array)

> 3차원 벡터이며, 동일 타입의 데이터만 저장 가능하다

```R
> a1 <- array(1:30, dim=c(2,3,5))
> a1
, , 1

     [,1] [,2] [,3]
[1,]    1    3    5
[2,]    2    4    6

, , 2

     [,1] [,2] [,3]
[1,]    7    9   11
[2,]    8   10   12

, , 3

     [,1] [,2] [,3]
[1,]   13   15   17
[2,]   14   16   18

, , 4

     [,1] [,2] [,3]
[1,]   19   21   23
[2,]   20   22   24

, , 5

     [,1] [,2] [,3]
[1,]   25   27   29
[2,]   26   28   30

> 
> a1[1,3,4]
[1] 23
> a1[,,3]
     [,1] [,2] [,3]
[1,]   13   15   17
[2,]   14   16   18
> a1[,2,]
     [,1] [,2] [,3] [,4] [,5]
[1,]    3    9   15   21   27
[2,]    4   10   16   22   28
> a1[1,,]
     [,1] [,2] [,3] [,4] [,5]
[1,]    1    7   13   19   25
[2,]    3    9   15   21   27
[3,]    5   11   17   23   29
```

