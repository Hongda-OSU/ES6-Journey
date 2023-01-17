### Chapter1: let 和 const 命令
#### --- let 命令
1. 基本用法
> `let`的用法类似于`var`，但是所声明的变量，只在`let`命令所在的代码块内有效
```javascript
{
  let a = 10;
  var b = 1;
}
a // ReferenceError: a is not defined.
b // 1
```
> `for`循环的计数器，合适使用`let`命令 (因为`i`只在`for`循环体内有效）
2. let 不存在变量提升
```javascript
// var 的情况
console.log(foo); // 输出undefined
var foo = 2;
// let 的情况
console.log(bar); // 报错ReferenceError
let bar = 2;
```
3. 暂时性死区
> ES6 明确规定，如果区块中存在`let`和`const`命令，这个区块对这些命令声明的变量，
> 从一开始就形成了封闭作用域。凡是在声明之前就使用这些变量，就会报错。(简单说，在区块内先声明，再使用)
---
#### --- 块级作用域
1. ES6 的块级作用域
```javascript
function f1() {
  let n = 5;
  if (true) {
    let n = 10;
  }
  console.log(n); // 5
}
```
> 上面的函数有两个代码块，都声明了变量`n`，运行后输出 5。这表示外层代码块不受内层代码块的影响。
> 如果两次都使用`var`定义变量`n`，最后输出的值才是 10。
2. 块级作用域与函数声明
> 块级作用域内部，优先使用函数表达式
```javascript
{
  let a = 'secret';
  let f = function () {
    return a;
  };
}
```
> ES6 的块级作用域必须有大括号，如果没有大括号，JavaScript 引擎就认为不存在块级作用域。
---
#### --- const 命令
1. 基本用法 (和let类似）
> `const`声明一个只读的常量。一旦声明，常量的值就不能改变。
```javascript
const PI = 3.1415;
PI // 3.1415
PI = 3;
// TypeError: Assignment to constant variable.
```
> `const`一旦声明变量，就必须立即初始化，不能留到以后赋值。
2. 本质
> `const`实际上保证的，并不是变量的值不得改动，而是变量指向的那个内存地址所保存的数据不得改动 \
> 1. 对于简单类型的数据（数值、字符串、布尔值），值就保存在变量指向的那个内存地址，因此等同于常量。
> 2. 但对于复合类型的数据（主要是对象和数组），变量指向的内存地址，保存的只是一个指向实际数据的指针，
> `const`只能保证这个指针是固定的, 至于它指向的数据结构是不是可变的，就完全不能控制了。(除非用`Object.freez`)
3. ES6 声明变量的六种方法
> `var, function, let, const, import, class`
4. 顶层对象的属性
> 顶层对象，在浏览器环境指的是window对象，在 Node 指的是global对象。\
> 但在ES6中，`let`命令、`const`命令、`class`命令声明的全局变量，不属于顶层对象的属性。
```javascript
var a = 1;
// 如果在 Node 的 REPL 环境，可以写成 global.a
// 或者采用通用方法，写成 this.a
window.a // 1

let b = 1;
window.b // undefined
```
