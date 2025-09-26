---
title: eclipseでgit&githubを利用する方法
description: eclipseでgit&githubを利用する方法
image: "images/eclipseicon.jpg"
tags: ["eclipse", "git", "github"]
date: '2025-09-26'
---

# eclipseでgitを利用する方法

1. ローカルリポジトリ作成
パッケージエクスプローラーで右クリック -> チーム -> プロジェクトの共有 -> git -> 作成

2. コミット
gitパースペクティブを開く -> ステージされていない変更をステージされた変更に移動(これがadd) -> コミットメッセージ記述 -> コミット

3. githubでリモートリポジトリを作成

4. プッシュ
eclipseでheadのプッシュ -> ロケーション -> urlにリモートリポジトリのurl貼り付け -> プッシュ[^1]

[^1]:***personal access token を発行していない場合***
github -> setting -> developer settings -> personal access tokens -> token(classic) -> generate new token -> generate new token classic でpersonal access token を作成し、eclipseのpasswordに入力