# 快速上手

按照 [安装和升级](install.md) 一文配置好环境之后，开始我们的使用 Matman 之旅。本文我们将以百度（ https://www.baidu.com ）为测试对象，使用 matman 做一个简单的端对端测试。

> 如果你不想跟着步骤来做，则可以直接访问 https://github.com/matmanjs/matman-demo-getting-started 来获取最终的代码。

## 1. 初始化测试项目

新建一个目录，例如 `matman-demo-getting-started` ，使用 `npm init` 命令初始化，然后安装 [matman](http://npmjs.com/package/matman):

```
$ npm i matman --save
```

你也可以手动新建一个 `package.json` ，拷贝下面的内容：

```json
{
    "name": "matman-demo-getting-started",
    "version": "1.0.0",
    "scripts": {
        "build": "matman build",
        "build-dev": "matman build --dev"
    },
    "dependencies": {
        "matman": "^4.0.7"
    }
}
```

## 2. 配置 matman.config.js

增加一个 `matman.config.js` 文件，内容如下：

```js
const path = require('path');

module.exports = {
    rootPath: __dirname,
    testerPath: path.join(__dirname, './src')
};
```

其中 `testerPath` 指定了我们的测试用例存放在那个目录下，这里我们指定为 `src` ，因此需要手动增加 `src` 文件夹。

## 3. 编写端对端测试模块

### 3.1 编写爬虫脚本

新增 `src/demo_baidu/crawlers/get-page-info.js` 文件，内容如下：

```
module.exports = () => {
    return {
        title: document.title,
        searchBtnTxt: document.querySelector('#index-bn').textContent,
        width: window.innerWidth,
        height: window.innerHeight,
        userAgent: navigator.userAgent,
        _version: Date.now(),
        newsInfo: getNewsInfo()
    };
};

/**
 * 获取新闻模块的信息
 */
function getNewsInfo() {
    const jqContainer = $('.tab-news-content .news-list-wrapper');
    let result = {
        isExist: !!jqContainer.length
    };

    const list = [];

    if (result.isExist) {
        jqContainer.children().each(function () {
            const $this = $(this);
            list.push({
                title: $('.rn-container .rn-h1', $this).text().trim()
            });
        });
    }

    result.list = list;

    return result;
}
```


## 1. 初始化测试项目

运行如下命令初始化一个测试项目：

```bash
$ matman init project
```

提示输入测试项目的名字，默认测试项目文件夹名字为 `matman-app`。初始化之后，会生成一个示例项目，结构如下：

![matman项目结构](../images/matmanproject.png)

- `matman.config.js`：配置文件
- `src` ：测试代码源代码
  - `lib`： 公共方法和配置
  - `testers`：测试代码
    - `demo_tester`：一个典型的测试对象，我们建议按照"测试页面"为维度划分
      - `cases/xx/index.js` 中编写端对端测试执行函数
      - `cases/xx/index.test.js` 中编写测试用例
      - `crawlers/get-page-info.js` 中编写爬虫脚本
      - `env/index.js` 中存放环境相关参数如爬取页面链接等

## 2. 安装 npm 依赖

初始化完成之后，进入到我们的测试项目中，手动安装 npm 包依赖。假设我们的项目名称为 `matman-app`，则：

```bash
$ cd matman-app
$ npm install
```

## 3. 试运行

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