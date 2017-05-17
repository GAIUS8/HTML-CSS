#17년 05월 16일
<a href="https://git-scm.com/book/ko/v2/Git-%EB%8F%84%EA%B5%AC-Stashing%EA%B3%BC-Cleaning"><참고URL1></a>    
<a href="https://git-scm.com/book/ko/v2/Git-%EB%8F%84%EA%B5%AC-%EA%B2%80%EC%83%89"><참고URL2></a>   
<a href="https://git-scm.com/book/ko/v2/Git-%EB%8F%84%EA%B5%AC-Stashing%EA%B3%BC-Cleaning"><참고URL3></a>

##stashing & cleaning

###상황
현재 수정중인 파일이 있음

```
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)
	
	modified:   project1.txt
	
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)
	
   modified:   project2.txt

```

###stash 사용하기

- 여기서  이 파일들을 커밋하지 않고 다른 작업을 우선적으로 해야할 일들이 생긴다. 이때 이들 파일을 따로 저장해두었다가 나중에 다시 작업하고 싶을 때, stash를 쓴다.

	```
	$ git stash
	Saved working directory and index state WIP on master: ca02e2c project2.txt added 
	```
	
	```
	$ git status
	On branch master
	nothing to commit, working tree clean
	```
	워킹 디렉토리가 깨끗해졌다.

- stash된 파일들을 확인하기   
	```$ git stash list ```

	```
	stash@{0}: WIP on master: 95bccf2 new file added
	stash@{1}: WIP on master: ca02e2c project2.txt added
	```

- stash된 파일 다시 사용하기
	
	```
	$ git stash apply (가장 최근에 stash된 것 불러옴)
	or
	$ git stash apply stash@{1} (지정하여 불러옴)
	```

- $ git stash apply 하면

	```
	On branch master
	Changes not staged for commit:
   (use "git add <file>..." to update what will be committed)
   (use "git checkout -- <file>..." to discard changes in working directory)
	
	       modified:   new.txt
	
	no changes added to commit (use "git add" and/or "git commit -a")
	```
	
	최근의 modified	되었던 파일이 다시 working space로 들어온다.

- 아까 stage 상태였던 녀석들은?

	```
	$ git stash apply stash@{1}
	
	On branch master
	Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)
	
	modified:   new.txt
	modified:   project1.txt
	modified:   project2.txt
	
	no changes added to commit (use "git add" and/or "git commit -a")
	```
	
	stash 상태에서 가져오면 그냥 modifing 상태로 가져온다( staging이 취소됨)   
	 그래서 git stash apply 명령을 실행할 때 --index 옵션을 주어 Staged 상태까지 적용한다. 그래야 원래 작업하던 상태로 돌아올 수 있다.
	 

- 스택에 남아 있는 stash 된 파일들 제거하기

	``` $ git stash drop ``` stash 한개씩만 제거 된다. (모두 제거는 clear 옵션)

- ```git stash --keep-index```.  
	현재 staging area에 있는 파일은 빼고 나머지 modified 파일들만 stash영역으로 이동해줌

- 추적하는 파일이든(기존에 있던 파일) 추적하지 않는 파일이든(방금 새로 만든 파일) 모두 stash 영역으로 보내는 옵션.  
	``` git stash -u```

- stash 한것을 다시 불러오기 전에 테스트 하기

	```
	$ git stash branch test-branch
	
	Switched to a new branch 'test-branch'
	On branch test-branch
	Changes to be committed:
	  (use "git reset HEAD <file>..." to unstage)
	
		modified:   new.txt
	
	Untracked files:
	  (use "git add <file>..." to include in what will be committed)
	
		untracked.txt
	
	Dropped refs/stash@{0} (428ce96394bb3a90adb8d4f5ba9e761784745331)
	```
	새로운 브렌치(test-branch)에서 이전의 파일들이 불러와진다. 이 상태에서 테스트 진행후 병합을 하던지 버리던지 하면 된다.
	
