# Git
* version 관리 툴
* 협업 관리 툴 
* 사실 git flow만 제대로 사용할 줄 알면 된다.

## 개념 
### stage 단위
관련 명령어
* git add 파일
* git status
* git stash save
* git stash apply
* git stash drop
* git stash pop

### 주의
* git add . 은 재앙의 시작
* git 을 되돌리는 용도로 쓰지 않는다. 재앙을 불러온다.
* 내가 깃에 올리는 내용이 뭔지 정확히 파악하고 올려야한다. 

## 커밋
관련 명령어 : git commit -m "커밋메시지" "커밋본문"

### 좋은 커밋 메시지 작성법
1. 제목과 본문을 한 줄 띄워 분리하기
2. 제목은 영문 기준 50자 이내
3. 제목 첫글자 대문자
4. 제목 끝에 . 금지
5. 제목은 명령조로
6. 본문은 영문 기준 72자마다 줄 바꾸기
7. 본문은 어떻게 보다 "무엇"을 "왜"에 맞춰 작성하기  


# Git flow (실제 여러명이 프로젝트에서 Git으로 협업하는 방법)

Source tree를 사용하여 깃 플로우를 쓰길 권장 합니다. <br>
괜히 저처럼 콘솔로 하다가 실수로 파일 add 잘못하는 일이 없길 바랍니다. <br>
Git 은 훌륭한 버전 관리 툴이자, 협업 툴입니다.


## 협업하기 (브랜치 관리 전략)
<img src="https://nvie.com/img/git-model@2x.png">
[우아한 형제 Git flow 설명](http://woowabros.github.io/experience/2017/10/30/baemin-mobile-git-branch-strategy.html)

### master branch
배포용 브랜치!
> 완전한 상태 유지를 위해 직접 커밋을 하지 않는다

### develop branch
코드 병합 작업을 하는 브랜치 
> (다음 버전) 개발을 할 때 쓰는 실질적인 브랜치 

### feature branch.
기능을 집접 다루는 브랜치
> 추가할 때 develop branch에서 분기해서 각 작업을 한 후 develop 에서 합친다

### release branch 
배포(출시)용도를 위해 만든 브랜치, develop과 master에 merge 된다 

### hotfix branch
출시 버전에서 발생한 버그를 수정하는 브랜치 

## Merge 가 되지 않을 때 
* 대부분 코드 수정이 있는데 commit 을 하지 않은 경우 
- git stash를 사용해보자 

* git history 가 다를 경우 
- 누군가가 서버에 올린 후 git reset을 해버림.. 대체로 답이 없기 때문에 해당 시점을 다시 따와서 수정한 코드를 넣는 식으로 해결 

## Git commit log 관리 
어려워짐.. (귀찮아짐), 처음 올릴 때 잘하자 or git squash 를 활용하자 

## Git 도구, 시각화 필요
* [git ignore 생성 사이트](https://www.gitignore.io/)


## 명령어 Cheat sheet


---
# Git online repository
* Git hub 
* Git lab


### See also
* [강추! 우아한 형제 Git flow 설명](http://woowabros.github.io/experience/2017/10/30/baemin-mobile-git-branch-strategy.html)
* [Git branch 전략](https://nvie.com/posts/a-successful-git-branching-model/#release-branches)
* [생활코딩](https://opentutorials.org/course/1492)
* [Toast 커밋 메세지](https://meetup.toast.com/posts/106)
* [Toast git squash](https://meetup.toast.com/posts/39)
* [Git 공부](http://jeong-pro.tistory.com/105?category=798425)

