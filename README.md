# 使用说明

摘要：使用官方推荐的安装流程，初始化 Vue 3 项目，厘清项目文件各部分功能与关系。

## 安装前提

已经安装合适的 Nodejs 环境，测试方法：`node -v`

```bash
$ node -v

//系统返回：
v16.14.0
```

## 创建项目

（1）新建项目文件夹，并进入

```bash
$ mkdir vue-demo

$ cd vue-demo

$ pwd
/Users/zhangminglei/Documents/git/vue-test/vue-demo
```

（2）使用项目初始化指令：`npm init vue@latest`

```bash
$ npm init vue@latest

//系统交互式反馈，输入名称，选择使用【Router】，其余默认
Vue.js - The Progressive JavaScript Framework

✔ Project name: … vue-demo
✔ Add TypeScript? … No / Yes
✔ Add JSX Support? … No / Yes
✔ Add Vue Router for Single Page Application development? … No / Yes
✔ Add Pinia for state management? … No / Yes
✔ Add Vitest for Unit Testing? … No / Yes
✔ Add Cypress for both Unit and End-to-End testing? … No / Yes
✔ Add ESLint for code quality? … No / Yes

Scaffolding project in /Users/zhangminglei/Documents/git/vue-test/vue-demo/vue-demo...

Done. Now run:

  cd vue-demo
  npm install
  npm run dev
```

（3）根据最后提示，进入文件夹，并安装项目

```bash
$ cd vue-demo
$ npm install

//系统反馈：
added 35 packages, and audited 36 packages in 19s

5 packages are looking for funding
  run `npm fund` for details

found 0 vulnerabilities
```

（4）运行`npm run dev`命令，开启开发预览

```bash
$ npm run dev

//系统反馈：
> vue-demo@0.0.0 dev
> vite

Pre-bundling dependencies:
  vue
  vue-router
(this will be run only when your dependencies or config have changed)

  vite v2.8.6 dev server running at:

  > Local: http://localhost:3000/
  > Network: use `--host` to expose

  ready in 588ms.
```

（5）打开 http://localhost:3000/ 查看结果，正常将显示`You did it!`

## 项目结构

使用 `tree` 命令，查看当前文件一级目录结构，如下：

```bash
$ tree -L 1
.
├── README.md
├── index.html
├── node_modules
├── package-lock.json
├── package.json
├── public
├── src
└── vite.config.js

3 directories, 5 files
```

| 序号 | 路径              | 说明                     |
| ---- | ----------------- | ------------------------ |
| 1    | README.md         | 项目说明文档             |
| 2    | index.html        | 项目入口文件【重要】     |
| 3    | node_modules      | nodejs 模块存储文件夹    |
| 4    | package-lock.json | nodejs 模块使用详情文件  |
| 5    | package.json      | nodejs 配置文件 【重要】 |
| 6    | public            | 公共资源文件夹 【重要】  |
| 7    | src               | 项目资源文件夹【重要】   |
| 8    | vite.config.js    | vite 配置文件 【重要】   |

### 核心文件：`index.html`

作用：作为整个项目的入口文件，整合和引入相关资源模块

```html
<!DOCTYPE html> //声明文件类型
<html lang="en">
  <head>
    //声明头信息（编码方式、图标、标题等）
    <meta charset="UTF-8" />
    <link rel="icon" href="/favicon.ico" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Vite App</title>
  </head>
  <body>
    //声明主体内容
    <div id="app"></div>
    //创建一个ID为“app”的div元素
    <script type="module" src="/src/main.js"></script>
    //以模块方式，引入核心js文件
  </body>
</html>
```

### 核心文件：`package.json`

作用：记录项目配置信息（名称、运行脚本、依赖模块等）

```json
{
  "name": "vue-demo",
  "version": "0.0.0",
  "scripts": {
    "dev": "vite", // 以开发模式运行预览，
    "build": "vite build", //打包构建当前项目，输出最终发布文件
    "preview": "vite preview --port 5050" //启动本地静态文件服务器，展示发布文件内容
  },
  "dependencies": {
    "vue": "^3.2.31",
    "vue-router": "^4.0.12"
  },
  "devDependencies": {
    "@vitejs/plugin-vue": "^2.2.2",
    "vite": "^2.8.4"
  }
}
```

