---
title: nuxt3 × google maps api
description: nuxt3 × google maps apiの設定方法
image: "images/nuxticon.jpg"
tags: ["nuxt"]
date: 2025-09-30
---

1. googlemaps/js-api-loaderをインストール
```
npm install @googlemaps/js-api-loader
```

2. apikeyを取得して.envに記述

3. nuxt.config.tsに記述を追加
```
// https://nuxt.com/docs/api/configuration/nuxt-config
export default defineNuxtConfig({
    compatibilityDate: '2025-07-15',
    devtools: { enabled: true },
    modules: ['@nuxtjs/tailwindcss', '@nuxt/eslint'],
    eslint: {
        config: {
            stylistic: {
                blockSpacing: true,
                indent: 4,
                semi: false
            }
        }
    },
    runtimeConfig: {
        public: {
            googleMapApiKey: process.env.GOOGLE_MAP_API_KEY
        }
    }
})
```

4. componentを作成
```
<script setup>
import { setOptions, importLibrary } from "@googlemaps/js-api-loader"

const config = useRuntimeConfig() // .envの値をruntimeConfig経由で取得
const mapElement = ref(null) // templateのdivと紐づけ(document.getElementById('')のvue.js版)

onMounted(async () => {
    // apiキー設定
    setOptions({
        key: config.public.googleMapApiKey,
        v: "weekly",
    })

    // ライブラリ読み込み
    const { Map } = await importLibrary("maps")

    // マップ描画
    new Map(mapElement.value, {
        center: { lat: 35.6809591, lng: 139.7673068 },
        zoom: 8
    })
})
</script>

<template>
    <div
        ref="mapElement"
        class="h-screen"
    />
</template>
```
- onMounted(): vueではtemplateがブラウザに描画された後でないとDOM操作ができないため、地図の描画はonMounted内で描画を行う