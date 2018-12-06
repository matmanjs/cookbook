# 快速上手

按照 [安装和升级](install.md) 一文配置好环境之后，开始我们的使用 MockStar 之旅。

## 1. 初始化语法

`mockstar init` 语法：

![`mockstar init` 语法](./images/mockstarinit.png)

## 2. 初始化项目

运行如下命令初始化一个项目：

```bash
$ mockstar init project
```

按照提示操作即可。

## 3. 安装依赖

初始化完成之后，进入到我们的项目中，手动安装 npm 包依赖。假设我们的项目名称为 `mockstar-app`，则：

```bash
$ cd mockstar-app
$ npm isntall
```

## 4. 项目结构
![`mockstar` 项目结构](./images/mockstarinit.png)
- `mock_server` 文件夹

    `lib` 文件夹中存放一些 mocker 桩对象用到的公共方法及数据；

    `mockers` 存放后面生成的 mocker 桩对象
- `mockstar.config.js` 配置文件

    配置对应 mocker 桩对象存放的地址

## 5. 启动项目

执行如下命令即完成项目的启动了：

```bash
$ npm start

# 或者
$ mockstar start --dev --watch
```

## 6. 打开管理端

默认情况下，mock server 会使用 `9527` 端口，因此打开浏览器，访问 `127.0.0.1:9527`。你可以激活不同的桩数据，体验自由切换桩数据的功能。

脚手架中提供了几个 mocker 样例，你可以进入到 `mock_modules` 目录下，找到其中一个桩数据，适当修改返回值，然后再在管理端"预览结果"。

> 当使用了 `--watch` 之后，我们会监听 `mockServerPath` 值对应的目录文件变化，自动重启服务。

## 7. 新增 mocker 桩对象

在 `mockstar-app` 目录下，执行如下命令来快速新建一个 mocker: 

```bash
$ mockstar init mocker
```

> 我们推荐为 mocker 设置一个容易识别的名字，一般建议与 CGI 相关，例如取 CGI 的名字为 mocker 名字，这样容易查找。

新建完成之后，我们唯一必须要修改的是目录下的 `config.js` 文件，设置其中的 `route` 值（请求的 path 值，不要加域名和 query 等）。该值用于匹配我们的 CGI，可参考 [Express router](http://expressjs.com/en/4x/api.html#router) 的说明。

## 8. 新增桩数据

在管理端刷新之后，会发现我们的 mocker 已经存在，接下来就需要根据自己的需要修改 `mock_modules` 下的桩数据即可！

一个桩数据模块只有一个要求，就是必须是符合 CommonJS 规范的。