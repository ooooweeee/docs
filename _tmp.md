# 环境搭建
> vue.config.js
```javascript
module.exports = {
	configureWebpack: {
		devTool: 'source-map',
		entry: '',
		resolve: {
			alias: {}
		}
	},
	pluginOptions: {
		electronBuilder: {
			preload: '',
			mainProcessFile: '', // 主进程入口文件
			mainProcessWatch: [], // 那些文件属于主进程
			chainWebpackMainProcess: config => {
				config.resolve.alias.set() // 路径别名
			}
		}
	}
}
```

> preload.js
```javascript
const { contextBridge, ipcRenderer } = require('electron')

// 将 ipcRenderer 挂在到 window 对象上
// 使用方法：window.ipcRenderer
contextBridge.exposeInMainWorld('ipcRenderer', {})
```

### 开发规则
1. 基座提供统一方法
	1. *指令* 下发不需要返回
	2. *请求* 执行后需要有反馈
	3. *监听* 发起请求后需要持续获得反馈
2. 用户文件存放位置
	1. 用户本地数据 AppData/Local
	2. 用户漫游数据 AppData/Roaming

> createFrame.js
```javascript
const { BrowserView, BrowserWindow } = require('electron')

const frame = new BrowserView()
frame.webContents.once('navigation-entry-committed', () => {
	const father = frame.webContents.getOwnerBrowserWindow()
	father.getSize()
	frame.setBounds()
	frame.setAutoResize({ width: true, height: true })
})

const win = new BrowserWindow({
	webPreferences: {
		nodeIntegration: false,
		contextIsolation: true,
		preload: ''
	}
})
win.on('maximize', () => {})
win.on('unmaximize', () => {})
```
