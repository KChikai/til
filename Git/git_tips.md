# Git Tips 

gitを使う際によく使うコマンド例．
雑なので注意．

<br>

## How to make a new repository

### 空のremote repositoryが既に作っている状態時

1. `mkdir hoge`  
2. `cd hoge` 
3. `git init`  
4. git add and commit + make remote repository
5. `git push --set-upstream [repository_URL] master`

### repositoryの作成で先にlocal repositoryを作成した場合

1. remoteにrepositoryを作成
2. `remote add <short_name> <remote_url>` で紐付け (short_nameは通常origin)
3. `git push --set-upstream origin master` でremoteにpush
4. remote repository nameを変更する際は`remote rename <old_name> <new_name>`

### git push時のfatal errorについて 

    git push origin HEAD:master

<br><br>


## 取り消し関連

### 一個前のコミットを取り消す

Example1
	`git add hoge` (通常通りファイルを追加)
	`git commit --amend -m “hoge commit”` (前のcommitは残したまま(反映させない)，新しいcommitを加える)

Example2
	`git reset --soft HEAD^`  (ワーキングツリーの内容はそのまま，前のcommitを完全に消去する)

Example3 
	`git reset --hard HEAD^` (ワーキングツリーの内容毎，前のcommitを削除し，二つ前のcommitの状態に戻る)

### git ignore の途中反映

キャッシュの消去が必要．変更分が消えるので注意．

    git rm -r --cached .


<br><br>

## Branch 


### 用語関連

- `master`
 : デフォルトのブランチ名 (svnでのtrunkと同じ)

- `origin`
 : リモートのサーバ名（デフォルト）

- `master`
 : 作業ディレクトリと結び付いているのがmasterブランチ．（ローカルリポジトリのブランチ）
　作業ディレクトリでファイルを更新してコミットする場合はmasterに入る．
　git cloneでリポジトリをコピーした場合，リモートブランチmasterがコピーされる．
    origin/masterはmasterにとっての上流ブランチ (引数なしでgit pullした時に対象になるブランチ) である．

- `origin/master`
 : リモートリポジトリにあるリポートブランチmasterと結びついているブランチ．
　origin/masterは，リポートブランチmasterをローカルリポジトリで
　トラッキングするためのブランチ（リモートトラッキングブランチ：リモート追跡ブランチ（git fetchで更新されるブランチの事））．
　リモートブランチを参照するために利用しています．
　このブランチは変更できません．「origin/master」というのは、originという名前の
　リモートリポジトリにあるmasterブランチをトラッキングしていることを意味する．


### Tips about branch

- `git branch -a`：ブランチ全体の表示（上部がローカルブランチ，下部・赤色の文字がリモートブランチを表す）
- `git checkout -b branch_name`：ブランチ作成とそのブランチへの切り替え(git branch branch_name + git checkout branch_name)
- `git push —set-upstream origin branch_name`：リモートへのローカルbranchの反映
- `git branch -r`：リモートブランチの確認
- `git checkout -b branch_name origin/branch_name`：リモートブランチをローカルにクローンする．


### remote branch をローカルに反映

    git branch new-branch origin/new-branch

ex)

    ChikaiMacBookPro:makoto near$ git branch django origin/django
    Branch django set up to track remote branch django from origin.


<br><br>

## GitHub関連

### git fork したリポジトリを本家に追従する方法

1. ローカルにforkしたブランチに移動
2. `git remote add root_branch [本家のgit_URL] `
3. `git remote fetch root_branch`
4. `git merge root_branch/master`

	(root_branchで名前でなくても良いはず)


### pull-request model

1. 対象のリポジトリをclone
2. `git checkout -b [branch-name]`
3. `git add` 
4. `git commit` 
5. `git push origin [branch-name]`
6. github上でpull-req
7. merge (これは管理者が行う)
