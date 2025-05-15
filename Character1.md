
# 第1章：JavaScript 概述  

## 一、核心概念  
### 1.1 JavaScript的三大组成部分  
- **ECMAScript**：定义语言核心（语法、数据类型、运算符、语句等）。  
- **文档对象模型（DOM）**：操作HTML/XML文档的树形结构。  
- **浏览器对象模型（BOM）**：操作浏览器窗口、设备功能及全局环境。  

## 二、发展历程  
### 2.1 起源（1995年）  
- 由Brendan Eich为Netscape Navigator 2开发，初名Mocha，后借势Java热度更名为JavaScript。  
- 微软推出JScript（IE中实现），导致多版本语法不统一，推动标准化需求。  

### 2.2 标准化（1997年）  
- ECMA成立TC39委员会，制定**ECMA-262**标准，定义**ECMAScript**规范。  
- 主流浏览器逐步实现规范，统一语法（如IE、Firefox、Chrome）。  

## 三、组成部分详解  
### 3.1 ECMAScript核心内容  
- **语法**：区分大小写，标识符规则（字母/下划线/$开头），严格模式（`"use strict"`）。  
- **数据类型**：6种原始类型（Undefined/Null/Boolean/Number/String/Symbol）+ Object引用类型。  
- **变量声明**：  
  - `var`：函数作用域，存在变量提升。  
  - `let`/`const`：块级作用域，无变量提升，`const`声明常量。  

### 3.2 文档对象模型（DOM）  
- **定义**：将文档抽象为树形节点（如`document`、`element`），支持增删改查节点。  
- **核心模块**：  
  - **DOM Core**：通用节点操作（如`createElement`、`appendChild`）。  
  - **DOM HTML**：HTML特定扩展（如`getElementById`、`querySelector`）。  

### 3.3 浏览器对象模型（BOM）  
- **核心对象**：  
  - `window`：浏览器窗口，全局对象（如`window.innerWidth`、`setTimeout`）。  
  - `navigator`：浏览器信息（如`navigator.userAgent`）。  
  - `location`：URL操作（如`location.href`、`location.reload()`）。  

## 四、ECMAScript版本演进  
### 4.1 主要版本特性对比  
| 版本       | 发布时间 | 核心特性                                                                 |  
|------------|----------|--------------------------------------------------------------------------|  
| **ES1**    | 1997     | 基础语法、数据类型、`Date`/`Math`对象。                                  |  
| **ES5**    | 2009     | 严格模式、`Object.defineProperty`、数组方法（`forEach`/`map`）。         |  
| **ES6（ES2015）** | 2015   | 类（`class`）、箭头函数、模块（`import`/`export`）、解构赋值。           |  
| **ES10（ES2019）** | 2019   | `Array.flat()`、`String.trimStart()`、`Object.fromEntries()`。             |  

## 五、浏览器支持与检测  
### 5.1 主流浏览器支持情况  
- **ES5**：IE9+、Chrome、Firefox、Safari全支持。  
- **ES6+**：现代浏览器（Chrome 49+、Firefox 45+）支持大部分特性，IE不支持ES6+。  

### 5.2 特性检测示例  
```javascript
// 检测箭头函数支持  
if (typeof (() => {}) === 'function') {  
  console.log('支持 ES6 箭头函数');  
} else {  
  console.log('不支持，需引入 polyfill');  
}  
```  

## 六、关键知识点对比  
### 6.1 数据类型检测差异  
| 表达式          | 返回值       | 说明                          |  
|-----------------|--------------|-------------------------------|  
| `typeof null`   | `"object"`   | 历史遗留问题，null 是独立类型 |  
| `typeof []`     | `"object"`   | 数组属于对象类型              |  
| `typeof function`| `"function"` | 函数是特殊对象                |  

### 6.2 作用域声明差异  
| 关键字 | 作用域   | 是否提升 | 是否可重复声明 |  
|--------|----------|----------|----------------|  
| `var`  | 函数作用域 | 是       | 是             |  
| `let`  | 块级作用域 | 否       | 否（同一作用域）|  
| `const`| 块级作用域 | 否       | 否（同一作用域）|  

## 七、面试高频问题  
### 7.1 JavaScript由哪几部分组成？  
**答**：由ECMAScript（核心语法）、DOM（文档操作）、BOM（浏览器交互）三部分组成。  

### 7.2 为什么typeof null返回"object"？  
**答**：早期JavaScript用3位二进制标识类型，null的二进制标识为`000`（对应object类型），导致误判，实际null是独立类型。  

## 八、代码示例  
### 8.1 DOM操作：创建元素并插入页面  
```javascript  
// 创建div元素并设置文本  
const div = document.createElement('div');  
div.textContent = 'Hello DOM!';  
div.style.color = 'red';  

// 插入body  
document.body.appendChild(div);  
```  

### 8.2 BOM操作：获取浏览器信息  
```javascript  
// 输出浏览器名称和版本  
console.log('浏览器名称：', navigator.appName);  
console.log('浏览器版本：', navigator.appVersion);  
```  

## 九、总结  
- **核心重点**：掌握JavaScript三大组成部分的职责，区分ECMAScript与宿主环境（浏览器）的关系。  
- **学习建议**：理解`typeof`的局限性，优先使用`let`/`const`声明变量，避免全局污染。  
- **后续基础**：后续章节将深入ECMAScript语法、DOM/BOM具体接口及实战应用。
