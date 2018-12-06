# 安装和升级

在使用 MockStar 来构建 mock server 之前，需要先安装 Node 和 [mockstar-cli](https://www.npmjs.com/package/mockstar-cli) 。

## 1. 安装 Node 

MockStar 是基于 Node 来实现的，因此需要在本机安装 [Node](https://nodejs.org/) 。

为了获得更好的性能，推荐安装最新版本的 Node，进入 https://nodejs.org/ 官网，选择 LTS 版本的 Node 安装即可。

安装完Node后，执行下面命令，查看当前Node版本：

```
$ node -v
v4.4.0
```

如果能正常输出Node的版本号，表示Node已安装成功(Windows系统可能需要重新打开cmd)。

## 2. 安装 mockstar-cli

[mockstar-cli](https://www.npmjs.com/package/mockstar-cli) 提供了一些命令行，用于初始化项目和启动 mock server 服务等。

> 该组件并非一定要安装，使用时可以参考 [非 CLI 方式](use-mockstar-without-cli.md) 一文。

Node 安装成功后，执行如下 npm 命令安装 mockstar-cli （Mac或Linux的非root用户需要在命令行前面加 `sudo`，如：`sudo npm install -g mockstar-cli`）。

```
$ npm install -g mockstar-cli
```

npm 默认镜像是在国外，有时候安装速度很慢或者出现安装不了的情况，如果无法安装或者安装很慢，可以使用淘宝的镜像安装：

```
$ npm install -g cnpm --registry=https://registry.npm.taobao.org
$ cnpm install -g mockstar-cli
```

或者直接指定镜像安装：

```
$ npm install -g mockstar-cli --registry=https://registry.npm.taobao.org
```

mockstar-cli 安装完成后，执行命令 `mockstar --help`，查看帮助信息:

```
$ mockstar --help

  Usage: mockstar [options] [command]

  Commands:
      start    Start local server.
      init     Initialize project.

  Options:
      -v, --version          Print mockstar version.
      -h, --help             Print help information.
      -w, --watch            Enter watch mode, which rebuilds or restart server on file change.
      --dev                  Debug for development.

  Report bugs to https://github.com/mockstarjs/mockstar/issues.
```

如果能正常输出 MockStar 的帮助信息，表示已安装成功。

## 3. 升级 mockstar-cli

> 为了能使用 MockStar 的所有功能，请记得将其升级到最新版本。

升级命令与安装命令类似，请参考上一节内容。