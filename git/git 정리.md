
### 새로운 저장소 생성
```git init```<br>
현재 디렉토리 기준 git 저장소 생성

-------------
### 원격 저장소

```git remote -v```<br>
현재 디렉토리와 연결된 원격 저장소 확인

```git init```<br>
git 등록

```git remote add (저장소 이름) (URL)```<br>
원격 저장소 연결

```git remote rename (기존이름) (변경할 이름)```<br>
원격 저장소 이름 변경

```git remote remove (저장소이름)```<br>
원격 저장소 삭제

```git clone (URL)```<br>
원격 저장소 복제

-------------
### 커밋 추가
```git add (파일명)```<br>
커밋에 단일 파일의 변경 사항을 추가

```git add . ```<br>
커밋에 모든 파일 추가

```git add -A```<br>
커밋에 파일의 변경 사항을 한번에 모두 포함

------------
### 커밋
```git commit -m "커밋 메세지"```<br>
커밋 생성

--------

```git status```<br>
파일 상태 확인

```git branch```<br>
브랜치 목록

```git branch (브렌치이름)```<br>
새 브렌치 생성 (local로 만듦)

```git checkout -b (브랜치이름)```<br>
브랜치 생성 & 이동

```git branch -d (브랜치이름)```<br>
브랜치 삭제

```git branch -m (새로운 브랜치이름)```<br>
현재 브랜치 이름 변경

```git branch -m (현재 브랜치이름) (새로운 브랜치이름)```<br>
다른 브랜치 이름 변경

-------
### 푸쉬
```git push origin main```<br>
원격 저장소에 업로드

### 병합
```git merge (다른 브랜치이름)```<br>
현재 브랜치에 다른 브랜치의 수정사항 병합

```git pull```<br>
원격 저장소의 변경 내용이 현재 디렉토리에 가져와지고(fetch) 병합(merge)됨

----------
## .gitignore
### 프로젝트 중간에 .gitignore 작성한 경우
$ git rm -r --cached .
$ git add .
$ git commit -m "git ignore add"
$ git push
