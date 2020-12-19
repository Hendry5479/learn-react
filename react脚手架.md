**三大框架的脚手架**：
Vue的脚手架：vue-cli
Angular的脚手架：angular-cli
React的脚手架：create-react-app
**React脚手架的意义**：解决前端工程复杂的问题
React脚手架默认node包管理工具**yarn**
### create-react-app
**目录结构分析**：
```
test-react
├─ README.md 
├─ package.json // 对应用程序的描述：包括应用名称、依赖包、以及项目启动、打包等等（node管理项目必备文件）
├─ public
│    ├─ favicon.ico // 应用顶部的icon图标
│    ├─ index.html // 入口文件
│    ├─ logo192.png // 被在manifest.json中使用
│    ├─ logo512.png // 被在manifest.json中使用
│    ├─ manifest.json // 和Web app配置相关
│    └─ robots.txt // 指定搜索引擎可以或者无法爬取哪些文件
├─ src
│    ├─ App.css // App组件的样式
│    ├─ App.js // App组件的代码文件
│    ├─ App.test.js // App组件的测试代码文件
│    ├─ index.css // 全局样式
│    ├─ index.js // 应用入口文件
│    ├─ logo.svg // React图标
│    ├─ serviceWorker.js // 默认帮助我们写好的注册PWA相关的代码
│    └─ setupTests.js // 测试初始化文件
└─ yarn.lock
```
**PWA：Progressive Web App**
可以添加至主屏幕,点击主屏幕图标实现启动动画以及隐藏地址栏;
实现离线缓存功能
实现消息推送等类似 Native App的功能

**Webpack**
静态模块打包器(module bundler)
webpack 处理应用程序时会递归构建一个依赖关系图(dependency graph)
这些模块会被打包成bundle；
React脚手架将webpack的配置隐藏起来（Vue CLI3开始也进行隐藏）
热更新只支持源代码，配置信息修改之后需要重新跑
**webpack配置**：yarn eject显示webpack配置，不可逆操作

