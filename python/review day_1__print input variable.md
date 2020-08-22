# 파이썬 복습 1일

## 피가되고 살이 될 기본으로 숙지할 내용

### 1. 출력

파이썬의 기본적인 출력문은 `print` 명령이며, 기본적으로 다음과 같이 구성할 수 있어요.

```python
print(출력 내용들, sep= 사이에 입력하고 싶은 것, end=마지막에 입력하고 싶은 것)
```

```python
>>> print(3 + 4)
7
```

```python
>>> v = 365
>>> print(v)
365
>>> print(v * 2)
730
```

위의 예제처럼 `print` 명령을 통해 출력하고 싶은 내용들은 수식, 변수, 변수를 활용한 수식 모두를 포함합니다.

`print`는 여러 변수, 결과 값을 한번에 출력할 수 있는데, 이 결과 사이에 입력하고 싶은 문자를 `sep` 인수에 입력할 수 있다. `sep` 인수의 기본 값은 공백이라는 점을 기억하자!

```python
>>> print(Hendrik, Lee)
Hendrik Lee
>>> print(Hendrik, Lee, sep='+')
Hendrik+Lee
```

`print`명령은 기본적으로 마지막에 개행을 포함한다. 즉 `end`인수의 기본 값은 개행 `\n`이라는 것에 유의하고, `end`인수에 `print`명령을 통해 출력하고 싶은 문자를 입력해 교체할 수 있다.

```python
>>>print(Hendrik)
>>>print(Lee)
Hendrik
Lee
>>>print(Hendrik, end='')
>>>print(Lee)
HendrikLee
```

위의 예제처럼 `print`문을 여러번 사용할 때 `end`인수를 입력해주지 않으면 개행처리가 된 것을 볼 수 있다. 하지만 `end`인수에 `''`라는 인수를 추가해 개행처리 없이 `print`명령을 수행한 것을 볼 수 있다.



### 2. 입력

사용자와 소통하기 위해서는 사용자가 원하는 것이 필요해요. 이 때 필요한 정보를 입력받기 위해 사용자에게 질문을 하고, 이 질문에 대해 답을 받는 명령을 `input`이라고 합니다!

```python
변수 = input('질문 내용')
```

위의 `input` 명령을 사용하면 사용자에게 질문 내용을 확인하고, 정보를 입력하도록 유도할 수 있어요. 이 때 사용자가 입력한 정보는 변수에 저장됩니다. 이를 아래의 예제에서 확인하세요.

```python
>>> name = input('이름은 무엇인가요?')
이름은 무엇인가요? Hendrik Lee
>>> print(name)
Hendrik Lee
```

하지만 `input`을 통해 입력받은 내용은 __무조건 문자열로 저장__됩니다! 그렇기에 나이와 같이 숫자를 입력할 때는 `int()`나 `float()`함수를 통해 정수 또는 실수로 변환하는 것이 중요합니다.

```python
>>> number = int(input('숫자를 입력해주세요'))
숫자를 입력해주세요 20
>>> print(number * 2)
40
```



### 3. 변수

앞에서 여러번 언급되었던 단어가 있습니다. 바로 __변수__인데요. 메모리에 __이름을 붙이고 값을 저장하는__ 것을 변수라고 합니다. 예를 들어 누군가의 이름을 작성해서 명령을 수행할 수 있지만, 이 이름의 입력이 반복된다면 우리는 `name`과 같이 새로운 변수를 만들어서 저장할 수 있습니다. 하!지!만! 변수를 설정할 때 기억해야 할 것들이 있습니다.

- 기본적으로 이름을 자유롭게 설정할 수 있으나 __중복으로 설정할 수 없습니다.__ 중복으로 설정하려고 시도한다면 아래 예제와 같은 상황을 맞이할거에요.

  ```python
  >>> name = Hendrik
  >>> print(name)
  Hendrik
  >>> name = Lee
  >>> print(name)
  Lee
  ```

  이처럼 중복으로 변수를 설정하려고 하면 기존에 저장되었던 값이 사라지고, 새로운 값으로 변수가 설정됩니다.

- 파이썬이 미리 활용방법을 저장해 놓은 __키워드__는 변수로 사용할 수 없습니다. 파이썬에서 키워드는 다음과 같습니다!

  | 분류        | 키워드                                      |
  | ----------- | ------------------------------------------- |
  | 제어문      | if, else, elif, for, while, break, continue |
  | 상수        | True, False, None                           |
  | 논리 연산자 | and, or, not, in                            |
  | 함수        | def, return, lambda, nonlocal, global       |
  | 예외 처리   | try, except, finally, raise                 |
  | 모듈        | import, from, class                         |
  | 기타        | is, del, with, as, yield, assert, pass      |

  혹시 이상한 점을 느꼈나요? 앞에서 열심히 배웠던 `print()`, `input()`과 같은 명령은 위의 __키워드__에 포함되지 않습니다. 하지만 `print()`같이 기본적으로 내장 된 함수나, 표준 모듈명도 변수로 쓰지 않는 것이 좋습니다. `print`를 변수로 사용하게 된다면, 이후에는 출력문과 이별을 하게 된다는 것을 명심합시다!

  ```python
  print("Hendrik")
  print = "Hendrik"
  print(345)
  
  Hendrik
  Traceback (most recent call last):
    File "~", line 3, in <module>
      print(345)
  TypeError: 'str' object is not callable
  ```

  위와 같이 오류문을 확인하게 될 거에요!

- 파이썬은 똑똑하게 __대소문자를 구분합니다.__ Hendrik, hendrik은 서로 다른 변수입니다. 일반적으로 입력의 편의를 위해 변수는 소문자로 입력하는 것이 좋아요

- 알파벳, 숫자, \_로 구성되는 변수는 __공백, 기호__는 사용할 수 없습니다! 다른 사람과 코드를 공유할 때 편의를 위해 여러 단어로 구성해야 할 때가 있는데, 이럴 때는 my_name처럼 _____을 활용해 구분해 줍시다. 

- 숫자도 변수에 쓸 수 있지만 __첫문자__를 숫자로는 쓸 수 없습니다!

- 똑똑한 파이썬은 한글이나 한자를 변수로 사용할수도 있습니다. 하지만 우리는 __GLOBAL__세계에 살고 있고, 또 한글과 영어를 왔다 갔다 하는 번거로움이 있기 때문에 일반적으로는 __영어__를 사용하는 것을 추천합니다!



파이썬의 변수는 값에 의해 타입이 바뀝니다. 이 때 변수의 타입을 알고 싶을 때 `type()`함수를 활용해 확인할 수 있습니다.

```python
>>> name = "Hendrik"
>>> type(name)
<class 'str'>
>>> hendrik_score = 100
>>> type(hendrik_score)
<class 'int'>
```

변수를 만들면 계속 존재하지만, 우리는 특정 변수를 지우고 싶을 때가 있습니다. 그럴 때! `del`명령을 사용해 변수를 삭제할 수 있습니다. 하지만 당연하게도 변수를 지우면 __변수를 참조할 수 없어요.__ 물론 다시 변수를 설정하는 것은 얼마든지 가능합니다.

```python
name = "Hendrik"
print(name)
del name
print(name)

Hendrik
Traceback (most recent call last):
  File "~", line 4, in <module>
    print(name)
NameError: name 'name' is not defined
```

