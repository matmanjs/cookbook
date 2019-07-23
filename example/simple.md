# 示例一

如果读者已经将示例项目下载下来，并使用`npm start`在本地运行起整个项目了的话，可以在http://localhost:3000/simple下 查看示例项目的界面，如下图

![主界面](../images/example/mainframe.png)

示例一的测试代码在DevOpts/matman-app/src/testers/page-simple下

## 参数设置

DevOpts/matman-app/src/testers/page-simple下的cases文件夹存储的是测试文件夹，一个测试文件夹中通常包含两个文件：index.js和index.test.js。

其中：

- index.js中包含对测试过程的设置，比如测试页面的大小，测试时数据的mock，测试过程中的模拟操作等。
- index.test.js中包含对各个阶段测试数据的比较和测试。

对测试思想还希望有深入了解的可以参考[数据快照](../main-concepts/data-snapshot.md)

可以看到page-simple下的cases文件夹有两个测试文件夹，我们先关注jQuery-check中的测试代码。

查看index.js，可以看到如下代码

```js
const env = require('../../env');

function getResult(opts) {
    // 1. 获取 caseParser对象
    const caseParser = env.getCaseParser(__dirname);

    // 2. 获取页面的 url
    const pageUrl = env.getPageUrl(true);

    // 3. 获取 crawlerScript 爬虫脚本路径
    const crawlerScriptPath = caseParser.getCrawlerScriptPath('../../crawlers/get-page-info');

    // 4. 获得一些配置参数
    const reqOpts = Object.assign({
        proxyServer: env.getProxyServer(false),
        wait: env.OPTS.WAIT,
        screenshot: true
    }, opts);

    // console.log(reqOpts);

    // TODO 应该在 useRecorder 为 true 时支持延时关闭，否则可能会造成来不及收集到数据上报信息
    // 5. 执行并返回 Promise 结果
    return caseParser.handleScan(pageUrl, crawlerScriptPath, reqOpts);
}

module.exports = getResult;
```

- caseParse是用来指定测试代码所在位置的方法，默认指定的是当前文件夹。

- pageUrl即为要测试的页面的地址，可以进入对应的env文件夹下的index.js中修改为本用例对应的页面地址，即`http://localhost:3000/simple`

- crawlerScriptPath对应的是爬虫脚本，即通常名为get-page-info的文件，在getCrawlerScriptPath()中传对应文件的相对路径来引用

- reqOpts中存储一些运行时的信息，包括是否在测试过程中代理服务器，等待时间，是否截屏等等。其中
    - proxyServer用来判断是否要使用代理，在env.getProxyServer()方法中传true时，matman运行时会使用8080端口作为自己的代理端口；设置为false时，matman运行时直接走现网不使用任何代理。如果想使用其余的端口可以在DevOpts/matman-app/src/lib/utils.js下的getProxyServer方法中再行设置；
    - wait用来判定何时认为页面已经加载完。OPTS.WAIT对应的值有两种形式。可以直接接数字代表加载时间（单位为秒）；也可以接上代码中所示的选择器，监听到该选择器对应的元素存在即代表页面加载完成，可以在对应的文件下进行修改。
    - screenshot用来设置是否要在用例执行过程中进行截图，设置为true则用例运行的每一步都会有对应的截图；设置为false则不会有截图。

reqOpts的参数和对应的意义可以参考[matman文档](https://www.npmjs.com/package/matman#213-handleoperatepageurl-crawlerscriptpath-opts---callaction)

最后将这些信息作为参数传递给用例，执行并返回结果

## 爬虫脚本

matman测试的思路可以这么简化理解：按照用例运行操作，记录每一步的操作时界面上的信息，和正确的信息进行比对。

为了获取界面上的信息，就需要书写爬虫脚本。

