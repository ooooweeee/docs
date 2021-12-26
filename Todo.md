# 基座功能

- [ ] 日志

- [ ] 自动更新

- [ ] 任务托盘
- [ ] 设置

### 技术点

- 任务托盘

- 项目初始化

  1. 安装 `vue` 脚手架

     ```shell
     npm install -g @vue/cli
     ```

  2. 创建一个简单的项目

     ```shell
     vue create git-book
     ```

  3. 添加`electron`环境

     ```shell
     vue add electron-builder
     ```

- 环境配置

  > vue.config.js

  1、如何修改入口文件

  主进程默认入口文件为 `src/background.js` ，请勿修改 `package.json` 中的 `main` 属性

  2、监听某个目录下或某个文件发生变化时重启应用

  默认只有入口文件发生变化时才会重启应用

  3、`preload` 如何生效

  仅在代码中添加 `preload` 是不生效的

  4、关于相关依赖安装失败

  项目目录下创建 `.npmrc` 文件，键入如下配置

  ```shell
  # node-sass 安装失败
  SASS_BINARY_SITE=https://npm.taobao.org/mirrors/node-sass/
  # electron 相关依赖安装失败
  ELECTRON_MIRROR=https://npm.taobao.org/mirrors/electron/
  ELECTRON_BUILDER_BINARIES=https://npm.taobao.org/mirrors/electron-builder-binaries/
  ```

  > preoload.js
  
  将方法挂载到 windows 上
  
- 通用方法

  1. 指令
  2. 请求
  3. 监听
  
- 开发规则

  1. 本地存储

     AppData/Local			用户本地数据

     AppData/LocalLow	用户本地数据（未获取管理员权限的应用）

     APpData/Roaming	用户漫游数据

- 所用依赖

  1. electron-log 日志
  2. request 请求
