# 파이썬 기초 (정규표현식 re)



## 정규표현식(re)

> 문자열을 규칙에 맞춰 정리한 것

데이터수집 (정규표현식) -> 전처리 -> 분석

### re

> regular express 정규표현식 모듈

정규표현식 예시

```python
data = """
kim 950101-1234567
lee 970202-2345678
"""
result = []
word_res = []
for line in data.split('\n'):
    word_res = []
    for word in line.split(" "):
        if len(word) == 14 and word[:6].isdigit() and word[7:].isdigit() : # isdigit() : 숫자인지 아닌지 확인해줌
            w = word[0:6] + "-" + "*******"
            word_res.append(w)
    result.append(" ".join(word_res))
            
print("\n".join(result))

# 정규표현식 사용시

import re
# regular express 정규표현식 모듈

data = """
kim 950101-1234567
lee 970202-2345678
"""

pattern = re.compile("(\d{6})[-]\d{7}")
print(pattern.sub("\g<1>-*******",data))
```



### 정규 표현식 작성방법

#### `match()` 

> re.match("패턴", "문자열")
>
> 주어진 문자열에 지정한 패턴이 있는징 여부를 확인

```python
print(re.match("hello", "hello.world"))
print(re.match("hi", "hello.world"))
# None이 나오면 패턴이 없는 것

print(re.match("[0-9]", '123'))
# 패턴이 문자열에 있는지 확인
# span = (0,1)패턴이 매치되는 문자열의 위치
```



#### 정규표현식 메타문자

>문자의 본래 의미가 아닌, 특정 의미를 갖는 문자
>
>() {} [] \ | ? + * $ ^ ...

1. [ ] : 문자와 관련된 정규식 사용 / [] 사이에는 어떤 문자도 올 수 있음

   ex) 정규표현식 : [abcdef] => 의미 : abcdef 여섯개의 문자 중에서 한개의 문자와 매치

   ​	"a"는 정규식에 일치하는 문자가 있으므로 -> 매치됨

   ```python 
   # [] 예시
   print(re.match("[abcdef]", "a")) -> match
   print(re.match("[abcdef]", "z")) -> None
   print(re.match("[abcdef]", "all")) -> match
   print(re.match("[abcdef]", "sky")) -> None
   print(re.match("[abcdef]", "best")) -> match
   print(re.match("[abcdef]", "fgha")) -> f만 match 되어 나옴
   
   print(re.match("[a-z]", "fgha"))
   print(re.match("[a-z]", "ABC"))
   # [a-z] : 알파벳 소문자 모두
   print(re.match("[A-Z]", "ABC"))
   # [A-Z] : 알파벳 대문자 모두
   print(re.match("[a-zA-Z]", "abc"))
   # [a-zA-Z] : 알파벳 대소문자 모두
   
   print(re.match("[0-9]", "119"))
   # [0-9] : 숫자 모두
   print(re.match("\d", "119"))
   # \d : 숫자와 모든 수 [0-9]와 같은 의미
   print(re.match("[^0-9]", "119"))
   # [^0-9] : 숫자를 제외한 모두
   print(re.match("\D", "119"))
   # \D : 숫자가 아닌 모든 것과 매치 [^0-9]와 같음
   
   print(re.match("\w", "test"))
   print(re.match("[0-9a-zA-Z]", "test"))
   # \w : 영문자 숫자 모두 매치 = [0-9a-zA-Z]
   
   print(re.match("\W", "test"))
   print(re.match("[^0-9a-zA-Z]", "대한민국"))
   # \W, [^0-9a-zA-Z] : 영문자, 숫자 외에 모두 매치
   
   print(re.match("[가-핳]", "대한민국"))
   # [가-핳] : 한국어 전체 매치
   ```

