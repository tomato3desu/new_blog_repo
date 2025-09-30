---
title: nuxt3 × tailwindcss4
description: nuxt3 × tailwindcss4 の簡単な設定方法
image: "images/nuxticon.jpg"
tags: ["nuxt", "tailwindcss"]
date: 2025-09-30
---

1. tailwindcss4をインストール
```
npx nuxi@latest module add tailwindcss
```
これでnuxt.config.tsのmoduleにtailwindcssの記述が自動で追加される

2. tailwind.config.jsを作成
```
npx tailwindcss init
```
tailwindcssの基本的な機能はここまでで使える

3. assets/css/tailwind.cssを作成し以下を記述
```
@tailwind base;
@tailwind components;
@tailwind utilities;
```

4. google fontsを使う場合
assets/css/tailwind.cssにgoogle fontsのimportを追加
```
@import url("googlefontsのurl");

@tailwind base;
@tailwind components;
@tailwind utilities;

```

tailwind.config.jsを編集
```
/** @type {import('tailwindcss').Config} */
export default {
  content: [　
    "./components/**/*.{vue,js,ts}",　
    "./layouts/**/*.vue",
    "./pages/**/*.vue",
    "./app.vue"　<- tailwindcssを適用する場所のリスト
  ],
  theme: {
    extend: {
      fontFamily: {
        bit: ['"Bitcount Grid Double"', 'sans-serif'], <- このfontをfont-bitで呼び出せるようにしている
      },
    },
  },
  plugins: [],
}

```