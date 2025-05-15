# 第 2 章：HTML 中的 JavaScript

## 一、<script>元素核心属性

### 1.1 基础属性

- **`src`**：指定外部脚本文件路径（如`<script src="app.js"></script>`）。
  - 可跨域加载脚本（需服务器允许），但会阻塞页面渲染。
- **`type`**：指定脚本类型，默认`text/javascript`（可省略），ES6 模块需设置为`type="module"`。
- **`crossorigin`**：配置跨域请求（如`crossorigin="anonymous"`），用于 CDN 脚本的 CORS 设置。

### 1.2 异步与延迟执行

| 属性    | 作用                                                               | 执行时机                       | 适用场景 |
| ------- | ------------------------------------------------------------------ | ------------------------------ | -------- |
| `async` | 异步加载脚本，不阻塞渲染，加载完成后立即执行（无序）。             | 加载第三方脚本（如 Analytics） |
| `defer` | 延迟加载脚本，等待文档解析完成后，按顺序执行（仅适用于外部脚本）。 | 加载多个有依赖的脚本           |

**示例**：

```html
<!-- 异步加载 -->
<script async src="analytics.js"></script>

<!-- 延迟加载（按顺序执行） -->
<script defer src="library.js"></script>
<script defer src="app.js"></script>
```

## 二、标签位置与加载策略

### 2.1 传统位置：头部加载

- **缺点**：阻塞页面渲染，导致白屏时间延长。
  ```html
  <head>
    <script src="old-library.js"></script>
    <!-- 阻塞渲染 -->
  </head>
  ```

### 2.2 优化位置：底部加载

- **优点**：先渲染页面内容，再执行脚本，提升用户体验。
  ```html
  <body>
    <!-- 页面内容 -->
    <script src="app.js"></script>
    <!-- 推荐位置 -->
  </body>
  ```

### 2.3 动态加载脚本

- 使用 DOM 操作动态插入`<script>`元素，实现异步加载（不阻塞渲染）。
  ```javascript
  const script = document.createElement("script");
  script.src = "dynamic.js";
  document.head.appendChild(script);
  ```

## 三、兼容性与特殊场景

### 3.1 XHTML 中的特殊处理

- XHTML 中需严格闭合标签，如：
  ```html
  <script type="text/javascript">
    <![CDATA[
      // 避免XHTML解析错误
    ]]>
  </script>
  ```
- 禁止使用`<script>`标签中的`</script>`字符串，需转义为`<\/script>`。

### 3.2 废弃语法

- 不再支持`language`属性（如`language="javascript"`），统一使用`type="text/javascript"`（可省略）。
- 避免在注释中包裹脚本（如`<!-- ... -->`），现代浏览器已无需此兼容处理。

## 四、行内脚本与外部文件对比

| 类型         | 优点                             | 缺点               | 最佳实践                     |
| ------------ | -------------------------------- | ------------------ | ---------------------------- |
| **行内脚本** | 直接嵌入逻辑，适合少量代码       | 难以维护，无法缓存 | 仅用于简单交互（如事件处理） |
| **外部文件** | 可缓存，分离代码与标记，便于维护 | 需要额外 HTTP 请求 | 所有复杂逻辑均应外置         |

**示例**：

```html
<!-- 行内脚本（不推荐） -->
<button onclick="alert('Hello');">点击</button>

<!-- 外部脚本（推荐） -->
<script src="events.js"></script>
```

## 五、文档模式与兼容性

### 5.1 文档模式分类

- **混杂模式（Quirks Mode）**：模拟旧浏览器行为（如 IE5），需省略`DOCTYPE`声明。
- **标准模式（Standards Mode）**：严格遵循 W3C 规范，需声明`DOCTYPE`（如`<!DOCTYPE html>`）。

### 5.2 DOCTYPE 声明

```html
<!-- HTML5 标准模式 -->
<!DOCTYPE html>

<!-- HTML 4.01 严格模式 -->
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01//EN" "http://www.w3.org/TR/html4/strict.dtd">
```

## 六、<noscript>元素：优雅降级

### 6.1 作用

- 当浏览器不支持 JavaScript 或禁用 JavaScript 时，显示替代内容。
  ```html
  <noscript>
    <p>本页面需要启用JavaScript</p>
  </noscript>
  ```

### 6.2 适用场景

- 提示用户启用 JavaScript。
- 提供非 JavaScript 环境的备用内容（如服务器端渲染 fallback）。

## 七、最佳实践总结

1. **脚本位置**：优先将脚本放在`</body>`前，避免阻塞渲染。
2. **外部脚本**：分离代码，使用`defer`或`async`优化加载顺序。
3. **避免行内脚本**：通过事件监听（如`addEventListener`）替代`onclick`等行内属性。
4. **DOCTYPE 声明**：始终添加`<!DOCTYPE html>`，确保标准模式。
5. **渐进增强**：使用`<noscript>`提供降级体验，同时确保核心功能不依赖 JavaScript。

## 八、代码示例：非阻塞加载脚本

```html
<!-- 异步加载无依赖的脚本 -->
<script async src="analytics.js"></script>

<!-- 延迟加载有顺序的脚本 -->
<script defer src="library.js"></script>
<script defer src="app.js"></script>

<!-- 动态加载（条件判断） -->
<script>
  if (typeof module !== "undefined") {
    const script = document.createElement("script");
    script.src = "module.js";
    document.head.appendChild(script);
  }
</script>
```

## 九、常见问题

- **Q：为什么推荐将脚本放在底部？**  
  A：避免阻塞 HTML 解析和渲染，提升页面加载速度。
- **Q：defer 和 async 的区别？**  
  A：`defer`按顺序执行，适合多个有依赖的脚本；`async`无序执行，适合独立脚本。
- **Q：如何检测浏览器是否支持 JavaScript？**  
  A：无需检测，直接使用特性，通过`<noscript>`处理不支持的场景（渐进增强原则）。
