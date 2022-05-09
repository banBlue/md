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
    mode: 'production', // 标志是生产环境,还是开发环境'mode' option to 'development' or 'production'
    entry: './main.js', // 入口文件
    output: { // 输出
        path: path.resolve(__dirname, 'dist'), // 输出目录
        filename: 'mybudel.js' // 输出入口主文件
    },
    module: { // 1.配置loader-处理顺序从右到左   2.'less-loader'如果直接使用这种方式的话,webpack会自动在node_modules中寻找
        rules: [
            {
                test: /\.css$/, // 匹配的文件
                use: 'css-loader' // 需要使用的loader
            },
            {
                test: /\.less/ //处理less文件
                use: ['style-loader','css-loader','less-loader']
            },
            {
                test: /\.js$/, // 匹配的文件
                use: path.resolve(__dirname, 'mloader/loader1.js'),
            },
            {
                test: /\.js$/, // 匹配的文件
                use: path.resolve(__dirname, 'mloader/loader2.js'),
            }
        ]
    },
    plugins: [ // 配置plugins
        new ConsoleLogOnBuildWebpackPlugin({ test: '自定义对象' })
    ]
}
```
2. package.json下script新建命令启动
```json
"scripts": {
    "build": "webpack --config webpack.config.js",
},
```
3. 执行npm run build

# 编写一个自己的loader文件
```js
// 创建一个mloader/loader1.js
// 导出一个处理函数
// option选项可通过this.option来进行获取
module.exports = function loader(source) {
    let s = source.replace('1', '2')
    return s;
};
```

# 编写一个自己的plugin插件文件
```js
// 创建一个mPlugins/ConsoleLogOnBuildWebpackPlugin.js
// 导出一个处理函数,一定要有apply属性
const pluginName = 'ConsoleLogOnBuildWebpackPlugin'

module.exports = class ConsoleLogOnBuildWebpackPlugin {
    apply(compiler) {
        compiler.hooks.run.tap(pluginName, compilation => {
            console.log("webpack 构建过程开始！")
        })
    }
}
```