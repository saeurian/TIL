# 파이썬 기초 (환경 세팅, Jupyter notebook, Pycharm)



## 파이썬 환경 세팅

1. 아나콘다 다운로드

   [아나콘다 사이트](https://anaconda.com/) 에서 Download > Windows > Python 3.7 다운로드 > default 옵션으로 next눌러 설치

2. 시작 메뉴에서 아나콘다 파일 (생성됨) 누르면 jupyter notebook 클릭

   * Jupyter notebook : 실제 파이썬을 실행할 프로그램

3. 파일 탐색기 > C 드라이브 > 사용자  > student 폴더가 디폴트로 Jupyter notebook에 등록됨

4. jupyter notebook > Downloads 폴더 클릭 > 오른쪽 상단에 `NEW` 버튼 클릭 후 `Python 3` 클릭 = 새로운 파이썬 코드 파일 생성 (Downloads 폴더에 만드는 이유는 딱히 없음 강사님이 편해서)



## Jupyter notebook

### 기본

* 한 칸(줄)을 "셀"이라고 함

* Web 환경

* 바로 test 가능

* 제목 클릭 하면 수정 가능

* 폴더 관리가 힘들 것 같으면 새로 폴더를 만들어서 저장하거나 하면 됨

* url 부분에서 파일 주소 확인할 수 있음

* 파일 확장자 : `.ipynb` 

* 주피터에서는 print문을 따로 작성하지 않아도 출력이 됨

* But 파이참에서는 print문을 꼭 작성해야 출력이 됨

* 한 셀에 여러 문장을 쓰더라도 print는 가장 마지막 문장이 됨

* 셀 안에 있는 문장을 모두 출력하고 싶으면 print 문법 사용해서 표시해주기

  

### 메뉴

#### File

- New notebook : 새로 생성

- Open : 기존에 있는 것 열기

- Save as : 다른 경로나 다른이름으로 다시 저장

- Download as :  파일 확장자 변경해서 다운로드

  ex) .py는 파이참으로 파일열때 예쁘게 열 수 있음

  Git hub에도 바로 보내서 관리할 수 있음

#### Edit

#### View

- line number 가 보이도록 설정해주면 좋음! (Toggle line number 선택)

#### Insert

- 새로운 셀을 어디에 추가할 것인지 선택가능

#### Cell

- 보통 키보드 단축키로 사용

#### Kernel

* 갑자기 멈추거나 했을 때 사용하면 좋음

#### Widgets



### 실제 실행  (Sell)

* Sell을 실행할 때는 **Shift + Enter**
* Sell 밑에 바로 붙어서 결과가 출력됨
* 오류 문법 일 때 Error 문구가 뜸, 어떤 에러인지 이름, 상세 내용과 어디서 에러가 났는지 확인해야 함



### 메모 방식

1. 긴 문자열 필요 시 """ """ 사용

```python
"""를 세번 치면 """  """ 생기며 안에 넣는 내용은 문자열로 인식함 
```

2. 코드 부연 설명 : Comment sentence 주석문 (비실행문)

``` python
# 앞에 샵을 붙이면 주석문, 코드 부연 설명시 주로 사용
```



## Pycharm

### 설치

이전에 아나콘다로 깔았던 python은 가상 환경

pycharm은 가상환경이 아닌, 로컬에 설치하는 것

1. python을 따로 로컬에서 다운로드 받거나
2. 아나콘다 python을 이용할 수 있음 < 수업에서는 2번 이용

[pycharm 다운로드](https://www.jetbrains.com/pycharm/)에서 다운받아 설치 (community 버전 다운)

시작에서 pycharm 들어가서 테마 등 옵션을 선택하고 next눌러주기

기본으로 아나콘다의 python을 선택함 -> interpretor를 바꿔주면 다운받은 python을 선택할 수 있음



### jupyter notebook 과 호환

jupyter notebook > save as 메뉴에서 .py 파일로 저장 후 오픈 가능

pycharm > 설정 > Project interpreter에서 아나콘다 환경으로 변경하면 pycharm에서 아나콘다의 패키지를 사용할 수 있음



### jupyter notebook 과 다른점

debug 모드를 이용해서 어디서 오류가 나는지 check 지점을 설정하고 확인할 수 있음

프로그래밍하기에 편함

결과를 보려면 print를 꼭 입력해줘야 함