2. ^문자열 : 문자열이 맨 앞에 오는지 판단

   문자열$ : 문자열이 맨 뒤에 오는지 판단

   search 함수에서 사용

   ```python
   print(re.search("^hi", "hello.hi")) -> None
   # hi문자열이 맨 앞에 오는지 판단
   print(re.search("hi$", "hello.hi")) -> match
   # hi문자열이 맨 뒤에 오는지 판단
   ```

3. | 문자열 : bar "또는"의 의미

   ```python
   print(re.match("hello|hi|good", "hi"))
   ```

4. `*` : 문자열이 0개 이상 있는지 판단

   ```python
   print(re.match("[0-9]*", '123'))
   # *은 숫자가 0개 이상 있는지 판단 (있을 수도, 없을 수도)
   # 위 코드에서는 숫자 3개가 매치됨
   print(re.match("[0-9]*", '12a3')) # 숫자 2개 매치
   print(re.match("[0-9]*", 'x12a3')) # 0개 매치
   
   print(re.match('a*', "aaab"))
   print(re.match('a*b', "b"))
   # a가 0개 이상 있으면서 b로 이어진다면 매치
   ```

5. `+` : 문자열이 1개 이상 있는지 판단

   ```python
   print(re.match("[a-z]+", "12a3bc")) -> None
   print(re.match("[a-z]+", "abc123def")) -> abc123def
   # + : 문자가 1개 이상 있는지 판단
   
   print(re.match('a+b', "b"))
   print(re.match('a+b', "ab"))
   print(re.match('a+b', "aab"))
   print(re.match('a+b', "aacb")) -> None
   ```

   ** 꼭! **패턴에 대해서** 문자열이 만족을 해야함

6. ? : 문자가 0개 또는 1개가 있는지 확인

   ```python
   print(re.match("h?", "h"))
   print(re.match("h?", "hi"))
   print(re.match("h?", "hello"))
   print(re.match("h?", "ello"))
   # ?는 문자가 0개 또는 1개가 있으면 매치됨
   # h?는 h문자가 0개 또는 1개가 있으면 매치됨
   ```

7. `.` : 문자가 1개 있으면 매치

   ```python
   # h.은 h문자 다음에 문자가 1개 있으면 매치됨
   print(re.match("h.", "h")) -> None
   print(re.match("h.", "hello"))
   print(re.match("h.l", "hello")) # h+문자+ㅣ모양이 나와야 함
   
   print(re.match("a.b", "ab")) -> None
   # a, b사이에 문자가 없어서
   print(re.match("a.b", "acb"))
   print(re.match("a.b", "accb")) -> None
   # a,b사이에 문자가 1개보다 많이 있어서
   ```

8. 문자{횟수} : 문자가 횟수만큼 있는지 확인

   문자열도 가능 (문자열){횟수} : 문자열이 지정된 횟수만큼 반복되는지 확인

   ```python
   # a{3} : a가 3개 있는지 확인
   print(re.match("a{3}", "aaabbbccc"))
   print(re.match("a{3}b", "aaabbbccc"))
   print(re.match("a{3}b*", "aaabbbccc"))
   print(re.match("a{3}b+", "aaabbbccc"))
   print(re.match("a{3}b+c", "aaabbbccc"))
   print(re.match("a{3}b+c*", "aaabbbccc"))
   
   print(re.match("a{3}", "aabbbccc")) -> a가 두개밖에 없음 None
   
   # (문자열){횟수}
   print(re.match("hi{2}","hi")) # h+i2번 나와야 함 -> None
   print(re.match("(hi){2}", "hi")) # hi가 2번 나와야 함 -> None
   print(re.match("(hi){2}", "hihi"))
   ```