### 核心目录：`public`

作用：存放不会被源码引用的静态文件，该目录中的资源在开发时能直接通过 `/` 根路径访问到，并且打包时会被完整复制到目标目录的根目录下。

```bash
$ cd public
$ ls

//系统反馈：
favicon.ico
```

例如，在目录下的文件 `favicon.ico`，在项目当中完整路径为`/public/favicon.ico`，但是在`index.html` 文件当中使用的路径为：`/favicon.ico`

### 核心目录：`src`

作用：存放实际 Vue 项目全部资源文件，包含：

```bash
$ cd src
$ tree -L 2

//系统反馈：
.
├── App.vue
├── assets
│   ├── base.css
│   └── logo.svg
├── components
│   ├── HelloWorld.vue
│   ├── TheWelcome.vue
│   ├── WelcomeItem.vue
│   └── icons
├── main.js
├── router
│   └── index.js
└── views
    ├── AboutView.vue
    └── HomeView.vue

5 directories, 10 files
```

其中：

- 主入口 js 文件：`main.js` 引入 Vue、路由等模块，创建 Vue 实例
- 主入口 Vue 文件：`App.vue` 引入和整合所需视图、组件等内容，定义主视图文件
- Vue 组件文件夹：`components` 最小粒度的 Vue 组件集合
- Vue 视图文件夹：` views` 定义由 Vue 组件等组成的视图
- Vue 路由文件夹： `router` 存放路由文件
- 静态资源文件夹：`assets` 存放需要在代码引用的静态资源，如样式表、logo 等

### 核心文件：`vite.config.js`

作用：实现 Vite 个性化设定

```js
import { fileURLToPath, URL } from "url";

import { defineConfig } from "vite";
import vue from "@vitejs/plugin-vue";

// https://vitejs.dev/config/
export default defineConfig({
  plugins: [vue()],
  resolve: {
    alias: {
      "@": fileURLToPath(new URL("./src", import.meta.url)),
    },
  },
});
```

## 打包构建

执行命令：`npm run build`

```bash
$ npm run build

//系统反馈：
> vue-demo@0.0.0 build
> vite build

vite v2.8.6 building for production...
✓ 41 modules transformed.
dist/assets/logo.da9b9095.svg        0.30 KiB
dist/index.html                      0.48 KiB
dist/assets/AboutView.f79b56c4.js    0.25 KiB / gzip: 0.21 KiB
dist/assets/AboutView.ab071ea6.css   0.08 KiB / gzip: 0.10 KiB
dist/assets/index.2b32a27e.js        11.17 KiB / gzip: 4.37 KiB
dist/assets/index.038ca730.css       3.87 KiB / gzip: 1.26 KiB
dist/assets/vendor.13977def.js       69.73 KiB / gzip: 27.77 KiB

```

执行完毕后，会在根目录下新产生一个 `dist` 文件夹，包含项目最终用于发布的静态工程文件：

```bash
$ cd dist
$ tree -L 2

//系统反馈：
.
├── assets
│   ├── AboutView.ab071ea6.css
│   ├── AboutView.f79b56c4.js
│   ├── index.038ca730.css
│   ├── index.2b32a27e.js
│   ├── logo.da9b9095.svg
│   └── vendor.13977def.js
├── favicon.ico
└── index.html

1 directory, 8 files
```

## 本地预览

运行：`npm run preview`，将在本地`dist` 文件夹，启动一个网页服务器：

```bash
$ npm run preview

//系统反馈：
> vue-demo@0.0.0 preview
> vite preview --port 5050

  > Local: http://localhost:5050/
  > Network: use `--host` to expose

```

打开：http://localhost:5050/ 可以查看最终网页效果。

**参考官方文档：**

- [Home | Vite 官方中文文档](https://cn.vitejs.dev/)
- [快速开始 | Vue.js](https://staging-cn.vuejs.org/guide/quick-start.html#with-build-tools)
