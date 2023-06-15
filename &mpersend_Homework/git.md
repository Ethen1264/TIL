# 📔 Git Command

## 📄 목차
1. Git의 정의
2. Git 설치 & 설정
3. Git 명령어 

<hr>

## 1. Git의 정리


### Git이란
1. Git은 **분산 버전관리 시스템**으로 파일의 변경사항을 추적하고 여러명의 사용자들 간에 파일에 대한 작업을 **조율**하는데 사용된다

### Git의 장점
1. 인터넷 연결이 되지 않는 곳에서도 개발을 할 수 있으며, 저장소가 **삭제**되더라도 **복구**가 가능하다
2. 여러 명이 동시에 작업하는 **병렬 개발**도 가능하다
3. 버전 관리를 하며 **체계적인 개발**이 가능하고, 프로그램이나 패치를 **배포**하는 과정도 간단해진다 

### GitHub
- Git: 형상 관리 도구
- GitHub: 형상 관리 도구(버전 관리) 웹호스팅 서비스
1.  github는 git 저장소를 관리하는 클라우드 기반 **호스팅 서비스** 이다 <br> git 저장소 호스팅 서비스는 클라우드 기반으로 다른 사람과 **소스코드 공유**가 가능하며 git의 기본적인 기능을 확장하여 제공할 수 있다 <br> 또한 클라우드 서버에 소스를 올리기 때문에 한 프로젝트에 여러 명의 사람이 참여하여 **버전 제어** 및 **공동 작업**이 가능하다

<hr>


## 2. Git 설치 & 설정
1. https://git-scm.com/ 링크에 들어가 자신의 OS에 맞는 git을 설치 받기
2. Git을 실행해서 git config --global user.name "**Your_name**"입력.
3. Git config --global user.email "**your_email**"입력 
4. Git config --list를 입력하여 자신이 입력한 정보 확인
<hr>

## 3. Git 명령어

### <새로운 저장소 생성>
``` markdown
$ git init: .git<span> 하위 디렉토리 생성 

$ git clone <https:.. URL>: 기존 소스 코드 다운로드/복제 

$ git clone /로컬/저장소/경로: 로컬 저장소 복제

$ git clone 사용자명@호스트:/원격/저장소/경로: 원격 서버 저장소 복제
```
<br>

### <추가 및 확정(commit)>
``` markdown
$ git add <파일명>: 커밋에 단일 파일의 변경 사항을 포함

$ git add -A: 커밋에 파일의 변경 사항을 한번에 모두 포함

$ git commit -m "커밋 메시지": 커밋 생성

$ git status: 파일 상태 확인
```
<br>

### <가지(branch)치기 작업>
``` markdown
$ git branch: 브랜치 목록

$ git branch <브랜치이름>: 새 브랜치 생성 (local로 만듦)

$ git checkout -b <브랜치이름>: 브랜치 생성 & 이동

$ git checkout master: master branch로 되돌아 옴

$ git branch -d <브랜치이름>: 브랜치 삭제

$ git push origin <브랜치이름>: 만든 브랜치를 원격 서버에 전송

$ git push -u < remote > <브랜치이름>: 	새 브랜치를 원격 저장소로 push

$ git pull < remote > <브랜치이름>: 원격에 저장된 git 프로젝트의 현재 상태를 다운받고 + 현재 위치한 브랜치로 병합
```
<br>

### <변경 사항 발행(push)>
``` markdown
$ git push origin master: 변경사항 원격 서버에 업로드

$ git push < remote > <브랜치이름>: 커밋을 원격 서버에 업로드

$ git push -u < remote > <브랜치이름>: 커밋을 원격 서버에 업로드

$ git remote add origin <등록된 원격 서버 주소>: 클라우드 주소 등록 및 발행
(git에게 새로운 원격 서버 주소 알림)

$ git remote remove <등록된 클라우드 주소>: 클라우드 주소 삭제
```
<br>

### <갱신 및 병합(merge)>
``` markdown
$ git pull: 원격 저장소의 변경 내용이 현재 디렉토리에 가져와지고(fetch) 병합(merge)됨

$ git merge <다른 브랜치이름>: 현재 브랜치에 다른 브랜치의 수정사항 병합

$ git add <파일명>: 각 파일을 병합할 수 있음

$ git diff <브랜치이름><다른 브랜치이름>: 변경 내용 merge 전에 바뀐 내용을 비교할 수 있음
```
<br>

### <태그tag 작업>
``` markdown
$ git log: 현재 위치한 브랜치 커밋 내용 확인 및 식별자 부여됨
```
<br>

### <로컬 변경사항 return 작업>
``` markdown
$ git checkout -- <파일명>: 로컬의 변경 사항을 변경 전으로 되돌림

$ git fetch origin: 원격에 저장된 git프로젝트의 현 상태를 다운로드
```
<hr>