* 정규표현식 실제 표현 방법

  ```python
  # 주의 사항 a[.]b = a + . + b
  "[a-z]+[.][a-z]+[.]+com"
  print(re.match("[a-z]+[.][a-z]+[.]+com", "test.abc.com"))
  
  tel1 = "010-1234-5678"
  tel2 = "02-1234-5678"
  print(re.match("[0-9]{3}-[0-9]{4}-[0-9]{4}",tel1))
  print(re.match("[0-9]{3}-[0-9]{4}-[0-9]{4}",tel2))
  print(re.match("[0-9]{2,3}-[0-9]{3,4}-[0-9]{4}",tel2))
  # {2,3} 숫자가 최소 2개 ~ 최대 3개 매치될 수 있음
  
  jm = "990101-1234567"
  check = re.match("[0-9]{6}-[0-9]{7}", jm)
  if check :
      print("정상번호")
  else : 
      print("비정상번호")
  ```




### 정규표현식 개념

1. [] : [] 사이의 문자들과 매치

   정규식 : [ABCDE]

   문자열	 A : 매치, BLUE : 매치, DRY : 매치, SKY : 매치 안됨

2. 

```python
\d <=> [0-9]. \D <=> [^0-9]
\w <=> [a-zA-Z0-9], \W <=> [^a-zA-Z0-9]
```

3. .(dot) : 모든 문자

```python
정규식 : a.b <=> a+모든문자+b
문자열 aab:매치, a0b:매치, abb:매치
absfsdfasfas : 매치안됨
```

4. *(0번 이상 반복)

```python
정규식 : ca*t
문자열  ct:매치,  cat:매치. caaaaat:매치
```

5. +(1번 이상 반복)

```python
정규식 : ca+t <-> a가 1번 이상 반복
문자열  ct:매치x,  cat:매치. caaaaat:매치
```

6. 

```python
ca{2}t <=> c + a는 반드시 2번 반복 + t
{} 안에 있는 숫자만큼 반드시 반복
문자열 cat:매치x, caat:매치
        
{2,5} : 2~5번 반복
ca{2,5}t <=> c + a는 2번이상 5번 이하 + t
문자열 cat:매치x caaat:매치
```

7. ca?t <=> c + a(있어도 없어도 됨) + t
8. \s : whitespace 문자 \n\r\f\t

```python
print(re.match("\s+", 'test'))
print(re.match("\s+", ' test'))
print(re.match("\s+", '  test'))
print(re.match("[a-zA-Z0-9\s]+", 'test HI 99 안녕'))
```

9. | :  or 기호

### 실습

```python
import re

re.match("a.b", "abb")
# re.match(패턴, 문자열)

print(re.match('[a-zA-Z]','hellohi123'))
print(re.match('[a-zA-Z]*','hellohi123'))
print(re.match('[a-zA-Z]+','hellohi123'))
print(re.match('[가-힣]+','반가워 안녕 ㅋㅋㅋ ㅎㅎ'))
print(re.match('[가-힣]+','반가워안녕ㅋㅋㅋㅎㅎ'))

print(re.match('[^a-zA-Z]+','hellohi123')) # 대괄호 안에 꺽쇠
print(re.match('^[a-zA-Z]+','hellohi123')) # 대괄호 밖에 꺽쇠 : 패턴문자로 시작하면 매치가 됨
print(re.match("[^A-Z]", "Hello"))
print(re.match("^[A-Z]", "Hello"))

print(re.match("[0-9]*", "123abc456")) #123
print(re.match("[0-9]+", "123abc456"))
print(re.match("^[0-9]+", "123abc456"))
print(re.search("[0-9]*$", "123abc456")) #456
print(re.search("[0-9]+$", "123abc456"))
==> 끝에서부터 찾으려면 match 함수 말고 search 함수를 써야 함

pat = re.compile('Bye|Hi') # "|" : or 기호
m = pat.match('Byehello')
m = pat.match('Hihello')
m = pat.match('hello')
print(m)
```



### 정규식을 작성하는 일반적인 형식 

[파이썬 라이브러리를 이용한 데이터 분석] p.298

1) 패턴을 저장(re.compile() 함수)

2) 패턴을 사용하여 문자열 검색을 수행(match, search, findall, finditer)



###  정규표현식 함수

* `compile()`

  정규식 저장 => 객체(패턴)