- 위키 디렉토리 청소하기
	```git clean``` : 워킹디렉토리 안에 추적하고 있지 않은 모든 파일을 삭제한다.   
	추적 중이지 않은 모든 정보를 워킹 디렉토리에서 지우고 싶다면 ```git clean -f -d ``` 사용한다. -f 옵션은 강제(force)의 의미이며 "진짜로 그냥 해라"라는 뜻이다.

   *이렇게 지우는 것은 복구가 안되기 때문에 일단 stash 상태로 옮기는 것이 더 좋다. 그 이후 지울지 말지를 판단하는 것이 더 옳다.

**[추가로 궁금했던 것]**
stash 저장을 할 때, 이름을 붙이려면 어찌 해야 하는가?

``` git stash save "named stash"```

이렇게 저장된다.

 ```
 stash@{0}: On test-branch: named stash
 stash@{1}: WIP on master: 95bccf2 new file added
 ```


###검색하기
#### git grep
Git의 `grep` 명령을 이용하면 커밋 트리의 내용이나 워킹 디렉토리의 내용을 문자열이나 정규표현식을 이용해 쉽게 찾을 수 있다.(파일 안의 내용까지 모두 검색)

[option]

- 명령을 실행할 때 -n 옵션을 추가하면 찾을 문자열이 위치한 라인 번호도 같이 출력한다.
- 어떤 파일에서 몇 개나 찾았는지만 알고 싶다면 `--count`옵션을 이용한다.
- 매칭되는 라인이 있는 함수나 메서드를 찾고 싶다면 -p 옵션을 준다.
- --and 옵션을 이용해서 여러 단어가 한 라인에 동시에 나타나는 줄 찾기 같은 복잡한 조합으로 검색할 수 있다.
- --break`와 `--heading 옵션을 붙여 더 읽기 쉬운 형태로 잘라서 출력할 수도 있다.

[git greap의 장점]   
git grep 명령은 grep 이나 ack 같은 일반적인 검색 도구보다 몇 가지 좋은 점이 있다. 우선 매우 빠르다. 또한, 워킹 디렉토리만이 아니라 Git 히스토리 내의 어떠한 정보라도 찾아낼 수 있다.

#### git log
어떤 변수가 어디에 있는지를 찾아보는 게 아니라, 히스토리에서 언제 추가되거나 변경됐는지 찾아볼 수도 있다. git log 명령을 이용하면 Diff 내용도 검색하여 어떤 커밋에서 찾고자 하는 내용을 추가했는지 찾을 수 있다.

[option]

- -S 옵션을 이용해 해당 문자열이 추가된 커밋과 없어진 커밋만 검색할 수 있다.
- 더 세세한 조건을 걸어 찾고 싶다면 로그를 검색할 때 -G 옵션으로 정규표현식을 써서 검색하면 된다.
- **라인 히스토리 검색** git log`를 쓸 때 `-L 옵션을 붙이면 어떤 함수나 한 라인의 히스토리를 볼 수 있다. 예를 들어, zlib.c 파일에 있는 ```git_deflate_bound``` 함수의 모든 변경 사항들을 보길 원한다고 생각해보자. ```git log -L :git_deflate_bound:zlib.c```라고 명령 실행하면 된다. 


##커밋 수정하기
###가장 최근의 커밋 메세지 수정하기

```git commit --amend```  : 이 명령은 자동으로 텍스트 편집기를 실행시켜서 마지막 커밋 메시지를 열어준다. 여기에 메시지를 바꾸고 편집기를 닫으면 편집기는 바뀐 메시지로 마지막 커밋을 수정한다.

**[주의사항!!]**
**이때 SHA-1 값이 바뀌기 때문에 과거의 커밋을 변경할 때 주의해야 한다. Rebase와 같이 이미 Push 한 커밋은 수정하면 안 된다.**


