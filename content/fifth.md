---
title: 激浅githubの使い方
description: 一旦githubのリモートリポジトリにpushできればおけな人向け
image: "images/githubicon.jpg"
slug: "fifth"
tags: ["git", "github"]
date: '2025-09-23'
---

# github

**リモートリポジトリ作成**

github で右上の+ボタンを押し、new repository -> create repository
↓のコマンドが出てくるのでそれに沿ってリモートリポジトリにpush

ローカルリポジトリ未作成
```
echo "# my_blog_repo" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main <- メインのブランチ名がmain以外の場合 mainに変更
git remote add origin url <-ローカルリポジトリとリモートリポジトリを紐づけ
git push -u origin main
```

ローカルリポジトリ作成済み
```
git remote add origin url
git branch -M main
git push -u origin main
```

- git branch -m ブランチ名: ブランチ名を変更
- git remote add <リモートリポジトリ名> <リモートリポジトリURL>：ローカルリポジトリとリモートリポジトリを紐づけ
- git push -u <リモートリポジトリ名> <ローカルブランチ名>:<リモートブランチ名（同じ場合省略可能）>  
git push -u の後は git push で更新可能