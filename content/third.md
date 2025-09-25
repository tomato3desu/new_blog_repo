---
title: nuxt × tailwindcss
description: nuxt3 × tailwindcss3 のプロジェクト作成方法、設定
image: "images/nuxticon.jpg"
tags: ["nuxt", "tailwindcss"]
date: 2025-09-21
---

# nxut3 × tailwindcss3プロジェクト作成方法

プロジェクトを作成
```
npx nuxi@latest init プロジェクト名
```

現在デフォルトでnuxt4が入るようになっているので、nuxt3を入れたい場合一度削除して3系を入れなおす
```
npm uninstall nuxt
npm install nuxt@3
```

tsconfig.jsonも3と4で書き方が違うので修正
```
{
  "extends": "./.nuxt/tsconfig.json",
  "compilerOptions": {
    "strict": true,
    "types": ["nuxt"]
  }
}
```

typescriptを使うためnodeの型定義を追加
```
npm install -D @types/node
```

tsconfig.jsonに記述を追加
```
{
  "extends": "./.nuxt/tsconfig.json",
  "compilerOptions": {
    "strict": true,
    "types": ["node","nuxt"]
  }
}
```

tailwindcssのnuxt用モジュールをインストール
```
npm install -D @nuxtjs/tailwindcss
```

assets/css/main.cssを作成
```
@tailwind base;
@tailwind components;
@tailwind utilities;
```

nuxt.config.tsを修正
```
export default defineNuxtConfig({
  compatibilityDate: '2025-07-15',
  devtools: { enabled: true },
  css: ['~/assets/css/main.css'],
  modules: ['@nuxtjs/tailwindcss'],
})
```