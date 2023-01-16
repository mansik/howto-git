# howto-git-github

#### 참고사이트  

> [git docs](https://git-scm.com/docs)  
> [git book](https://git-scm.com/book/ko/v2) : 필수로 읽어야 함(한국어는 일부 명령어에 대한 설명이 빠져있는 경우 있음)  
> github : new repogitory 생성시 나타나는 가이드  참고  

#### 책

> 팀 개발을 위한 git, github 시작하기

#### 동영상

> [드림코딩-깃,깃허브 제대로 배우기](https://youtu.be/Z9dvM7qgN9s)  
> [코딩알려주는 누나](https://youtu.be/lelVripbt2M)  
> [생활코딩 github](https://youtube.com/playlist?list=PLuHgQVnccGMDWjb0TWItMCfDWDs8Y3Oo7)  
> [github pull request](https://youtube.com/playlist?list=PLuHgQVnccGMBXv1OKe3Hn3Jq6F735-uWm)  
> [Visual Studio Code 로 다루는 Git](https://youtube.com/playlist?list=PLuHgQVnccGMAQvSVKdXFiOo51HUD8iQQm)  
> [Visual Studio Code에서 Git으로 협업하기](https://youtube.com/playlist?list=PLuHgQVnccGMD-XRW1zlqC7U2uCzOxyT8u)  
> [Git and GitHub for Beginners Tutorial](https://youtu.be/tRZGeaHPoaw)  

#### git GUI for windows/mac

> [sourcetree](https://www.sourcetreeapp.com/)

#### 실습 사이트

> [githowto, 예제 및 차례대로 해 볼 수 있음](https://githowto.com/)  
> [git branching 실습](https://learngitbranching.js.org/)

#### 차례

* [git 용어](#git-용어)
* [git 구조, 개념](#git-구조,-개념)
  * github에 git push 할 경우 Authentication failed 오류 발생시 처리
* [git 설정](#git-설정)
* [git 사용 방법 1](#git-사용-방법-1)
  * git 사용 방법 정리
* [git 사용 방법 2](#git-사용-방법-2)
* [git branch 다루기](#git-branch-다루기)
* [git 원격 저장소 다루기](#git-원격-저장소-다루기)
* [좋은 커밋 메지지 7가지 규칙](https://jane-aeiou.tistory.com/93)


# git 용어

* working directory : 현재 작업 directory, 소스가 있는 폴더
* staging area :  일반적으로 Git 디렉터리에 포함된 파일로, 다음 커밋에 포함될 항목에 대한 정보를 저장합니다. index라고도 함.
* repogitory :git directory(저장소) : 소스의 변경사항 히스토리가 저장되는 장소
* branch(브런치) : 개발을 하다 보면 코드를 여러 개로 복사해야 하는 일이 자주 생긴다. 코드를 통째로 복사하고 나서 원래 코드와는 상관없이 독립적으로 개발을 진행할 수 있는데, 이렇게 독립적으로 개발하는 것이 브랜치다.


# git 구조, 개념

* `-----------------------로컬-------------------------------------------|---원격`
* `working directory(=working tree)` --- `staging area` --- `git directory` --- `github`
* (untracked/tracked ) --------------- (staged(=cached)) --- (local repository) --- (remote repository)
* (tracked : git add 한 파일은 git에서 추적 관리, unmodified/modified)
*           <------------------------------------------------------------ clone : 원격저장소에서 복사해서 새로운 디렉토리로 가져오기    
*                                   add ->          commit ->        push ->    : 작업파일들을 원격저장소로 올리기(push)  
*           <------------------------------------------------------------ pull  : 원격저장소의 정보 가져오기(fetch) + 병합하기(merge)  
*                                                                  <---- fetch  : 원격저장소의 정보(이력)만 가져온다. 코드는 안가져온다.


## github에 git push 할 경우 Authentication failed 오류 발생시 처리

* remote: Support for password authentication was removed on August 13, 2021.  
* remote: Please see https://docs.github.com/en/get-started/getting-started-with-git/about-remote-repositories#cloning-with-https-urls for information on currently # # recommended modes of authentication.   
* fatal: Authentication failed for 'https://github.com/mansik/python_project_20221226.git/'  

> github 에서 로그인 password를 사용하지 못하도록 해서 
> https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token 을 따라 작업(아래 설정 참고)


### github Personal Access Token 설정  

* 위치 :  github/Settings/Developer settings/Personal access tokens/Fine-grained

> 다음 항목 read and write  

* Repository access  
  * All repositories 또는 다른 옵션 선택
* Permission  
  * Repository permissions  
    * Contents  (Repository contents, commits, branches, downloads, releases, and merges.)  


# git 도움말 보기

```
git help <verb>

git help config  # config  명령어에 대한 도움말
git add -h # add 명령어에 대한 간략 도움말(-h, --help)
```

# 상태를 확인 하기 위해 사용하는 명령어

```
# it status 명령어는 각 상태에 맞는 명령어 사용법도 보여주므로 참고 하면 된다.
git status # show the working tree status

# commit 후의 log 보기
git log # show the commit logs
git log --oneline 

# 원격저장소 정보 보기
git remote -v  # 원격 저장소명칭과 url을 보기
```

# git config 설정

> 많이 사용하는 명령어

```
6  git config --global user.name "ms"  # user.name setting, (*필수*)
7  git config --global user.email "ms@gmail.com" # user.email setting, (*필수*)  

10  git config --global core.autocrlf true # git 에 저장시 crlf(\r\n) -> lf(\n) 으로 변환, (윈도우에서는 설치시 옵션에서 선택되므로 설정할 필요 없음)
10  git config --global core.autocrlf input # git 에 저장시 줄바꿈문자를 lf(\n) 으로 변환, (맥/리눅스, *필수*)

    git config --global pull.rebase false  # pull 시에 충돌시 rebase 하지 않고 merge  (윈도우에서는 설치시 옵션에서 선택되므로 설정할 필요 없음)
    git config --list
```

```
 1  git config --list  # git config의 list  # (*자주사용하는 명령어*)
 2  git config --global -e # .gitconfig 의 내용 보기  # (*자주사용하는 명령어*)
 3  code . # 현재폴더(.)에서 code(visual studio code)  실행  
 4  git config --global core.editor "code --wait" # git에 설정된 editor을 visual studio code 로 셋팅,  --wait 는 code 가 종료될 때까지 command 가 기다림.  
 5  git config --global -e # editor 실행  
 6  git config --global user.name "ms" # user.name setting, (*필수*)  
 7  git config --global user.email "ms@gmail.com" # user.email setting, (*필수*)
 8  git config user.name # 보기  
 9  git config user.email # 보기  
 11  git config core.autocrlf # 보기
 10  git config --global core.autocrlf true # git 에 저장시 crlf(\r\n) -> lf(\n) 으로 변환, (윈도우에서는 설치시 옵션에서 선택되므로 설정할 필요 없음)
 10  git config --global core.autocrlf input # git 에 저장시 줄바꿈문자를 lf(\n) 으로 변환, (맥/리눅스, *필수*)
 11  git config core.autocrlf # 보기  
 12  git config --list   # 전체 옵션값 보기
 
 # 옵션값 보기 (우선순위 local > global > system)
     git config core.name # core.name 의 옵션값 보기
     git config --list   # 전체 옵션값 보기
     git config --local --list  # 현재 저장소의 옵션값 보기
     git config --global --list  # 현재 사용자의 옵션값 보기
     git config --system --list  # 시스템의 옵션값 보기     
```

# git 사용 방법 1

>  : 아직 버전관리를 하지 않는 로컬 디렉토리 하나를 선택해서 Git 저장소를 적용하는 방법  
>  , 로컬에 git 저장소를 만들고 나서 나중에 github에 올리는 경우  

> 많이 사용하는 명령어

```
> 로컬 저장소 작업
 35  echo .ipynb_checkpoints/ > .gitignore # .gitignore 파일에 git에 올리지 않는 파일 또는 디렉터리를 기록, git에 저장/추적 안됨
 
 14  git init # git 초기화, initialized empty repogitory (*필수*)
 25  git add . # working directory의 모든파일(.)을 staging area 에 추가, 이후 부터 working directory의 파일이 수정될 때마다 변경사항 추적됨(tracked) (*필수*)
 26  git status #  working tree의 상태 보기 (*자주사용하는 명령어*)
 38  git status -s # 간략히 보기(-s : short) (*자주사용하는 명령어*)
 39  git diff # working directory 에서 추적(tracked)인 파일의 변경사항 보기
 40  git diff -staged # staging area의 변경사항 보기
 49  git commit -m "1-4 작업" # staging area의 파일을 git directory 로 이동, message의 내용으로 저장. (*필수*)
 50  git log # commit 한 히스토리 보기 (*필수*)
     git checkout 5813bb5  # 5813bb5 커밋으로 코드를 되돌리기(working directory 의 파일이 해당 커밋으로 변경됨)
     git checkout -  # 최신커밋으로 코드를 되돌리기     
     
 > 원격 저장소 작업  
 64  git remote add origin https://github.com/mansik/python_project_20221226.git # 현재 프로젝트에 원격 repogitory를 origin 이라는 이름으로 추가 (*필수*)
 66  git remote -v # 원격 저장소 세부 보기
 67  git push -u origin master # origin(저장소), master(브런치), -u(set upstream, 이후에서 git push 시 origin, master 을 입력하지 않아도 된다. -u 는 생략가능) (*필수*)
 
 74  git add .
 76  git commit -m "add file"
 77  git push  # 위에서 git push -u 를 사용했으므로 여기서는 생략해도 위에 설정된 저장소, 브런치로 push 된다.
```

> 사용 예시

```
   13  cd /media/ms/My/Documents/python_project_20221226/ # 프로젝트 폴더로 이동
   14  git init # git 초기화, initialized empty repogitory (*필수*)
   15  ls
   16  ls -al
   17  open .git # .git 폴더 열기 (연결된 프로그램으로 연다.)
   18  rm -rf .git # .git 폴더를 지우면 git을 사용안하는 상태로 됨
   19  git init
   20  git status # 현재 repogitory 의 상태 보기
   21  git config --global alias.st status # status 명령을 st로 alias(별칭) 를 만듬
   22  git st # git status 명령과 동일
   23  git config -h # config 명령의 도움말
   24  git status   
   25  git add . # working directory의 모든파일(.)을 staging area 에 추가, 이후 부터 working directory의 파일이 수정될 때마다 변경사항 추적됨(tracked) (*필수*)
   #   git add *.txt # *.txt 를 staging area에 추가
   26  git status
   27  git rm --cached .ipynb_checkpoints/ # staging area 에서 .ipynb_checkpoints/ 폴더 삭제, 하위 디렉터리에 파일이 있으면 삭제 안됨(-r 사용)
   28  git rm --cached -h # 도움말 
   29  git rm --cached -r .ipynb_checkpoints/ # staging area에서 .ipynb_checkpoints/의 하위디렉터리 까지 삭제(-r), --cached / --staged 같음
   30  git status
   31  git rm --cached encoding.ipynb  # staging area에서 해당 파일 삭제, (-r : 하위디렉터리 까지 삭제)
   32  git status
   33  git add encoding.ipynb # staging area에 추가
   34  git status
   35  echo .ipynb_checkpoints/ > .gitignore # .gitignore 파일에 git에 올리지 않는 파일 또는 디렉터리를 기록, git에 저장/추적 안됨
   36  ls -al
   37  open .gitignore 
   38  git status -s # 간략히 보기(-s : short) (*자주사용하는 명령어*)
   39  git diff # working directory 에서 추적(tracked)인 파일의 변경사항 보기
   40  git diff -staged # staging area의 변경사항 보기
   42  git diff --cashed # cashed = staged 동일
   44  git config --global -e
   # .gitcofig 파일에 아래 내용 추가  (difftool 로 code를 셋팅, code = visual studio code)
   # [diff]
   #	tool = vscode
   # [difftool "vscode"]
   #	cmd = code --wait --diff $LOCAL $REMOTE   
   46  git difftool # working directory에서 추적되고 있는 파일(tracked)에서 변경사항이 있으면 vscode가 열림.
   47  git difftool --staged   # staging area 의 파일의 변경사항이 있으면 vscode가 열림.
   49  git commit -m "1-4 작업" # staging area의 파일을 git directory 로 이동, message의 내용으로 저장. (*필수*)
   50  git log # commit 한 히스토리 보기
   51  git status
   52  echo "#(책) Do It! 파이썬 생활프로그래밍 소스" > README.md
   53  git status -s
   54  git commit  -a -m "add readme.md and .gitignore" # -a -m : git add . 명령과 git commit -m "" 의 명령을 같이 실행하는 것과 같음.
   55  git status -s
   56  git commit  -h  # 도움말
   61  git add . # working directory 의 모든 파일을 staging area 로 이동
   62  git commit  -m "add readme.md and .gitignore" # commit message와 함께 commit
   63  git status -s
   64  git remote add origin https://github.com/mansik/python_project_20221226.git # 현재 프로젝트에 원격 repogitory 추가 (*자주사용하는 명령어*)
   65  git remote # 원격 저장소 명칭 보기 (origin)
   66  git remote -v # 원격 저장소 세부 보기
   67  git push -u origin master # origin(저장소), master(브런치), -u(set upstream, 이후에서 git push 시 origin, master 을 입력하지 않아도 된다. -u 는 생략가능) (*필수*)
   68  git remote -v
   69  git remote    
   71  echo "add file" > add.txt
   72  git status
   73  git status -s
   74  git add .
   76  git commit -m "add file"
   77  git push  # 위에서 git push -u 를 사용했으므로 여기서는 생략해도 위에 설정된 저장소, 브런치로 push 된다.
   78  git remote
   79  git remote -v
   80  git push
```

## git 사용 방법 정리

> github에서 저장소를 새로 만들면 아래 가이드 라인이 나타난다.

```
echo "# test" >> README.md
git init
git add README.md
git commit -m "first commit"
git remote add origin https://github.com/mansik/test.git
git push origin master
```

# git 사용 방법 2 

> : 기존 repogitory 를 clone해서 사용시, git init 할 필요 없음

```
git clone https://github.com/mansik/test.git my-test # my-test 폴더로 원격저장소를 다운받아서 사용
또는
cd my-test
git clone https://github.com/mansik/test.git # my-test 폴더로 원격저장소를 다운받아서 사용
cd my-test
git add README.md
git commit -m "first commit"
git push origin master


# 마지막 commit message 변경

git commit --amend -m "첫번째 커밋" # 마지막 commit message 변경
git push -f origin master  # 원격저장소에 강제로  push 


# 마지막 commit 에 수정된 파일 추가 및 commit message 변경하기
git commit -m "initial commit" 
git add .
git commit --amend
```

# git branch(분기) 다루기 

> [3.1 Git Branching - Branches in a Nutshell](https://git-scm.com/book/en/v2/Git-Branching-Branches-in-a-Nutshell)

```
# From Git version 2.23, git checkout 대신 git switch, git restore 을 사용할 수 있음.(git checkout의 기능을 분리 시켰음)

git branch testing  # testing 이라는 새로운 브런치 생성(*자주사용하는 명령어*)
git switch iss53  # 다른 브런치(iss53)로 이동, 해당 브런치의 파일을 working directory로 복사(*자주사용하는 명령어*)
# git checkout iss53  # 다른 브런치(iss53)로 이동, 해당 브런치의 파일을 working directory로 복사(git checkout 대신 git switch 사용)
echo "iss53 branch 에서 작업" > iss53.txt
git commit -a -m 'finished the new footer [iss53]'
.. iss53 브런치에서 작업 후 commit 후 
git log --oneline --decorate --graph --all  # 현재 브랜치가 가리키고 있는 히스토리가 무엇이고 어떻게 갈라져 나왔는지 보여준다.
git switch master  # master 브런치로 이동, git switch - # 이전 브런치로 이동
# git checkout master  # master 브런치로 이동(git checkout 대신 git switch 사용)
git merge iss53  # ss53 브랜치를 master 브랜치에 Merge(합친다) , 다른 브랜치를 현재 switch된 브랜치에 Merge 하는 명령이다.
git switch -c newbranch  # newbranch 를 만들고 switch 까지 한번에 함.(*자주사용하는 명령어*)
# git checkout -b newbranch  # newbranch 를 만들고 checkout 까지 한번에 함.(git checkout 대신 git switch 사용)
```

# git 원격저장소 다루기

> 많이 사용하는 명령어

```
git pull origin master  # 원격저장소(origin)의 브런치(master)을 가져와서 병합한다. fetch + merge (*자주사용하는 명령어*)
git remote -v  # 원격 저장소명칭과 url을 보기
git remote show origin  # 원격 저장소의 URL과 추적하는 브랜치 보기
```

> 사용 예시

```
git remote add origin https://github.com/mansik/python_project_20221226.git  # 현재 프로젝트에 원격 repogitory 추가 (*필수*), git remote add <단축이름> <url> 
git pull origin master  # 원격저장소(origin)의 브런치(master)을 가져와서 병합한다. fetch + merge (*자주사용하는 명령어*)
git remote remove origin  # 현재 프로젝트에서 원격 저장소 삭제
git remote -v  # 원격 저장소명칭과 url을 보기 (*자주사용하는 명령어*)
git remote add origin https://github.com/mansik/python_project_20221226.git

git fetch origin  # 원격 저장소의 내용을 가져온다. working directory 에 적용하지는 않는다. 로컬에서 하던 작업을 정리하고 나서(commit등) 수동으로 Merge 해야 한다

git remote show origin  # 원격 저장소의 URL과 추적하는 브랜치 보기
git remote rename origin paul  # 리모트 저장소의 이름을 변경, origin -> paul 로 변경
git remote  # 결과는 paul 을  보여줌
```