* ` match()` 

  문자열의 처음부터 정규식과 매치되는지 조사

* ` search()`

  문자열 전체에 대해서 정규식과 매치되는지 조사

* `findall()`

  정규식과 매치되는 모든 문자열을 리스트로 리턴

* `finditer()`

  정규식과 매치되는 모든 문자열을 반복가능한 객체로 리턴

* `group()`

  매치된 문자열 출력

* `start()`

  매치 시작위치 출력

* `end()`

  매치 마지막 위치 출력

* `span()`

  매치 (시작, 끝) 위치 출력

```python
# match
m=p.match('python')
print(m)

m=p.match('python')
if m :
    print("매치됨", m.group()) # .group() : 매치된 문자열 출력
    
else:
    print("매치안됨")
print(m)

# search
m = p.search('python')
print(m)

m = p.search('9 python 7 java')
print(m)

# findall
res = p.findall('Life is too short') #[a-z]+
print(res)

# finditer
res = p.finditer('Life is too short') #[a-z]+
print(res) # 반복가능한 타입으로 변경

for i in res :
    print(i)

for i in res :
    print(i.start()) # 매치 시작위치
    print(i.end()) # 매치 끝 위치
    print(i.group()) # 매치 문자열
    print(i.span()) # (시작, 끝)
    
# 알아두기
p = re.compile("[a-z]+")
m = p.match("multi")
# <=> 둘은 같은 의미
m = re.match("[a-z]+", "multi")
```



### 정규식 컴파일 옵션

####  re.DOTALL 옵션

.을 사용할 때, \n문자도 포함하고자 하는 경우

```python
p=re.compile('a.b') # .은 모든 문자와 매치(\n 문자 제외)
m = p.match('a\nb')
print(m)

# DOTALL 옵션 :  .을 사용할 때, \n문자도 포함하고자 하는 경우

p=re.compile('a.b', re.DOTALL) # .은 모든 문자와 매치(\n 문자 제외)
m = p.match('a\nb')
print(m)
```



#### re.I 옵션

ignorecase는 대소문자 구분없이 매치 수행

```python
# re.I 옵션 : ignorecase는 대소문자 구분없이 매치 수행
p = re.compile('[a-z]', re.I) #'[a-zA-Z]'와 같은 의미
m = p.match('Python')
print(m)
```



#### re.MULTILINE 옵션

문자열 모든 라인에 정규식 적용

```python
text = """python one
python two
you need python
"""

p = re.compile("^python\s\w+") # python으로 시작하고 python끝에 공백문자+숫자문자 한글자 이상으로 구성된 패턴
print(p.match(text))
print(p.search(text))
print(p.findall(text)) # ^를 문자열 전체의 처음에 대해서 적용

# 문자열의 각 라인 단위로 정규식(^)를 적용 => MULTILINE
p = re.compile("^python\s\w+", re.MULTILINE) 
print(p.findall(text))
```



