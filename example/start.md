# 启动和运行

## 代理

首先需要设置whistle代理，whistle安装参见[whistle文档](../third-party/whistle.md)

安装之后，就可以开启whistle代理了。

进入目录 [DevOpts/whistle/](https://github.com/matmanjs/matman-demo/tree/master/DevOpts/whistle)

运行如下命令：

```bash
# 运行whistle脚本
./start-dev-8080.sh 

```

看到如下的输出，说明whistle运行成功

```bash
Ready to start whistle...
[i] whistle killed.
[i] whistle@1.15.10 started
[i] 1. use your device to visit the following URL list, gets the IP of the URL you can access:
       http://127.0.0.1:8080/
       http://10.64.66.73:8080/
       Note: If all the above URLs are unable to access, check the firewall settings
             For help see https://github.com/avwo/whistle
[i] 2. configure your device to use whistle as its HTTP and HTTPS proxy on IP:8080
[i] 3. use Chrome to visit http://local.whistlejs.com/ to get started
Setting whistle[127.0.0.1:8080] rules successful.
```

这样代理的准备工作就完成了

## 启动桩数据

进入目录 [DevOpts/mockstar-app/](https://github.com/matmanjs/matman-demo/tree/master/DevOpts/mockstar-app) ，运行如下命令：

```bash
# 安装依赖
npm i

# 运行服务器
npm start
```

看到如下的输出，说明mockstar运行成功

```bash
> mockstar-app@ start /Users/remozhang/remozhang/git/matman-demo/DevOpts/mockstar-app
> mockstar start --watch

Load config file: /Users/remozhang/remozhang/git/matman-demo/DevOpts/mockstar-app/mockstar.config.js
[i] MockStar@1.1.3 is running for /Users/remozhang/remozhang/git/matman-demo/DevOpts/mockstar-app
       http://127.0.0.1:9527
       http://10.64.66.73:9527
```

## 启动项目

控制台/终端切到主目录下，运行如下命令

```bash
# 安装依赖
npm i

# 运行项目
npm start

```

## 开始测试

控制台/终端切到matman-app目录下，运行如下命令：

```bash
# 安装依赖
npm i

# 编译爬虫脚本
npm run build

# 开始测试
npm test

```

然后测试就开始了。

