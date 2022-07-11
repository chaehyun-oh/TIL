# 1주차 summary



## Markdown

텍스트 기반의 가벼운 마크업 언어.

마크다운은 가능한 읽을 수 있도록 최소한의 문법으로 구조화

단순 텍스트 문법으로 내용을 작성하며 다양한 환경에서 변환하여 보여짐



## Git

Git: 분산 버전 관리 시스템

버전 관리, 소스코드 관리: 동일한 정보에 대한 여러 버전을 관리하는 것

commit = **의미있는 저장**, 반드시 작동이 가능한 상태 & 오류가 없는 상태로 커밋

커밋 메세지: 행위에 대한 기록 (eg. 각각 파일 세부 수정 사항)

커밋한 내용은 되돌릴 수 있으나 커밋하지 않은 내용은 돌이킬 수 없음

각 프로젝트 별로 git으로 관리, 한번에 X



### 기초 명령어

- pwd (print working directory): 현재 디렉토리 출력
- cd (chaenge directory): 디렉토리 이동
  - cd .. : 상위 디렉토리로 이동
  - . : 지금 있는 폴더
  - cd 파일명 첫 글자 + tab 하면 자동완성
- ls (list): 목록
- mkdir (make directory): 디렉토리 생성
- touch: 파일의 날짜와 시간을 수정(0바이트 빈 파일 생성)
- rm 파일명: 해당 파일 제거 *(휴지통에 가지않고 바로 제거되니 주의)*
  - rm -r 폴더명: 해당 폴더 제거
- ctrl + l: 명령어 전부 지우기



### Git 기초 명령어

- $ git init
- $ git add <파일명.확장자>
- $ git commit -m '커밋 메세지'
- $ git status
- $ git log
- $ git config -l
- $ git config --global -l
- $ git config user.name





## GitHub

네트워크를 활용한 원격 저장소, GitHub도 버전을 관리함



### 명령어

- $git remote add origin <원격 저장소 주소>
- $ git push <원격 저장소 이름> <브랜치 이름>
- $ git pull <원격 저장소 이름> <브랜치 이름>
- $ git remote -v
- $ git clone <원격 저장소 주소>



Clone과 Pull의 차이점

- Clone: 원격 저장소 복제 (협업 프로젝트, 외부 오픈소스 참여 등)
- Pull: 원격 저장소 커밋 가져오기





## Branch

브랜치의 목적: 독립적인 버전들을 만들어나갈 수 있도록 하기 위함.

HEAD: 전체 커밋중에서 현재 보고 있는 위치를 알려주는 것

브랜치: 특정한 버전들의 흐름 (작업 내역)



### Branch 관련 명령어

- $ git branch : 브랜치 목록 조회
- $ git branch <브랜치 이름> : <브랜치 이름>의 브랜치 생성

- $ git checkout <브랜치 이름> :marter 에서 <브랜치 이름> 브랜치로 이동
- $ git checkout -b <브랜치 이름> : <브랜치 이름>의 브랜치 생성 후 해당 브랜치로 이동
- $ git merge <브랜치 이름> : master 브랜치에서 <브랜치 이름>  브랜치 병합
- $  git branch -d <브랜치 이름> : 해당 브랜치 삭제



### Branch 병합 시나리오

Branch merge: 각 브랜치에서 작업 후 이력을 합치기 위해 merge 사용

병합 진행 시, 만약 서로 다른 이력(commit)에서 동일한 파일을 수정한 경우 충돌 발생할 수 있음.

이 경우엔 반드시 직접 수정을 해야 함.



1. fast-forward:

   브랜치가 생성된 이후 master 브랜치에 변경 사항이 없는 상황 (혼자 작업하는 상황)

   기존 master 브랜치에 변경사항 없이 단순히 앞으로 이동

2.  merge commit

   기존 master 브랜치에 변경사항이 있어 병합 커밋 발생

3.  merge commit 충돌

   서로 다른 이력(commit)을 병합하는 과정에서 같은 파일의 동일한 부분이 수정되어 있는 상황
   원하는 형태로 코드를 직접 수정하고 add, commit 실행해야 함

   

## GitHub Flow

Git Flow: Git을 활용하여 협업하는 흐름. Branch를 활용하는 전략을 의미함

- master (main): 배포 가능한 상태의 코드
- develop (main): feature branch로 나뉘어지거나, 버그 수정 등의 개발을 진행 (개발 이후 release branch로 갈라짐)
- feature branches (supporting): 기능별 개발 브랜치(topic branch), 기능이 반영 또는 드랍되는 경우 브랜치 삭제
- release branches (supporting): 개발 완료이후 QA/test 등을 통해 얻은 minore bug fix 등을 반영
- hotfixes (supporting): 긴급히 반영해야하는 bug fix, release branch는 다음 버전을 위한 것이라면 hotfix는 현재 버전을 위한 것



### Github로 협업하는 방법

1. Feature Branch Wokrflow: 저장소의 소유권이 있는 경우
2. Forking Workflow: 저장소의 소유권이 없는 경우

