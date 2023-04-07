# ts

## 什么是 TypeScript

TypeScript 是 JavaScript 的超集，意味着它能做 JavaScript 所做的一切，但有一些附加功能。

使用 TypeScript 的主要原因是为 JavaScript 添加静态类型。静态类型意味着变量的类型在程序中的任何时候都不能被改变。它可以防止大量的 bug!

TypeScript 不能被浏览器理解，所以它必须由 TypeScript 编译器（TSC）编译成 JavaScript,我们很快会讨论这个问题。

## 如何设置 TypeScript 项目

需要安装 Node 和 TypeScript 编译器

```bash
# 1. 先安装 node 这里忽略

# 2. 然后通过运行以下命令在你的机器上全局安装TypeScript编译器。
npm i -g typescript
# 检查安装是否成功（如果成功，它将返回版本号:
tsc -v


# init node env
npm init -y

# install typescript
npm install typescript -D

# or
# yarn add typescript -D

# generate ts config: tsconfig.json
tsc --init

# fix code env
# rootDir = "./src"
# outDir = "./dist"
```

## ts 类型

### 基本类型

number, string, boolean, symbol, null, undefined

基元（Primitives）是不可变的（immutable）：它们不能被改变。重要的是，不要将基元本身与分配给基元值的变量相混淆。变量可以被重新分配一个新值，但现有值不能像对象、数组和函数那样被改变。

```ts
let name = "Danny";
name.toLowerCase();
console.log(name); // Danny - the string method didn't mutate the string

let arr = [1, 3, 5, 7];
arr.pop();
console.log(arr); // [1, 3, 5] - the array method mutated the array

name = "Anna"; // Assignment gives the primitive a new (not a mutated) value
```

### 根类型

Object, {}

```ts
let data: Object = new Sec<string>();
let data: {} = new Sec<string>();
// 除了 null 和 undefined 不能给他，其他所有类型都可以给它，它就是超级类型
```

### 对象类型

Array, object, function

```ts
let data: object = { name: "liwei" };
```

数组的应用：

```ts
let ids: number[] = [1, 2, 3, 4, 5]; // can only contain numbers
let names: string[] = ['Danny', 'Anna', 'Bazza']; // can only contain strings
let options: boolean[] = [true, false, false]; can only contain true or false
let books: object[] = [
  { name: 'Fooled by randomness', author: 'Nassim Taleb' },
  { name: 'Sapiens', author: 'Yuval Noah Harari' },
]; // can only contain objects
let arr: any[] = ['hello', 1, true]; // any basically reverts TypeScript back into JavaScript

ids.push(6);
ids.push('7'); // ERROR: Argument of type 'string' is not assignable to parameter of type 'number'.
```

你可以使用联合类型来定义包含多种类型的数组:

```ts
let person: (string | number | boolean)[] = ["Danny", 1, true];
person[0] = 100;
person[1] = { name: "Danny" }; // Error - person array can't contain objects
```

如果你用一个值初始化一个变量，没有必要明确说明类型，因为 TypeScript 会推断出它的类型:

```ts
let person = ["Danny", 1, true]; // This is identical to above example
person[0] = 100;
person[1] = { name: "Danny" }; // Error - person array can't contain objects
```

### enum

enum

### 其他类型

any, unknown, never, void, tuple, mutable tuple.

### 合成类型

联合类型， 交叉类型

联合类型是一个可以被分配到多个类型的变量:

```ts
// let str = "abc";
// str = 3;

// 联合类型
let str: string | number | boolean = "abc";
str = true;

console.log("str:", str);

// 交叉类型
// let obj: { username: string } = { username: "liwei" };
// let obj2: { age: number } = { age: 23 };

type Obj1 = { username: string };
type Obj2 = { age: number };

let obj3: Obj1 & Obj2 = { username: "liwei", age: 34 };
```

### 字面量数据类型

```ts
type A = number | string;
let a: A = "abc";
a = 3;

type num = 1 | 2 | 3;
let n: num = 3;

type increaseFlag = 0 | 1;
function isStartUp(increase: increaseFlag) {
    if (increase) {
        console.log("open");
    } else {
        console.log("close");
    }
}

isStartUp(1);
```

### 引用类型

在 JavaScript 中，几乎 "所有东西 "都是一个对象。事实上（而且令人困惑的是），如果用 new 关键字定义的话，字符串、数字和布尔都可以成为对象:

```ts
let firstname = new String("Danny");
console.log(firstname); // String {'Danny'}
```

但是，当我们谈论 JavaScript 中的引用类型时，我们指的是数组、对象和函数。

## from

-   [面向初学者的 TypeScript 完全指南](https://www.freecodecamp.org/chinese/news/learn-typescript-beginners-guide/)
