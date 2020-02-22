# 什么是babel?
babel是js编译器，它可以转换语法、@babel/polyfill兼容不同目标环境的特性、进行源码转换等。

e.g：将es6的箭头函数转换成普通函数：
// Babel Input: ES6 arrow function
[1, 2, 3].map((n) => n + 1);

// Babel Output: ES5 equivalent
[1, 2, 3].map(function(n) {
  return n + 1;
});

## 可以编译es6及以上版本js
Babel通过语法转换可以支持最新版本的js。
在这些babel插件的帮助下我们可以使用最新的js语法，而不必等浏览器更新支持这些新的js特性才能使用。

**ts** babel不会对ts进行类型检查，可以安装@babel/preset-flow检查类型

## 插件化
Babel是各种插件化构成的