###여러개의 커밋 메세지 수정하기
1. ```git rebase -i HEAD~3``` 입력(여기서는 최근에서부터 3번째꺼까지 조회)
2. 화면창에 변경할 commit을 선택하여 pick이 있는 곳에 pcik을 지우고 edit 입력 후 텍스트 에디터 저장후 나가기
3. 그다음부턴 terminal 지시에 따름
4. (지시) ```git commit --amend``` edit을 설정한 commit	중에서 가장 옛날 것의 commit message 변경 화면이 나온다. 여기서 변경하고 싶은대로 변경하고
5. (지시) ```git rebase --continue``` 하면 최종적으로 변경이 완료 됨.
6. 여러개의 commit을 연속으로 바꾸고자 할때는 처음 pick을 여러개 동시에 edit	으로 바꾼다음에 연속되는 지시에 따라 ```git commit --amend```와 ```git rebase --continue```를 반복하면 된다.


###커밋 순서 바꾸기
위의 커밋 편집기에서 순서를 바꾸면 되는데, 충돌에 유의해야 한다.


### 편집기에서 merge하기 (3개 이상의 파일 merge)
‘`pick’이나 ‘`edit'말고 ``squash’'를 입력하면 Git은 해당 커밋과 바로 이전 커밋을 합칠 것이고 커밋 메시지도 Merge 한다. 그래서 3개의 커밋을 모두 합치려면 스크립트를 아래와 같이 수정한다.

pick f7f3f6d changed my name a bit
squash 310154e updated README formatting and added blame
squash a5f4a0d added cat-file
저장하고 나서 편집기를 종료하면 Git은 3개의 커밋 메시지를 Merge 할 수 있도록 에디터를 바로 실행해준다.

	 
##Reset

###트리의 종류
- HEAD : 마지막 커밋 스냅샷, 다음 커밋의 부모 커밋
- Index : 다음에 커밋할 스냅샷 - staging area
- 워킹디렉토리 : 샌드박스

<img src="https://git-scm.com/book/en/v2/images/reset-workflow.png">


###reset의 역할
트리를 예측가능한 방법으로 조작

1단계: HEAD	이동 : 현재 브렌치가 가리키는 커밋만 이전으로 되돌림.
2단계: Index 업데이트  : reset에 아무 명령어도 안쓰면 기본적으로 --mixed옵션으로 실행 스테이징 에어리아에 있는 것들을 비우고 가장 최근의 커밋으로 되돌림.
3단계: 워킹 디렉토리 업데이트 : --hard옵션 - 워킹 디렉토리의 내용까지 전부 되돌림.

[다시보기].  
reset 명령은 정해진 순서대로 세 개의 트리를 덮어써 나가다가 옵션에 따라 지정한 곳에서 멈춘다.

1.HEAD가 가리키는 브랜치를 옮긴다. (--soft 옵션이 붙으면 여기까지)

2.Index를 HEAD가 가리키는 상태로 만든다. (--hard 옵션이 붙지 않았으면 여기까지)

3.워킹 디렉토리를 Index의 상태로 만든다.


####경로를 주고 Reset 하기
예를 들어 git reset file.txt 명령을 실행한다고 가정하자. 이 형식은(커밋의 해시 값이나 브랜치도 표기하지 않고 `--soft`나 `--hard`도 표기하지 않은) `git reset --mixed HEAD file.txt`를 짧게 쓴 것이다.

1. HEAD의 브랜치를 옮긴다. (건너뜀)

2. Index를 HEAD가 가리키는 상태로 만든다. (여기서 멈춤)

본질적으로는 file.txt 파일을 HEAD에서 Index로 복사하는 것뿐이다.   
<img src="https://git-scm.com/book/en/v2/images/reset-path1.png">. 

####합치기 (squash)
```git reset --soft HEAD~2```
<img src="https://git-scm.com/book/en/v2/images/reset-squash-r2.png">

```git commit```
<img src="https://git-scm.com/book/en/v2/images/reset-squash-r3.png">

###checkout
HEAD를 직접 옮겨서 관리한다. 작업 시에는 여러가지 시도를 해보고 변경하지 않은 파일만 업데ㅣ트를 하는 등 reset보다 지능적으로 기능한다.
 
