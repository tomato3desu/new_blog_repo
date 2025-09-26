---
title: プロになるためのtypescript感想：オブジェクト編
description: プロになるためのtypescript（通称ブルーベリー本）を読んで新たに学んだことをまとめました。（オブジェクト編）
tags: ["typescript"]
date: '2025-09-26'
---

1. スプレット構文<br>
...オブジェクト名　でオブジェクト作成時に他オブジェクトをコピーできる
```
const yuu = {
    name: "takasaki yuu",
    age: 17
}

const yuu2 = {
    ...yuu,
    grade: 2
}
```

スプレット構文でコピーした値は変更してもコピー元のオブジェクトやスプレット構文で新たにコピーしたオブジェクトには反映されない。これはスプレット構文で複製した分だけオブジェクトができるからだが、オブジェクト内にオブジェクトがある場合、そのオブジェクトは複製されず単一の共通オブジェクトとして扱われてしまう点に注意。
```
const kasumin = {
    name: "nakasu kasumi",
    age: 16,
    threeSize: {
        b: 76,
        w: 55,
        h: 79
    }
}

const kasumin2 = {
    ...kasumin
}

const kasumin3 = {
    ...kasumin2
}

kasumin.name = "kasumin"
kasumin2.age = 17
kasumin3.threeSize.b = 80
console.log(kasumin)
console.log(kasumin2)
console.log(kasumin3)
```
↓結果
```
[LOG]: {
  "name": "kasumin",
  "age": 16,
  "threeSize": {
    "b": 80,
    "w": 55,
    "h": 79
  }
} 
[LOG]: {
  "name": "nakasu kasumi",
  "age": 17,
  "threeSize": {
    "b": 80,
    "w": 55,
    "h": 79
  }
} 
[LOG]: {
  "name": "nakasu kasumi",
  "age": 16,
  "threeSize": {
    "b": 80,
    "w": 55,
    "h": 79
  }
} 
```

2. 分割代入 <br>
const { a, b } = obj の形でオブジェクトのプロパティを取り出せる
```
const setsuna = {
    characterName: "yuki setsuna",
    characterAge: 17
}

const { characterName, characterAge } = setsuna
//console.log(characterName) -> "yuki setsuna" 
//console.log(characterAge) -> 17
```

プロパティ名をそのまま使いたくない場合は別名を付けられる
```
const setsuna = {
    characterName: "yuki setsuna",
    characterAge: 17
}

const { characterName: setsunaName, characterAge: setsunaAge } = setsuna
//console.log(setsunaName) -> "yuki setsuna" 
//console.log(setsunaAge) -> 17
```
ネストしている場合
```
const setsuna = {
    characterName: "yuki setsuna",
    characterAge: 17,
    threeSize: {
        b: 83,
        w: 56, 
        h:81
    }
}

const { characterName: setsunaName, characterAge: setsunaAge, threeSize: {b} } = setsuna
//console.log(setsunaName) -> "yuki setsuna" 
//console.log(setsunaAge) -> 17
//console.log(b) -> 83
```

- 分割代入は便利だが型注釈がつけられない点に注意
- 配列も同様に分割代入可能

3. restパターン<br>
分割代入されたオブジェクトを除く残りのプロパティをすべて持つオブジェクトが作成される

```
const rina = {
    name: "rina tennoji",
    age: 16,
    threeSize: {
        b: 71, 
        w: 52, 
        h: 75
    }
}

const { name: characterName, ...restObj } = rina
//console.log(characterName) -> "rina tennoji" 
//console.log(restObj) -> {
  "age": 16,
  "threeSize": {
    "b": 71,
    "w": 52,
    "h": 75
  }
} 
```