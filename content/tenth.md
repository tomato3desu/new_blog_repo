---
title: eslint × nuxt3設定
description: eslintをnuxt3で設定する方法
image: "images/nuxticon.jpg"
tags: ["typescript", "javascript"]
date: '2025-09-29'
---

1. @nuxt/eslintをインストール

```
npx nuxi module add eslint
```

2. eslint.config.mjsに記述を追加

```
// @ts-check
import withNuxt from './.nuxt/eslint.config.mjs'

export default withNuxt(
  // Your custom configs here
  {
    files: ["**/*.vue", "**/*.ts", "**/*.js", "**/*.mjs"],
    rules: {
      "no-console": "off", <-consoleの記述を許さないやつ、開発中はconsole.logとかするから無効化
      "typescript-eslint/no-explicit-any": "off", <- any許さないやつ、無効化
      "@stylistic/quotes": "off", <- シングルクォートとダブルクォートを統一するやつ、無効化
      "@stylistic/comma-dangle": "off", <-余計なカンマを許さないやつ、無効化
      "@stylistic/eol-last": "off", <- ファイルの最後に改行を強制させるやつ、無効化
      "nuxt/nuxt-config-keys-order": "off" <- keyの順序に口出ししてくるやつ、無効化
    }
  },
  {
    files: ["**/*.vue"],
    rules: {
      "vue/multi-word-component-names": "warn" <- componentsの名前が複数ワードじゃないと怒るやつ
    }
  }
)

```

3. nuxt.config.tsに記述を追加
```
// https://nuxt.com/docs/api/configuration/nuxt-config
export default defineNuxtConfig({
  compatibilityDate: '2025-07-15',
  modules: ['@nuxt/eslint'],
  devtools: { enabled: true },
  eslint: {
    config: {
      stylistic: {
        blockSpacing: true, <- {} これの前後に空白作るやつ
        indent: 2, <- インデントのスペースの数を設定するやつ
        semi: false <- 行末のセミコロン必要か不要か
      }
    }
  }
})
```

4. package.jsonのscriptsに記述を追加
```
"lint": "eslint .",
"lint:fix": "eslint . --fix"
```
これによりnpm run lint でルールに反したコードを検知<br>
npm run lint:fix　で一部のルールに反したコードを自動修正

5. vscodeの設定<br>
プロジェクト直下に.vscode/setting.jsonを作成
```
{
  "editor.codeActionsOnSave": {
    "source.fixAll": true,
    "source.fixAll.eslint": true
  },
  "editor.formatOnSave": true,
  "eslint.validate": [
    "javascript",
    "javascriptreact",
    "vue",
    "typescript",
    "typescriptreact"
  ]
}

```
これでコード記述中にエラー、警告をリアルタイム表示