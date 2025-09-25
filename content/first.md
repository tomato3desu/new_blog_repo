---
title: nuxt3 × tailwindcss でgoogle fontを利用する方法
description: nuxt3 × tailwindcss でgoogle fontを利用する方法
image: "images/nuxticon.jpg"
tag: ["nuxt", "tailwindcss"]
date: 2025-09-22
---

# nuxt3 × tailwindcss でgoogle fonts を設定する方法

1.google fonts で好きなフォントをカートに追加し、get embed code　をクリック
2.Embed code in the <head> of your html の一番下のリンクからhrefをコピー
3.assets/css/main.cssでimport


assets/main.css
```
/* 1. Google Fonts 読み込み */
@import url("https://fonts.googleapis.com/css2?family=Bitcount+Grid+Double:wght@100..900&display=swap");

/* 2. Tailwind 読み込み */
@tailwind base;
@tailwind components;
@tailwind utilities;
```


nuxt.config.ts
```
export default defineNuxtConfig({
  compatibilityDate: '2025-09-19',
  devtools: { enabled: true },
  css: ['~/assets/css/main.css'], 
  modules: ['@nuxt/image', '@nuxt/eslint', '@nuxtjs/tailwindcss'],
})
```

tailwind.config.js
```
/** @type {import('tailwindcss').Config} */
module.exports = {
  content: [
    "./components/**/*.{vue,js,ts}",
    "./layouts/**/*.vue",
    "./pages/**/*.vue",
    "./app.vue",
  ],
  theme: {
    extend: {
      fontFamily: {
        bit: ['"Bitcount Grid Double"', 'sans-serif'],
      },
    },
  },
}
```
後はfontFamilyで設定した名前をclassで内でfont-名前の形で呼び出すだけ
```
<p class="text-4xl m-4 font-bit">tomato</p>
```