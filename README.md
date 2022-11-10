# web-sourcecode-analysis 源码阅读系列
## 项目初始化

1. 安装依赖

```bash
npm install
# or 
pnpm install
# or
yarn 
```

2. `scripts` 脚本命令说明

|  名称   | 作用  | 用法 |
|  ----  | ----  | ---- 
| serve  | 启动本地Web服务（便于 esm 模块使用） | `pnpm run serve`
| dev:vue3  | 本地启动 Vue3 开发构建，支持热更新，sourcemap | `pnpm run dev:vue3`
| dev:vue3_esm  | 本地web服务调试，用于 esm 模式下调试 Vue3 源码 | `pnpm run dev:vue3_esm`
| dev:vue3  | 用于 umd 模式下调试 Vue 源码 | `pnpm run dev:vue3`

3. **VsCode** 调试说明

- 配置 `.launch.json`，具体详情[点击](https://go.microsoft.com/fwlink/?linkid=830387)

## Vue3

> 依赖初始化
```bash
pnpm i
```

可以在 `vue3\examples` 中编写你的 Vue 代码，并通过 vscode 进行埋点调试，支持 esm 和 umd 模式下的源码调试。

> ps: esm 模式下需要基于web服务下才可以加载成功

项目中分别编写了在 esm 和 umd 模式下的调试代码。可以通过以下的步骤以及简单案例来编写并调试你的代码。

**ESM 编写调试 Vue3**
<video id="video" controls="" preload="none" >
    <source id="mp4" src="./static/videos/vue3_esm.mp4" type="video/mp4">
</videos>
1. 执行 `npm run dev:vue3_esm` 开启 `本地 web 服务`并 构建 `Vue3` 开发环境代码（自带热更新，sourcemap），可通过 `Vue3 esm 调试` 来调试源码。

2. ESM 模式下的 html 编写

> vue3\examples\index.html

```html
<div id="app"></div>
<!-- ESM 使用以下方式 -->
<!-- 加载测试脚本 -->
<script type="module" src="./reactive/reactive.esm.js"></script>
```

3. js 文件的编写

> vue3\examples\reactive\reactive.esm.js

```js
// 加载 vue.esm-browser.js 文件
import * as Vue from '../../node_modules/vue/dist/vue.esm-browser.js'
const {reactive} = Vue
console.log(reactive({name: 'coderookie262'}))
```


**UMD 编写调试 Vue3**
<video id="video" controls="" preload="none" >
    <source id="mp4" src="./static/videos/vue3_global.mp4" type="video/mp4">
</videos>

1. 执行 `npm run dev:vue3` 构建 `Vue3` 开发环境代码（自带热更新，sourcemap），可通过 `Vue3 global 调试` 调试源码

2. UMD 模式下的 html 编写

> vue3\examples\index.html

```html
<div id="app"></div>
<!-- 加载 js 文件 -->
<script src="../node_modules/vue/dist/vue.global.js"></script>
<!-- 加载测试脚本 -->
<script src="./reactive/reactive.global.js"></script>
```

3. js 文件的编写

> vue3\examples\reactive\reactive.global.js

```js
const {reactive} = Vue
console.log(reactive({name: 'coderookie262'}))
```

