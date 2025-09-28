---
title: プロになるためのtypescript感想：ユニオン型編
description: プロになるためのtypescript（通称ブルーベリー本）を読んで新たに学んだことをまとめました。（ユニオン型編）
tags: ["typescript"]
date: '2025-09-28'
---

1. ユニオン型(OR)<br>
const x: string | number のように複数の型を取りうる場合 

```
type Human = {
  name: string
  age: string
}

type Student = {
  name: string
  age: number
  grade: number
}

type User = Human | Student

const yuu: User = {
  name: "Yuu Takasaki",
  age: 17,
  grade: 2
}

function showAge(user: User){
  const age = user.age <- ageは string | number　のユニオン型になる
  console.log(age)
}

```

2. インターセクション型(AND)<br>
オブジェクト型を拡張した新しい型を作るのにつかわれる場合が多い
```
type Human = {
  name: string
  age: number
}

type Student = Human & {
  grade: number
}

const Karin: Student = {
  name: "Karin Asaka",
  age: 18,
  grade: 3
}
```

3. 型の絞り込み<br>
typescriptではuserの型がHumanならばといった条件を直接書くことができないためtag/typeのようなプロパティを使ってオブジェクトの型を絞り込みすることがある
```
function getName(user: User): string {
  if(user.tag === "Human"){
    return user.name
  }else{
    return "名無し"
  }
}

type Animal = {
  tag: "Animal",
  species: string
}

type Human = {
  tag: "Human"
  name: string
}

type User = Animal | Human

const tama: User = {
  tag: "Animal",
  species: "cat"
}

const yuu: User = {
  tag: "Human",
  name: "Yuu Takasaki"
}

// console.log(getName(tama)) -> "名無し" 
// console.log(getName(yuu)) -> "Yuu Takasaki" 
```
