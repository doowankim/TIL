# Git 명령어 정리

### Git repository 연결 및 commit push 하는 법

> 1. github.com 본인 respository 생성 후 만들어지는 url 복사 (ex: https://github.com/repo이름/)
>
> 2. 터미널에서 본인 원격 저장소 연결 후 commit 날리는 법

(1). `git init` : .git이라는 하위 디렉토리를 생성, .git 디렉토리에는 저장소에 필요한 뼈대 파일이 들어있다

(2). `git remote -v` : 원격 저장소 어디에 연결되어 있는지 확인

(3). `git remote add origin "repository url"` : 원격 저장소와 연결해주는 작업

(4). `git add .` : 작성하거나 수정한 코드를 원격저장소에 추가하는 작업

(5). `git commit -m "파일명"` : git add .한 파일의 이름을 정해주는 작업

(6). `git push origin master` : command를 입력하면 원격 저장소에 push 된다


### Git branch 생성

(1). `git checkout -b 브랜치 이름` : ex) git checkout -b feature/a  => feature/a 라는 이름의 branch 생성

(2). `git push origin 브랜치 이름` : ex) git push origin feature/a

> (1), (2) 두 개의 command 입력 시 local과 저장소의 remote branch가 생성된다.
>
> 생성된 branch는 각자가 local 및 저장소 기준이므로, local의 branch를 remote branch와 연동하는 작업을 수행하는 것이 좋다.

(3). `git branch --set-upstream-to origin/브랜치 이름` : ex) git branch --set-upstream-to origin/feature/a
> (3) command 입력 시 branch 연동

### Git branch 삭제
> 작업이 끝나고, 기준 branch로 pull request가 종료되어서 merge까지 완료하였다면 해당 branch를 삭제한다
>
(1). `git checkout develop` : develop branch로 이동(다른 branch로 이동 후 삭제하여야 한다)

(2). `git branch --delete 브랜치 이름` : ex) git branch --delete feature/a

> 여기서, 작업된 사항이나 commit한 이력이 남아있을 경우 (2) 와 같은 command로 branch가 삭제되지 않는 경우도 있다
>
(3). `git branch -D 브랜치 이름` : 강제로 branch 삭제(이 경우, local branch는 삭제되지만 remote branch는 삭제되지 않는다)

(4). `git push origin :브랜치 이름` : ex) git push origin :feature/a (해당 command를 통해 remote branch를 삭제할 수 있다)

### 원격 저장소 URL 변경하기
> 기존 원격 저장소 URL을 변경하기 위해 `git remote set-url` 명령어를 사용한다
>
(1). `git remote -v` : 현재 연결되어 있는 원격 저장소가 어디인지 확인

(2). `git remote set-url origin 새로운 원격저장소 URL` : 새로운 원격저장소 URL에 연결

(3). `git remote -v` : 바뀐 원격 저장소 URL 확인

> * `No such remote '[name]'` => 이 에러는 이름을 변경할 원격 저장소가 없음을 의미한다
