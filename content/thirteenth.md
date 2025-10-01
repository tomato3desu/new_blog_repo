---
title: nuxt3 × google maps api（マーカー編）
description: nuxt3 × google maps apiのマーカー設定方法
image: "images/nuxticon.jpg"
tags: ["nuxt"]
date: 2025-09-30
---

1. PinElementをインポート

```
const { AdvancedMarkerElement, PinElement } = await importLibrary("marker")
```

2. new PinElementで作成<br>
- background: 背景色
- borderColor: ボーダーの色
- scale: 大きさ
- glyphColor: 中心部の色
- glyph: 中心部の形

```
const pinElement = new PinElement({
            background: "#7fffbf",
            borderColor: "#ff84ff",
            scale: 1.5,
            glyphColor: "white",
            glyph: String(pin.pinId),
            
        })
```

3. マーカー作成時にcontentで指定
```
new AdvancedMarkerElement({
            map,
            position: { lat: pin.lat, lng: pin.lng },
            content: pinElement.element,
        })
```