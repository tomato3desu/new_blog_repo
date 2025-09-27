---
title: プロになるためのtypescript感想：関数編
description: プロになるためのtypescript（通称ブルーベリー本）を読んで新たに学んだことをまとめました。（関数編）
tags: ["typescript"]
date: '2025-09-27'
---


1. 可変長引数<br>
任意の数の引数を受け取れる。<br>
引数の型は配列にする必要がある
```
const chars = (...chars: string[]): string => {
  let result = ""
  for(const char of chars){
    result += char
    result += " "
  }

  return result
}

// console.log(chars("Hello", "World")) -> "Hello World " 
//console.log(chars("I", "can", "speak", "Japanese")) -> "I can speak Japanese "
// console.log(chars()) -> "" 
```

通常の引数と併用できる
```
const chars = (name: string, ...chars: string[]): string => {
  let result = name + " "
  for(const char of chars){
    result += char
    result += " "
  }

  return result
}

// console.log(chars("Yuu", "is", "cute")) -> "Yuu is cute "
// console.log(chars("Ayumu")) -> "Ayumu "
// console.log(chars()) -> Expected at least 1 arguments, but got 0.(2555)
```

2. スプレット構文と可変長引数の併用

配列をスプレット構文で可変長引数を持つ関数に渡すことができる
```
const chars = (...chars: string[]): string => {
  let result = ""
  for(const char of chars){
    result += char
    result += " "
  }

  return result
}

const sayHello = ["Hello", "World"]

console.log(chars(...sayHello))
```

3. コールバック関数
関数の引数として関数を渡す
```
type User = { name: string, age: number}
const getName = (u: User): string => u.name
const users: User[] = [
  { name: "Shizuku", age: 16 },
  { name: "Emma", age: 18 }
]

const names = users.map(getName)
const names2 = users.map((u:User[]) string => u.name) //getNameを使わない場合
// console.log(names) -> ["Shizuku", "Emma"] 
```
配列はmapの他にもコールバック関数を使ったメソッドが多くある
- filter
- every
- some
- find<br>
など

3. 関数型
```
const sayHello = (num: number):string  => "Hello".repeat(num) //関数型　: (num: number) => string
const sayHi = (num: number) => "Hi ".repeat(num) //返り値の型は省略できる（型推論される）
/* 返り値の型は省略できるが、省略すると関数内で型チェックが働かなくなる＆関数だけ見て引数の型が何かわかりずらくなるので、基本的には省略しないほうが良い */

type repeating = (num: number) => string

const sayGoodbye: repeating = (num: number):string  => "GoodBye ".repeat(num)//関数型も型定義できる
const sayYes: repeating = (num) => "Yes ".repeat(num) //(parameter) num: number　引数の型が推論され省略できる

//関数引数の場合も省略できる
const nums = [1, 2, 3, 4, 5]
const arr = nums.filter((x) => x % 2 === 0)
console.log(arr) //[2, 4]
```

4. ジェネリクス<br>
入力の型は何でもいいが入力の型によって出力する型が決まる場合に有効な書き方
```
function repeat<T>(el: T, length: number): T[] {
  const result: T[] = []
  for(let i = 0; i < length; i++){
    result.push(el)
  }

  return result
}

// console.log(repeat<string>("a", 5)) -> ["a", "a", "a", "a", "a"] 
// console.log(repeat<number>(10, 5)) -> [10, 10, 10, 10, 10] 
```
アロー関数
```
const repeating = <T>(el: T, length: number): T[] => {
  const result: T[] = []
  for(let i = 0; i < length; i++){
    result.push(el)
  }

  return result
}


// console.log(repeating<string>("tomato", 3)) -> ["tomato", "tomato", "tomato"]
```