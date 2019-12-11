# Git

> Git은 분산형 버전 관리 시스템(DVCS) 이다.
>
> 소스코드 형상 관리 도구로, 코드의 이력을 관리 할 수 있다.

## Git 로컬 저장소 활용하기

> git은 `repository`(`저장소`) 로 각각 프로젝트를 관리한다.

### 0. 기본 설정

Git에서 이력을 남기기 위해 작성자(author) 정보를 추가한다. 매 컴퓨터에서 최초로 한 번만 설정하면 된다.

```bash
$ git config --global user.nave {유저네임}
$ git config --global user.email {이메일}
```

* 일반적으로 {`유저네임`}, {`이메일`}에는 github 정보를 넣는다. (중괄호 제외)
* 설정이 잘 되었는지 다음 코드로 확인한다.

```bash
$ git config --global -l
```

### 1. 저장소 생성

```bash
$ git init
Initialized empty Git repository in C:/Users/student/Desktop/TIL/.git/
(master) $
```

**github 시작할 때 디렉토리에서 오른쪽 버튼 클릭 - "`git bash here`" 로 들어가기

### 2. add

> 커밋 대상 파일을 `staging area`로 이동 시킨다.
>
> 즉, 이력을 남길 파일을 담아 놓는 것이다.

`.` 은 현재 디렉토리(폴더)를 뜻한다.

```bash
$ git add .	# 현재 디렉토리 모두 stage
$ git add git.md	# 특정 파일만 stage
$ git add images/	# 특정 폴더만 stage
```

항상 `git status` 명령어를 통해 상태를 확인하자.

```bash
$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   Azure Pass - Multicampus.txt
```



### 3.  `commit`

> git에서 이력을 남기기 위해서는 커밋을 진행 == 확정을 진행한다.

``` bash
$ git commit -m 'Git 기초'
[master 037e7da] Git 기초
 1 file changed, 36 insertions(+)
 create mode 100644 Git.md
```

* 이력을 확인하기 위해서는 `git log` 를 활용한다.

```bash
$ git log
commit 037e7da5fe5a3b36265cf43b824b8378bba63bde (HEAD -> master)
Author: saeurian <sa_eurian2@naver.com>
Date:   Thu Dec 5 12:39:44 2019 +0900

    Git 기초

commit 09a6afc0920afe643671622e13b6b1ba675805c8
Author: saeurian <sa_eurian2@naver.com>
Date:   Thu Dec 5 12:36:44 2019 +0900

    Git 기초
```

## 원격 저장소 활용하기

### 0. 기본 설정

> 원격 저장소를 생성한다. (예 - github)

### 1. 원격 저장소 등록

`origin`이라는 이름으로 해당 url을 원격 저장소로 등록

최초에 한번만 하면 된다.

```bash
$ git remote add origin https://github.com/saeurian/TIL-a.git
```

```bash
$ git remote -v
origin  https://github.com/saeurian/TIL-a.git (fetch)
origin  https://github.com/saeurian/TIL-a.git (push)
```

** git remote -v 저장소 목록 확인 가능

### 2. 원격 저장소 push

앞으로 변경되는 사항이 있으면 항상 `add`, `commit`, `push`를 진행한다.

```bash
$ git push -u origin master
Enumerating objects: 8, done.
Counting objects: 100% (8/8), done.
Delta compression using up to 4 threads
Compressing objects: 100% (8/8), done.
Writing objects: 100% (8/8), 46.09 KiB | 11.52 MiB/s, done.
Total 8 (delta 0), reused 0 (delta 0)
To https://github.com/saeurian/TIL-a.git
 * [new branch]      master -> master
Branch 'master' set up to track remote branch 'master' from 'origin'.
```

