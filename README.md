# howto-git

* 참고사이트  
> [git docs](https://git-scm.com/docs)  
> [git book](https://git-scm.com/book/ko/v2)  
> github : new repogitory 생성시 나타나는 가이드  

#### 차례
* git 용어
* git 구조, 개념
  * github에 git push 할 경우 아래과 같은 오류 발생시 처리
* git 설정
* git 사용 방법 1 
  * git 사용 방법 정리
* git 사용 방법 2 

# git 용어
* working directory : 현재 작업 directory, 소스가 있는 폴더
* staging area :  일반적으로 Git 디렉터리에 포함된 파일로, 다음 커밋에 포함될 항목에 대한 정보를 저장합니다. index라고도 함.
* repogitory :git directory(저장소) : 소스의 변경사항 히스토리가 저장되는 장소
* branch : 

# git 구조, 개념
* `working directory` - `staging area` - `git directory`  -> `github`
*                        (cached/staged)- (repository)  
*  untracked, tracked  
*(tracked : git add 한 파일은 git에서 관리되는 파일)

*             <------------------------------------------- clone : 원격저장소에서 복사해서 새로운 디렉토리로 가져오기    
*                     add ->        commit ->       push ->       : 작업파일들을 원격저장소로 올리기
*             <------------------------------------------- pull   : 원격저장소의 것을 가져오기

## github에 git push 할 경우 아래과 같은 오류 발생시 처리
* remote: Support for password authentication was removed on August 13, 2021.  
* remote: Please see https://docs.github.com/en/get-started/getting-started-with-git/about-remote-repositories#cloning-with-https-urls for information on currently # # recommended modes of authentication.   
* fatal: Authentication failed for 'https://github.com/mansik/python_project_20221226.git/'  

> github 에서 로그인 password를 사용하지 못하도록 해서 
> https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token 을 따라 작업(아래 설정 참고)

### github Personal Access Token 설정  
> 다음 항목 read and write  
* Repository access  
  * All repositories  
* Permission  
  * Repository permissions  
    * Contents  (Repository contents, commits, branches, downloads, releases, and merges.)  

# git 설정
```
> 많이 사용하는 명령어
6  git config --global user.name "ms"  # user.name setting, (*필수*)
7  git config --global user.email "ms@gmail.com" # user.email setting, (*필수*)  
10  git config --global core.autocrlf true # git 에 저장시 \r\n -> \n 으로 저장, (윈도우에서는 *필수*), 리눅스/맥은 해당 없음  
```

```
 1  git config --list  # git config의 list  
 2  git config --global -e # .gitconfig 의 내용 보기  
 3  code . # 현재폴더(.)에서 code(visual studio code)  실행  
 4  git config --global core.editor "code --wait" # git에 설정된 editor을 visual studio code 로 셋팅,  --wait 는 code 가 종료될 때까지 command 가 기다림.  
 5  git config --global -e # editor 실행  
 6  git config --global user.name "ms" # user.name setting, (*필수*)  
 7  git config --global user.email "ms@gmail.com" # user.email setting, (*필수*) >  
 8  git config user.name # 보기  
 9  git config user.email # 보기  
 10  git config --global core.autocrlf true # git 에 저장시 \r\n -> \n 으로 저장, (윈도우에서는 *필수*), 리눅스/맥은 해당 없음  
 11  git config core.autocrlf # 보기  
 12  git config --list  
```

# git 사용 방법 1
>  : 아직 버전관리를 하지 않는 로컬 디렉토리 하나를 선택해서 Git 저장소를 적용하는 방법  
>  , 로컬에 git 저장소를 만들고 나서 나중에 github에 올리는 경우  

```
> 많이 사용하는 명령어
 35  echo .ipynb_checkpoints/ > .gitignore # .gitignore 파일에 git에 올리지 않는 파일 또는 디렉터리를 기록, git에 저장/추적 안됨

 14  git init # git 초기화, initialized empty repogitory (*필수*)
 18  rm -rf .git # .git 폴더를 지우면 git을 사용안하는 상태로 됨
 20  git status # 현재 repogitory 의 상태 보기
 19  git init
 25  git add . # working directory의 모든파일(.)을 staging area 에 추가, 이후 부터 working directory의 파일이 수정될 때마다 변경사항 추적됨(tracked) (*필수*)

 31  git rm --cached encoding.ipynb  # staging area에서 해당 파일 삭제, (-r : 하위디렉터리 까지 삭제)
 38  git status -s # 간략히 보기(-s : short)
 39  git diff # working directory 에서 추적(tracked)인 파일의 변경사항 확인
 40  git diff -staged # staging area의 변경사항 확인
 49  git commit -m "1-4 작업" # staging area의 파일을 git directory 로 이동, message의 내용으로 저장. (*필수*)
 50  git log # commit 한 히스토리 확인
 56  git commit  -h
 64  git remote add origin https://github.com/mansik/python_project_20221226.git # 현재 repogitory 에 원격 repogitory 추가 (*필수*)
 65  git remote # 원격 저장소 명칭 보기 (origin)
 66  git remote -v # 원격 저장소 세부 보기
 67  git push -u origin master # origin(저장소), master(브런치), -u(git push 시 -u 옵션을 사용하면 이후에서 git push 시 origin, master 을 입력하지 않아도 된다.) (*필수*)
 74  git add .
 76  git commit -m "add file"
 77  git push  # 위에서 git push -u 를 사용했으므로 여기서는 생략해도 위에 설정된 저장소, 브런치로 push 된다.
```

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
   23  git config --h # config 명령의 도움말
   24  git status   
   25  git add . # working directory의 모든파일(.)을 staging area 에 추가, 이후 부터 working directory의 파일이 수정될 때마다 변경사항 추적됨(tracked) (*필수*)
   #   git add *.txt # *.txt 를 staging area에 추가
   26  git status
   27  git rm --cached .ipynb_checkpoints/ # staging area 에서 .ipynb_checkpoints/ 폴더 삭제, 하위 디렉터리에 파일이 있으면 삭제 안됨(-r 사용)
   28  git rm --cached --h 
   29  git rm --cached -r .ipynb_checkpoints/ # staging area에서 .ipynb_checkpoints/의 하위디렉터리 까지 삭제(-r), --cached / --staged 같음
   30  git status
   31  git rm --cached encoding.ipynb  # staging area에서 해당 파일 삭제, (-r : 하위디렉터리 까지 삭제)
   32  git status
   33  git add encoding.ipynb # staging area에 추가
   34  git status
   35  echo .ipynb_checkpoints/ > .gitignore # .gitignore 파일에 git에 올리지 않는 파일 또는 디렉터리를 기록, git에 저장/추적 안됨
   36  ls -al
   37  open .gitignore 
   38  git status -s # 간략히 보기(-s : short)
   39  git diff # working directory 에서 추적(tracked)인 파일의 변경사항 확인
   40  git diff -staged # staging area의 변경사항 확인
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
   50  git log # commit 한 히스토리 확인
   51  git status
   52  echo "#(책) Do It! 파이썬 생활프로그래밍 소스" > README.md
   53  git status -s
   54  git commit  -am "add readme.md and .gitignore" # -am : git add . 명령과 git commit -m "" 의 명령을 같이 실행하는 것과 같음.(리눅스에서는 작동이 안되네..ㅠㅠ)
   55  git status -s
   56  git commit  -h
   61  git add . # working directory 의 모든 파일을 staging area 로 이동
   62  git commit  -m "add readme.md and .gitignore" # commit message와 함께 commit
   63  git status -s
   64  git remote add origin https://github.com/mansik/python_project_20221226.git # 현재 repogitory 에 원격 repogitory 추가 (*필수*)
   65  git remote # 원격 저장소 명칭 보기 (origin)
   66  git remote -v # 원격 저장소 세부 보기
   67  git push -u origin master # origin(저장소), master(브런치), -u(git push 시 -u 옵션을 사용하면 이후에서 git push 시 origin, master 을 입력하지 않아도 된다.) (*필수*)
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
```
