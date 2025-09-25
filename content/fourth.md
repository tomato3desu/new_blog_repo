---
title: 激浅gitの使い方
description: とりあえずローカルリポジトリにコミットするまでの流れを書きました
image: "images/giticon.jpg"
tags: ["git"]
date: '2025-09-23'
---

# git

- ・git --version:gitのバージョン確認
- ・git status: gitの状態確認
- ・git log: コミット履歴 qで終了
- ・git branch: ローカルブランチの一覧を表示

- gitignore: gitで管理しないファイルを記述したファイル

1. リポジトリ初期化
```
git init
```

2. ステージングエリアに追加

```
git add ファイル名
git add . <-すべて追加
```

3. コミット
```
git commit -m "コミットメッセージ"
```


---　ブランチ ---

・git checkout ブランチ名：　ブランチ切り替え

1. ブランチ作成 & 切り替え
```
git checkout -b ブランチ名
```

2.マージ（今いるブランチに対して指定したブランチをマージ）
```
git merge article/update
```

--- 変更を戻す ---

git log で　commit id　を調べる -> git reset --hard コミットID
***変更したという履歴が残らない***

git log で　commit id　を調べる -> git revert コミットID
***こちらはログに残る***