---
layout: post
title: Learning git
published: true
---

## Git setup in MAC
1. check if already installed

*이미 설치 된지 확인*
```bash
$ git
```qgu

2. Download git !

*깃 다운로드!*
```bash

w install git
```

3. Set who's working in this local repo.

(If u want to use different emails for each project, delete --global)

*현재 로컬 저장소의 사용자 등록*

*(만약 프로젝트마다 다른 이메일 사용하고 싶으면 --global 지워버렷)*

```bash
$ git config [--global] user.name “Shaun Koh”
$ git config [--global] user.email email_id@email_domain.com
```

4. Check git config ( Saved in ~/.gitconfig )

*깃 설정 확인*
```bash
$ git config --list
```

5. Check if public key already exists

*퍼블릭 키 존재 여부 확인*
```bash
$ cat ~/.ssh/id_rsa.pub
```

6. If no directory, generate public key

*디렉토리 없으면 퍼블릭키 생성*
```bash
$ ssh-keygen
```
(press enter three times for public key)

*(엔터 세번 눌러줌)*

7. Check key
*키 확인*
```bash
$ cat ~/.ssh/id_rsa.pub
```

8. Copy key into clipboard

*키 클립보드에 복사*
```bash
$ pbcopy < ~/.ssh/id_rsa.pub
```

9. Add my public key in github’s setting-> SSH and GPG keys, new SSH key

*깃허브 세팅 -> SSH and GPG keys -> new SSH key 에 내 퍼블릭 키 추가*

reference: https://help.github.com/en/github/authenticating-to-github/connecting-to-github-with-ssh

----
TODO FROM HERE
----

## Start git in Mac
1. Change directory (cd) into working dir


2. Initialize git

```bash
$ git init .
```

3. Checking initialization: check .git

```bash
$ ls -al
```
---

<u>Creating Version</u>

Working Tree <-> Starting Area <-> Repository

Repository: where versions are saved // .git directory

*버전 저장되는 곳*

Staging Area: Files that are staged for version

*저장소에 staging 할 파일들 있는곳*

Working Tree: Currently working files that are not staged for version

*현재 작업중인, staging 안될 파일들 있는곳*


---

4. Checking working tree status

```bash
$ git status
```

5. Adding into staging area

```bash
$ git add <filename>
```

6. Creating version from staging area

```bash
$ git commit -m “message 1”
```

7. Creating version from staging area with multiple line messages

```bash
$ git commit
```

8. Add and create version simultaneously

```bash
$ git commit -am “version 2” // untracked files cannot be processed. i.e., new files must be added before at least once with ‘git add ‘
```

9. Show versions

```bash
$ git log
```

10. Show diff stat

```bash
$ git log --stat
```

/* Version difference */

// Show difference

```bash
$ git diff
```

// Delete changes in ORIGINAL file into previous version

```bash
$ git reset --hard
```
// Show patch log

```bash
$ git log -p
```
---
Checkout : converting version

Revert to previous version while preserving all

: controls HEAD’s ptr

---
// master === latest version

```bash
$ git log
```
// Go back to previous version —> does not erase

```bash
$ git checkout <commit_id from git log>
```
// Go back to latest version again

```bash
$ git checkout master
```
---
Version Deletion

RESET

:control
nch that HEAD points

e.g. reset master // means chang
nch’s version to master’s version

e.g. reset version // chang
nch’s version to specific version and unlink(delete) specific version’s post-versions


---
* Not only deletes version, but also currently modifying files : gone from git log

```bash
$ git reset --hard <commit_id>
```
* Delete only version and keep currently modifying files : gone from git log

```bash
$ git reset --soft <commit_id>
```
---
Revert

revert without deleting version: stays in git log

MUST BE reverted from top to down ONE BY ONE

---

```bash
$ git revert <commit_id>
```

* If u do not want to commit specific file, create “.gitignore” file
* tag : nickname for commit id
* git log --all --graph --oneline


##
NCH : multiple operation in one repo

* Sho
nch list : currently in master
```bash
$ gi
nch // * master
$ git log --all --graph --oneline // (HEAD -> master) work 3
```

* Creat
nch
```bash
$ gi
nch
nch_name]
$ gi
nch // * master apple   —>  * means curren
nch
$ git log --all --graph --oneline // (HEAD -> master, apple) work 3 —> HEAD-> means curren
nch
```

### Merging and handling conflict

* 3 Cases:
1. different files —>add together
2. same file w/ different part —> merge automatically
3. same file w/ same part —> CONFLICT


* base : mutual parent

base
nch a — merge commit

  \___ master ___/



* If you want to merge
nch a’ into ‘master’ , first u must be in ‘master
nch
```bash
$ git checkout master
$ git merge
nch_a]
```

* CONFLICT —> select one or both content and erase rest
```
<<<<<<<<< HEAD
content 1
==========
content 2
>>>>>>>>
nch a
```

### 3-way merge

here|base|there|2-way|3-way
:---:|:---:|:---:|:---:|:---:
A|A|A|A|A
H|B|B|conflict|H
C|C|T|conflict|T
H|D|T|conflict|conflict

### Using git mergetool in MAC

1. Download the latest .dmg package for Mac Link: [Meld for OSX][meldlink]
[meldlink]: https://github.com/yousseb/meld/releases/ "go meld"


2. Set git difftool/mergetool: Edit ~/.gitconfig as following
```bash
$ sudo vim ~/.gitconfig
```
```
[diff]
	tool = meld
[difftool]
	prompt = false
[difftool "meld"]
	trustExitCode = true
	cmd = open -W -a Meld --args \"$LOCAL\" \"$PWD/$REMOTE\"
[merge]
	tool = meld
[mergetool]
	prompt = false
[mergetool "meld"]
	trustExitCode = true
	cmd = open -W -a Meld --args --auto-merge \"$PWD/$LOCAL\" \"$PWD/$BASE\" \"$PWD/$REMOTE\" --output=\"$PWD/$MERGED\"
```

3. Test
```bash
$ git difftool
$ git mergetool
```

### Connecting to remote repos

* origin is the nickname for the remote repo
```bash
$ git remote add origin https://github.com/kohpaul/learn_git.git
```

* Check remote repo
```bash
$ git remote
```
* Pushing
```bash
$ git push
```
* If first time, set default remote repo
```bash
$ git push --set-upstream origin master
```
```bash
$ git push -u origin master
```


create a new repository on the command line
echo "# self_learn" >> README.md
git init
git add README.md
git commit -m "first commit"
git remote add origin https://github.com/kohpaul/self_learn.git
git push -u origin master

…or push an existing repository from the command line
git remote add origin https://github.com/kohpaul/self_learn.git
git push -u origin master

References:

https://opentutorials.org/course/3837

https://opentutorials.org/course/3839

https://opentutorials.org/course/3840

https://opentutorials.org/course/3841
