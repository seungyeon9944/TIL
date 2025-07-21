## 수정사항 쓰고 저장을 꼭 하자 !! 

## `git init`
git 저장소로 초기화


## `git add` <파일명>
git에 추가할 준비 **(staging area로 이동)**


## `git commit -m` <메시지>
staging에 있는 내용을 기록


## `git status`
현재 변경사항 내역 + staging area 표시


## `git log`
여태까지 변경내역들 확인


## `git log –oneline`
Commit 목록 한 줄로 보기


## `git config –global -l`
설정정보 보기


## Vim (text editor) 
`i`를 쓰면 insert, 
`esc`로 명령어 입력
`:wq`로 write와 quit
혹은 `git commit –amend -m “amend commit”` (+ 직전 `commit`이라면 전체 수정도 가능)

---

# 원격 저장소 
Remote Repository, 온라인 상에서 저장하고 공유할 수 있게 하는 저장공간
원격 저장소 서비스의 예시로는 Gitlab, Github, Bitbucket
`git remote add origin https://주소`


## `git push <name> <branch>` 혹은 `git push origin master`
`push`하면 local에서 Github repository로
내 저장소의 변경내역(`commit`)들을 원격에 푸시한다


## `git pull <name> <branch>` 혹은 `git pull origin master`
`pull`하면 Github repository에서 local로 
원격 저장소에 있는 내용을 가져온다


## 절차 : **`add - commit – push`**
![원격저장소절차](https://miro.medium.com/max/3834/1*g-iW9rUZVeHSdKNnVbAuQg.png)


## `git clone <url>`
저장소를 복제해 온다.


## `gitignore` 
git이 추적하지 않도록 설정하는데 사용되는 텍스트파일 (ex. API 키, .vscode, .idea 등등)
- `.gitignore`도 그냥 txt 파일이기 때문에 `add – commit – push` 절차가 필수적임	
- Gitignore.io 웹사이트 통해서 파일 먼저 생성하는 것도 가능


## `git` 기타 명령어
- `git remote -v`
현재 로컬 저장소에 등록된 원격 저장소 목록 보기
- `git remote rm` 원격_저장소_이름
현재 로컬 저장소에 등록된 원격 저장소 삭제


## `git revert` 
**(올라간 후의 커밋)** 특정 commit을 없었던 일로 만드는 작업, 없애고 싶은 commit의 반대를 적용해서 원상복구함, 없애고싶은 commit이 사라지지는 않음. 기록이 손실되는 것을 방지하며 기록의 무결성과 협업의 신뢰성을 높임


## `git reset`
**(올라가기 전의 커밋, 최대한 지양)** 특정 commit으로 되돌아가는 작업, 되돌아간 commit 이후의 (push 이후의) commit은 모두 삭제. 
`git reset` [옵션] <`commit id`>의 형태

[옵션] 자리에는
- **--soft** (파일은 남아있음 다음에 commit할 수 있도록 되어있음) 
- **--mixed** (다음에 add할수 있도록 함, 완전히 지워지지는 않음)
- **--hard** (파일도 같이 사라짐) 


## `git restore`
변경상태의 파일을 working directory에서 수정사항 취소


## `git rm --cached`
staging area에 있는 내용을 working directory로 되돌리기