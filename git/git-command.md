## 명령어

### git fetch

- 원격저장소에 있는 변경내역들을 가져와서 확인
- 원격 저장소에 변경사항이 있는지 확인만 하고, 변경된 데이터를 로컬 Git에 실제로 가져오지는 않음
- **FETCH_HEAD** 는 fetch 명령어 이후 생성되는 임시 브랜치로 체크아웃이 가능함

```bash
git fetch [원격저장소 이름]
# 원격저장소에 변동사항만을 가져 옵니다

git merge FETCH_HEAD
# FETCH_HEAD에 업데이트된 원격저장소의 최신 커밋이, 현재 브랜치에 병합 됩니다.

git fetch; git merge FETCH_HEAD
# git fetch + merge FETCH_HEAD 명령어를 한 번에 사용
```

### git pull

- 원격 저장소로부터 최신 커밋들을 내려받아서, 현재 로컬 브랜치와 **자동으로 병합**을 진행
- fetch 와 merge를 합친 과정

> 💡 **merge 와 rebase는 한 브랜치에서 다른 브랜치로 합치는 방법으로 실행결과는 동일함
> 그러나 커밋 히스토리는 달라짐**

### git merge

- ‘현재' 브랜치에서 [브랜치 명]의 변경사항을 병합

### git rebase

- base를 재설정하는 명령
- 예를 들어 A브랜치에서 B브랜치에 대한 rebase를 할 경우 A브랜치의 Base Commit이 B브랜치의 Head Commit로 변경됨
- 깔끔한 커밋히스토리를 유지 할 수 있음

### git stash

- 변경사항을 일시적으로 저장하고, 이후 stash 공간으로 이동
- git stash pop
  - git stash pop {index 번호}
  - 스택에 쌓인 가장 최근의 변경 사항을 불러와 작업 디렉토리에 적용
  - 이 때, 스택에서 해당 변경 사항은 제거
- git stash apply
  - 스태시를 적용한 후에도 스태시가 적용되어 있는 상태를 유지
  - 임시 저장공간에서 삭제되지 않음
  - 만약 브랜치마다 적용을 하고싶다면 git stash apply를 활용할 수 있습니다.
- git stash list
  - 현재 stash들의 목록을 확인

> 💡 **reset은 되돌려야 할 커밋이 local에만 존재할 경우** **revert은 되돌려야 할 커밋이 push된 경우**

### git reset

- 마지막 커밋을 실행 취소할 수 있음
- 커밋 기록이 변경되기 때문에 사용하지 않는 것을 지향
- --soft : 커밋 취소, staging 상태 유지(add)
- --mixed: 커밋 취소, staging 취소, local 변경 상태로 유지 (default)
- --hard: 커밋 취소, staging 취소, local 변경 상태 취소
- HEAD^: 최신 커밋 취소
- HEAD~(수량) : 수량에 숫자를 적으면 최근커밋부터 해당 숫자까지 커밋 취소

### git revert

- git revert [되돌리고 싶은 커밋 이름]
- 특정 커밋의 내용을 되돌리는 새로운 커밋 생성

### gt rev-parse

- 특정 커밋의 SHA-1 해시 값을 얻는 명령어
