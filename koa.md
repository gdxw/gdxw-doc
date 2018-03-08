## egg框架学习

### koa vs express

* 异步编程模型 
    * express - es2015, promise, generator
    * koa - es2017, async   (node 8.0 +)
* middleware - 中间健
    * koa - 洋葱型
    * express - 堆栈
* context
    * express - request, response, next
    * koa - context, next

### 安装使用

指定node版本
```
npm i n -g
n -h
n
## 指定版本 （8.0以上）
```

安装egg
```
npm i egg-init -g
egg-init egg-example --type=simple
cd egg-example
npm i

```

EGG 概念

中间件、插件、应用、框架、loader关系

中间件：
    * 加载有先后顺序
    * 中间件的定位是拦截用户请求，并进行处理。
插件：
    * 迷你应用，可以包含中间件、service、配置、框架扩展
    * 没有独立的router、controller
框架：
    * 框架包含多个插件
    * 没有独立的router、controller
应用：
    * 应用依赖与框架
    * 包含中间件、service、配置、框架扩展、router、controller
loader：
    * 应用、框架和插件都称为加载单元（loadUnit）

加载顺序：插件 => 框架 => 应用依次加载



文件加载顺序 plugin > config > extend > 自定义初始化（app.js,agent.js） > service > middleware > controller > router  

加载中同名会覆盖


