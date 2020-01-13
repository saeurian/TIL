# 파이썬 기초 (Class, 모듈, 패키지, 예외처리)

## Class

> 객체를 표현하기 위한 개념
>
> EX)
>
> 게임에서 기사, 궁수, 마법사 등 직업별로 클래스가 생성됨
>
> 웹브라우저 - 스크롤바, 버튼, 체크박스 등 구성요소 모두 클래스임



### 만드는 과정

클래스는 속성과 메서드로 구성됨

1. 기사 클래스로 홍길동 객체(캐릭터)를 생성
2. 체력, 마나, 공격력 ... 초기값 설정 - 속성
3. 달리기, 베기, 찌르기 ... 동작 설정 - 메서드



### 계산기 만들기

```python
class FourCal():
     def setData(self, first, second):
            # 여기서 self 는 밑의 a를 의미
            self.first = first # self.first=4 first는 임시변수 같은 것
            self.second = second # self.first=2
     def add(self):
         res = self.first + self.second
         return res
     def sub(self): # self에는 first와 second가 정의되어 있음
         res = self.first - self.second
         return res
     def div(self):
         res = self.first / self.second
         return res
     def mul(self):
         res = self.first * self.second
         return res
       
 # 사칙 연산 클래스
a = FourCal() # FourCal 이라는 class로 부터 객체 생성(a)
a.setData(4,2) # 숫자 4, 2를 a에 지정
print(a.mul()) 
print(a.add()) # 4+2 = 6 리턴
print(a.sub()) 
print(a.div())  
```



### Class 상속

class 자식클래스명(부모클래스명):

자식 클래스는 부모클래스의 모든 기능을 사용할 수 있음 & 기능 변경 추가 가능

```python
class MoreFourCal(FourCal):
     pass
    
b= MoreFourCal()
b.setData(4,2)
print(b.mul()) 
print(b.add())
print(b.sub()) 
print(b.div())  
```

* 기능 추가

  ```python
  class MoreFourCal(FourCal):
      def setData(self, first, second):
              # 여기서 self 는 밑의 a를 의미
              self.first = first # self.first=4 first는 임시변수 같은 것
              self.second = second 
      def pow(self):
          res = self.first ** self.second # 제곱연산
          return res
      
      b= MoreFourCal()
  b.setData(4,2)
  print(b.pow())
  ```

* 메서드 오버라이딩(overriding)

  부모클래스로부터 상속받은 메서드를 자식이 변경한 것

  ```python
  class SafeFourCal(FourCal):
      def div(self): # self 무조건 필수 (FourCal의 div함수를 변경)
          if self.second == 1:
              print("1로 나누지 마세요")
              return 
          else:
              return self.first/self.second
          
  sfc = SafeFourCal()
  sfc.setData(4,1)
  print(sfc.div())
  ```



### 변수 여러개 받기 *args

```python
class Person():
    def __init__(self, *args): # *args : 인수가 여러개 들어올 수 있음
        self.name = args[0]
        self.age = args[1]
        self.addr = args[2]
    def greeting(self):
        res = "안녕하세요. 나는 {}입니다.".format(self.name)
        return print(res)
    
ps = Person("홍길동", 25, "서울시 역삼동")
ps.greeting() # 안녕하세요. 나는 홍길동입니다.
print("이름:", ps.name)
print("나이:", ps.age)
print("사는곳:", ps.addr)
```



## 모듈(module)

> 함수나 변수, 클래스들을 모아놓은 파일
>
> 다른 파이썬 프로그램에서 모듈을 사용하기 편하게 하기 위해서
>
> 확장자 .py가 붙은 파일



**모듈**(파일) : 함수들의 묶음(.py or .ipynb)

**패키지**(폴더) : 모듈 또는 서브 패키지(하위폴더)

(수업) Anaconda3 > Lib에서 확인 가능



### 문법

단, 불러올 때 모듈파일이 같은 폴더 안에 있어야 함

1. 해당 파일이 같은 경로에 있는 경우
2. extend library 에 있는 기본적으로 사용할 수 있는 파일

위의 두 경우는 바로 import 가능

모듈에는 1개 이상의 함수, 변수, 클래스 등이 올 수 있다.

```python
import 모듈이름
모듈이름.함수이름()

# 함수를 바로 불러올 때
# from 모듈이름 import 모듈함수
from mod1 import add
print(add(1,3))

# 모든 함수를 다 쓰고 싶을 때 * 활용
from mod1 import *
print(sub(1,2))
```



### Main module

main module의 내용 main module에서만 시랭하는 방법

```python
if __name__== "__main__":
    print(add(2,3))
    print(sub(4,2))
# mod1에서 mod1(main)을 실행할 때 if부분을 실행
# 즉 해당파일에서만 동작이 실행하도록 해줌

__name__== "__main__"을 사용하면
__name__== "__main__" 조건이 참이됨
따라서 if 문에 있는 문장을 수행
그런데, 외부 파일에서 이 모듈을 불러와 실행할 때는 __name__!= "__main__"이므로
if문이 실행이 안됨
```



### random

> 난수 생성 모듈

```python
import random # random 모듈(random.py)을 가져옴
```



* `random()`

  ```python
  random.random() # 모듈 이름 . 함수 이름
  ```

* `randint()`

  ( ) 안에 난수의 범위 설정 > 정수(int)형태의 난수 생성

  ```python
  i = 0
  while i!=6 :
      print(random.randint(1,45)) # () 안에 난수의 범위 설정 > 정수(int)형태의 난수 출력
      i += 1
  ```

* `choice()`

  choice(시퀀스형)

  시퀀스형 내에서 무작위로 추출

  ```python
  random.choice([1,2,3,4,5,6])
  random.choice("hello")
  random.choice(range(10,20))
  ```

  



## 패키지(package)

파이참 > New > Python package 에서 생성 가능

### 문법

```python
# case1
# import 패키지명.모듈명
import pack1.pack_first
# 패키지명.모듈명.함수명()
pack1.pack_first.prn()

# case2
# from 패키지명.모듈명 import 함수
from pack1.pack_first import prn
# 함수
prn()

# case3
# from 패키지명 import 모듈명
from pack1 import pack_first
# 모듈명.함수명
pack_first.prn()
```



## 예외처리(try)

> 예외 상황이 발생했을 경우를 미리 대비하여 어떻게 처리할 지 미리 정해두는 것

* 예외상황 예시

  1. 없는 파일이거나 (다른 곳으로 파일 이동)

     ```python
     f = open("없는파일.txt", "r")
     ```

  2. 연산과정에서 0이 와서 0으로 나누게 되거나 (ZeroDivisionError 발생)

     ```python
     print(2/0) # ZeroDivisionError 발생
     ```

### `try- except` 문법

try : 기본 시행문장 / except : 오류발생 시 시행문장

```python
try :
    print(2/0)

# print(2/0) 문장을 수행하는 과정에서 예외상황이 발생한 경우
# 만약 ZeroDivisionError 예외상황이면
# 아래와 같은 문장을 수행해라
except ZeroDivisionError as e :
    print("{} | 0으로 나누시면 안됨".format(e))
```



## 