[국립국어원](http://www.korean.go.kr) << 가입해두기

##  Grouping

패턴식 내부에 괄호로 묶어서 표현

괄호로 묶인 부분이 그룹이 됨

``` python
pat = re.compile('(xyz)+')
m = pat.search('xyzxyzxyz ok')
print(m.group()) # 매칭된 문자열 출력
```

```python
"""
kim 010-2345-6789
hongkong 02-1234-5678
lee seoul (x)
park 010 1234 5656 (x)
"""

pat = re.compile("\w+\s+\d+[-]\d+[-]\d+")
# m = pat.search("kim 010-2345-6789")
# m = pat.search("hong 02-1234-5678")
# m = pat.search("lee seoul")
# m = pat.search("park 010 1234 5656")
print(m)
```

* 그룹핑 실습

  ```python
  pat = re.compile("\w+\s+\d+[-]\d+[-]\d+")
  m = pat.search("kim 010-2345-6789")
  
  # () : 그룹핑 기호
  # 이름 부분만 그룹핑 => (\w+)
  pat = re.compile("(\w+)\s+\d+[-]\d+[-]\d+")
  m = pat.search("kim 010-2345-6789")
  print(m.group(0))
  print(m.group(1))
  
  # 숫자 모두 그룹핑
  pat = re.compile("(\w+)\s+(\d+)[-](\d+)[-](\d+)")
  m = pat.search("kim 010-2345-6789")
  print(m.group(0)) -> kim 010-2345-6789
  print(m.group(1)) -> kim
  print(m.group(2)) -> 010
  print(m.group(3)) -> 2345
  print(m.group(4)) -> 6789
  
  # 중첩 그룹핑 확인
  pat = re.compile("(\w+)\s+(\d+)[-]((\d+)[-](\d+))")
  m = pat.search("kim 010-2345-6789")
  print(m.group(0)) -> kim 010-2345-6789
  print(m.group(1)) -> kim
  print(m.group(2)) -> 010
  print(m.group(3)) -> 2345-6789
  print(m.group(4)) -> 2345
  print(m.group(5)) -> 6789
  # group이 중첩되는 경우에는 바깥쪽 그룹부터 먼저 배정
  ```

* 그룹핑 이름 설정

  (?P<이름>패턴)

  ```python
  pat = re.compile("(?P<name>\w+)\s+(\d+)[-]((\d+)[-](\d+))")
  m = pat.search("kim 010-2345-6789")
  print(m.group())
  print(m.group('name'))
  ```



## 치환 (sub())

패턴식지정.sub(바꿀문자열, 대상문자열)

=> 대상 문자열에서 패턴이 발견되면 바꿀문자열로 변경해라

```python
pat = re.compile("red")
pat.sub('color', 'blue socks and red shoes') # 치환 red 부분이 color로 변경됨
# 치환 결과 -> 'blue socks and color shoes'
# pat.sub(바꿀문자열, 대상문자열)
# 해석 : 대상 문자열에서 패턴이 발견되면 바꿀문자열로 변경해라

# blue 또는 red는 모두 color로 변경하시오.
# 치환 결과 => 'clor socks and red shoes'
pat = re.compile("red|blue")
pat.sub('color', 'blue socks and red shoes')

pat=re.compile('are') # 패턴
pat.sub("R", "You are duzing off. I'm also sleepy")
# "You are dozing off. I'm also sleepy." 문자열에서
# 'are'패턴이 발견되면, "R"로 치환


pat = re.compile('우리나라|한국|코리아|대한민국')
pat.sub("대한민국", "우리나라 좋은 나라 한국 코리아 대한민국")
# 우리나라, 한국, 코리아, 대한민국 => 대한민국

# 연습문제
# park 010-1234-5678 => 010-1234-5678 park
# grouping, sub 함수 활용
h = re.match("(\w+)\s+(\d+\-\d+\-\d+)", "park 010-1234-5678")
name = h.group(1)
phone = h.group(2)
print(phone + ' ' +name)

# 강사님 답
# p = re.compile("패턴")
# print(p.sub("바꿀문자열","문자열"))
p = re.compile("(?P<name>\w+)\s+(?P<phone>(\d+)[-](\d+)[-](\d+))")
print(p.sub("\g<0> \g<1>","park 010-1234-5678"))
```

* 다른 표현방식

  re.sub("패턴", "바꿀 문자열". "문자열")

  ```python
  # re.sub("패턴", "바꿀 문자열". "문자열") 로도 표현 가능
  
  g=re.sub("우리나라|한국|코리아|대한민국", "대한민국", "우리나라 좋은 나라 한국 코리아 대한민국")
  print(g)
  ```

* re.sub(함수,"문자열")

  ``` python
  def toHex(mat):
      val = int(mat.group())
      return hex(val)
  
  pat = re.compile("\d+")
  pat.sub(toHex,"call 114, 99 for user code")
  ```



