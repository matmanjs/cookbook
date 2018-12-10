# 快速上手

按照 [安装和升级](install.md) 一文配置好环境之后，开始我们的使用 Matman 之旅。

## 1. 初始化语法

`matman init` 语法：

```
$ matman init

  Usage: mockstar init <command> [options]
  Commands:
      project    Initialize project.
      tester     Initialize tester.
  Options:
      --dev                  Debug for development.
  Report bugs to https://github.com/mockstarjs/mockstar/issues.
```

## 2. 初始化项目

运行如下命令初始化一个项目：

```bash
$ matman init project
```

按照提示操作即可。

## 3. 安装依赖

初始化完成之后，进入到我们的项目中，手动安装 npm 包依赖。假设我们的项目名称为 `matman-app`，则：

```bash
$ cd matman-app
$ npm isntall
```

## 4. 项目结构
![`matman` 项目结构](./images/matmanproject.png)
- `src` 文件夹

    `lib` 文件夹中存放一些爬虫或测试用到的公共方法及数据；

    `testers` 存放后面生成的测试对象

    `page_index` 一个典型的测试对象，`cases/xx/index.js` 中编写 electron 执行时用到的参数，`cases/xx/index.test.js` 中编写测试用例，`crawlers/get-page-info.js` 中编写爬虫脚本，`env/index.js` 中存放环境相关参数如爬取页面链接等。

- `matman.config.js` 配置文件

    配置对应 mocker 桩对象存放的地址

## 5. 启动项目

执行如下命令即完成项目的启动了：

```bash
$ npm build #修改过爬虫文件后，如果只是修改测试用例则无需执行该步骤

# 之后
$ npm run test
```

## 6. 新增 tester 测试对象

在 `testers` 目录下，执行如下命令来快速新建一个 tester: 

```bash
$ matman init tester
```

> 我们推荐为 tester 设置一个容易识别的名字，一般建议与页面相关，例如取页面的名字为 tester 名字，这样容易查找。

新建完成之后，我们唯一必须要修改的是目录下的 `env/index.js` 文件，设置其中的 `getPageUrl` 函数中页面链接参数的值，该值用于匹配测试用的页面，还有 `WAIT` 值，该值用于控制爬虫开始执行的时间点。