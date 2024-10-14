# commit 날짜 및 시간 변경하기

#### 커밋을 아직 하지 않은 상태에서 어제 날짜로 commit을 하는 방법

```git
git commit --date "1 day ago" -m "커밋 메시지"
```

<br>

#### 특정 날짜, 시간을 골라서 commit하는 방법

```git
git commit --date "Mon 15 Jan 2024 12:30:00 KST" -m "커밋 메시지"
```

<br>

#### 바로 최근 commit에 날짜를 변경하는 방법

```git
# 최근 커밋을 어제의 현재 시간으로 변경하기 (커밋 수정x)
git commit --amend --no-edit --date "1 day ago"

# 최근 커밋을 특정 날짜, 시간으로 변경하기 (커밋 수정x)
git commit --amend --no-edit --date "Mon 15 Jan 2024 12:30:00 KST"

# 최근 커밋을 어제의 현재 시간으로 변경하기 (커밋 수정o)
git commit --amend --date "1 day ago" -m "커밋 메시지"

# 최근 커밋을 특정 날짜, 시간으로 변경하기 (커밋 수정o)
git commit --amend --date "Mon 15 Jan 2024 12:30:00 KST" -m "커밋 메시지"
```

> `--amend`는 최근 commit의 수정사항을 적용하여 이전 커밋을 덮어씁니다. `--no-edit`은 이전 commit 메시지를 수정하지 않는다는 뜻입니다.

<br>

#### 특정 커밋 날짜 수정하기

프로젝트 경로로 이동한 후 `git log` 명령어를 입력하면 다음과 같이 `commit` 내역을 보여줍니다.

```bash
commit 681e57a56809158d819f01111e59eb31319ea994
Author: # github 이름 및 email 계정
Date:   Sun Jan 14 00:00:00 2024 +0900

commit 8cb15192a41513e3b792b851f8eebfa13439c715
Author: # github 이름 및 email 계정
Date:   Fri Jan 12 14:53:17 2024 +0900
```

이때 수정하고 싶은 커밋 메시지 1칸 아래 해시값을 입력해야 합니다.

```git
# 위에서 일요일 commit 메시지를 수정하려면 아래 금요일 해시값을 입력해야합니다.
git rebase -i 8cb15192a41513e3b792b851f8eebfa13439c715

# 위와 동일한 방법 다른 명령어
# 가장 최신 commit으로부터 2칸 뒤를 지칭하는 명령어
git rebase -i HEAD~2
```

다음과 같은 창이 나오면 변경하려고 했던 커밋의 `pick`을 `edit`으로 변경합니다.

```git
pick 89425cc commit message
pick 271a474 commit message

# Rebase 58a150c..271a474 onto 58a150c (2 commands)
#
# Commands:
# p, pick <commit> = use commit
# r, reword <commit> = use commit, but edit the commit message
# e, edit <commit> = use commit, but stop for amending
# s, squash <commit> = use commit, but meld into previous commit
# f, fixup [-C | -c] <commit> = like "squash" but keep only the previous
#                    commit's log message, unless -C is used, in which case
#                    keep only this commit's message; -c is same as -C but
#                    opens the editor
# x, exec <command> = run command (the rest of the line) using shell
# b, break = stop here (continue rebase later with 'git rebase --continue')
# d, drop <commit> = remove commit
# l, label <label> = label current HEAD with a name
# t, reset <label> = reset HEAD to a label
# m, merge [-C <commit> | -c <commit>] <label> [# <oneline>]
#         create a merge commit using the original merge commit's
#         message (or the oneline, if no original merge commit was
#         specified); use -c <commit> to reword the commit message
# u, update-ref <ref> = track a placeholder for the <ref> to be updated
#                       to this position in the new commits. The <ref> is
#                       updated at the end of the rebase
#
# These lines can be re-ordered; they are executed from top to bottom.
#
```

저장하고 나온 후에 다음 명령어를 입력해야 합니다.

```git
# 원하는 날짜, 시간으로 변경하기
git commit --amend --no-edit --date "Mon 16 Jan 2024 00:00:00 KST"

# 다음으로 넘어가기
git rebase --continue
```

> 중간에 실수 했을 때는 `git rebase --abort`를 입력해서 해당 작업을 중도 취소할 수도 있습니다.

만약 수정된 `commit`을 `push`할 때 `git push -u origin main` 명령어를 입력해야 하는데 에러가 난다면 `git push -f origin main` 명령어를 입력해야 합니다.
