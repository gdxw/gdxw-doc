# bable编译说明

## 什么是bable 

简单的讲就是一个编译工具，可以把我们写的代码转换成指定代码,在现在的前端开发中，我们经常使用babel来编译我们的代码，如前端项目中的``.babelrc``文件。

例如：es6 转换 es5 ，下面是一个react的配置

```
// bable配置文件
{
    "presets": ["env", "es2015", "react", "stage-3"],       // 预设
    "plugins": [
        ["import",{
            "libraryName": "antd",
            "libraryDirectory": "es",   // default: lib
            "style": "css"
        }]
    ],
    "comments": false       // 是否在编译文件中生成注释  默认：true
}
```

## presets

预设 具体请参考 [babel-presets](https://babeljs.io/docs/plugins/#presets)

先解释一下presets是中的配置：

**es2015**：是我们要编译ES6(es2015)的代码，需要预先加载的编译相关模块, 会将es6的语法转换成es5的语法ba。
```
npm install --save-dev babel-preset-es2015
```

**react**：是我们要编译react中的jsx语法。
```
npm install --save-dev babel-preset-react
```
默认含有以下插件：
[
    preset-flow
    syntax-jsx
    transform-react-jsx
    transform-react-display-name
]

**env**：bable官方提供 , 是根据我们的环境需求来进行相关代码的编译，例如需要兼容ie8浏览器，会自动加载相关的编译模块。


**stage-3**： ES7不同阶段语法提案的转码规则（共有4个阶段：stage-0 > stage-1 > stage-2 > stage-3 ）
```
npm install --save-dev babel-preset-stage-0
```

stage-0 的范围最广

stage-0 包含  stage-1  依次类推


## plugins

babel的插件，presets是预先安装好的一些插件

**plugins的路径可以通过npm的形式是相对或绝对路径**
```
"plugins": ["babel-plugin-myPlugin"]
"plugins": ["./node_modules/asdf/plugin"]
```

如果你使用 babel-plugin- 作为 plugin 的前缀，你可以使用简写的形式省略掉该前缀,preset 与之相同;

```
"plugins": ["babel-plugin-myPlugin"]
"plugins": ["myPlugin"]

"presets": ["babel-preset-myPreset"]
"presets": ["myPreset"]
```

**plugins 和 Preset 的执行顺序**

这意味着如果两次转译都访问相同的”程序”节点，则转译将按照 plugin 或 preset 的规则进行排序然后执行。

* Plugin 会运行在 Preset 之前。
* Plugin 会从第一个开始顺序执行。ordering is first to last.
* Preset 的顺序则刚好相反(从最后一个逆序执行)。

项目中这段代码的意思是：
```
"plugins": [
        ["import",{
            "libraryName": "antd",
            "libraryDirectory": "es",   // default: lib
            "style": "css"
        }]
    ],
```

antd 是react的一个组件库，在开发中我们需要按需加载，例如：
```
import Button from 'antd/lib/button';
import 'antd/lib/button/style';
```

添加该配置后，我们可以直接这样写:

```
import {Button} from 'antd'
```
>注意：如果webpack配置添加了vendor库，babel-plugin-import是没有用的。

**babel-polyfill**

es5没有Promise，WeakMap，Array.from，Object.assign这些方法，需要添加polyfill来进行支持。

## 其他options

**comments**

是否在编译文件中生成注释  默认：true  


## 一般常用的配置

**react + antd 版本**
``` 
npm install --save-dev babel-core
npm install --save-dev babel-loader
npm install --save-dev babel-preset-es2015
npm install --save-dev babel-preset-react   
npm install --save-dev babel-preset-env   
npm install --save-dev babel-plugin-import
npm install --save babel-polyfill   // 支持es6的一些新语法
npm install --save-dev babel-preset-stage-2
```

``.babelrc``文件
```
{
    "presets": ["es2015", "react", "stage-2"],
    "plugins": [
        ["import",{
            "libraryName": "antd",
            "libraryDirectory": "es",  
            "style": "css"
        }]
    ],
    "comments": false
}
```

**vue + element**

```
npm install --save-dev babel-core
npm install --save-dev babel-loader
npm install --save-dev babel-preset-vue-app
npm install --save babel-polyfill
npm install --save-dev babel-preset-stage-2
```

``.babelrc``文件
```
{
    "presets": ["vue-app", "stage-2"],
    "comments": false
}
```
