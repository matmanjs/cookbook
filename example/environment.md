# 环境准备

## whistle

使用教程请参见 [whistle](../third-party/whistle.md)

## switchOmega

参见 [switchOmega](../third-party/switchOmega.md)

## mockstar

### 安装

参见 [mockstar安装和升级](https://mockstarjs.gitbook.io/cookbook/install#2-an-zhuang-mockstarcli)

### 快速上手

参见 [mockstar快速上手](https://mockstarjs.gitbook.io/cookbook/getting-started)

### 使用

#### 浏览器中使用

示例二页面的 `http` 请求来自 `mockstar` 提供的桩数据。

因此，如果想要在浏览器中看到示例二的界面的话，需要设置whistle代理，使浏览器请求指向 `mockstar` 。

在 `mockstar` 的根目录下执行如下命令：

```bash
# 打开mockstar
npm start

# 开启whistle
w2 start
```

之后设置 `whistle` 代理，使请求转发到 `mockstar`

```tpl
cgi.now.qq.com/cgi-bin 127.0.0.1:9527
now.qq.com/maybe/report statusCode://200
now.qq.com 127.0.0.1:3000
```

全部完成后，访问 `now.qq.com/transaction` ，可以看见如下界面：

![明细页面](../images/example/transaction.png)

#### matman调用

`matman` 中要使用 `mockstar` 提供的桩数据的话，需要先创建对应的 `mockstar-cases` ，通过不同的 `case` 在每次测试时固定获取不同的 `mock` 数据。

##### mockstar-cases 创建

在 [mockstar-cases.js](https://github.com/matmanjs/matman-demo/blob/master/DevOpts/matman-app/src/testers/page-transaction/env/mockstar-cases.js) 是 `matman` 和 `mockstar` 之间进行交互的文件，它预定义了一个变量和一个函数。

- `DEFAULT_MOCK` : 预定义的变量，以json形式存储默认情况下的mock数据，key为mocker名，value为mock的名字。

- `getMockStarQuery` : 预定义的函数，用于将json形式表示的mock数据转成mock数据

有上述两个方式之后，就可以自定义方法来组装自己的 `mock-case` 了。如示例里提供的 `getBasicFlow` 和 `getEmptyFlow` 。最后将 `getMockStarQuery` 的结果作为返回值，就完成了一个 `mock` 方法。

##### index.js引用不同的mock

要使用上面创建的 `mock-case` ，需要对应的 `mock` 方法暴露给外部使用。 即包含在 `module.exports` 内。

使用 `mock-case` 本质是通过代理服务器转接到 `mockstar` 上，因此首先需要开启 `whistle` 和 `mockstar` 。

在 `index.js` 中，添加如下设置：

1. `proxyServer` : `env.getProxyServer(true)`

2. `mockstarQuery` : mock方法，例： `env.mockstarCases.getBasicFlow()`

这样就可以实现测试中使用 `mock` 数据

##### index.test.js动态修改mock