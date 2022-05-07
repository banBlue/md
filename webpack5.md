[TOC]

# webpack5配置步骤
## 安装webpack
```
npm install --save-dev webpack
npm install --save-dev webpack-cli
```

***

## 配置文件
1. 项目根目录下新建webpack.config.js,导出一个配置对象
```js
// 项目下新建main.js
import chajian from './chajian.js'
chajian()
// 项目下新建chajian.js
export default function chajian () {return 10}


// 配置:项目下新建webpack.config.js
const path = require("path")
module.exports = {
    entry: './main.js', // 入口文件
    output: { // 输出
        path: path.resolve(__dirname, 'dist'), // 输出目录
        filename: 'mybudel.js' // 输出入口主文件
    }
}
```
2. package.json下script新建命令启动
```json
"scripts": {
    "build": "webpack --config webpack.config.js",
},
```
3. 执行npm run build