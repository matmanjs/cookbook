# 测试

这里设置爬取的数据等于预设置的数据即可。这里有两种测试方案：有数据时和没有数据时

## 无数据校验

测试无数据的测试脚本如下：

```js
it('数据快照校验通过', function () {
            expect(data).to.eql({
                'transactionListInfo': {
                    'emptyPic': 'http://now.qq.com/img/nopkdata@2x_c3c9fbba.png',
                    'emptyWording': '暂无流水记录',
                    'isExist': true,
                    'list': [],
                    'total': 0
                }
            });
        });
```

## 有数据校验

测试有数据的测试脚本如下：

```js
it('数据快照校验通过', function () {
            expect(data).to.eql({
                'transactionListInfo': {
                    'emptyPic': '',
                    'emptyWording': '',
                    'isExist': true,
                    'list': [{
                        'id': 'id_1_1539224581000_6',
                        'isExist': true,
                        'isExpire': false,
                        'money': '+0.09',
                        'name': '摇一摇新手红包',
                        'time': '2018.10.11'
                    }, {
                        'id': 'id_1_1539224580000_10001',
                        'isExist': true,
                        'isExpire': false,
                        'money': '+0.19',
                        'name': '摇一摇任务红包',
                        'time': '2018.10.11'
                    }, {
                        'id': 'id_1_1539224579000_10002',
                        'isExist': true,
                        'isExpire': false,
                        'money': '+0.29',
                        'name': '摇一摇任务红包',
                        'time': '2018.10.11'
                    }, {
                        'id': 'id_1_1539224578000_10003',
                        'isExist': true,
                        'isExpire': false,
                        'money': '+0.39',
                        'name': '摇一摇任务红包',
                        'time': '2018.10.11'
                    }, {
                        'id': 'id_1_1539224577000_10004',
                        'isExist': true,
                        'isExpire': false,
                        'money': '+0.49',
                        'name': '摇一摇任务红包',
                        'time': '2018.10.11'
                    }, {
                        'id': 'id_1_1539224576000_10005',
                        'isExist': true,
                        'isExpire': false,
                        'money': '+0.59',
                        'name': '摇一摇任务红包',
                        'time': '2018.10.11'
                    }, {
                        'id': 'id_1_1539224575000_10079',
                        'isExist': true,
                        'isExpire': false,
                        'money': '+0.69',
                        'name': 'QQ春节红包',
                        'time': '2018.10.11'
                    }, {
                        'id': 'id_2_1539138181000_6',
                        'isExist': true,
                        'isExpire': false,
                        'money': '-1.09',
                        'name': '提现',
                        'time': '2018.10.10'
                    }, {
                        'id': 'id_2_1539138180000_10001',
                        'isExist': true,
                        'isExpire': false,
                        'money': '-1.19',
                        'name': '提现',
                        'time': '2018.10.10'
                    }, {
                        'id': 'id_2_1539138179000_10002',
                        'isExist': true,
                        'isExpire': false,
                        'money': '-1.29',
                        'name': '提现',
                        'time': '2018.10.10'
                    }, {
                        'id': 'id_2_1539138178000_10003',
                        'isExist': true,
                        'isExpire': false,
                        'money': '-1.39',
                        'name': '提现',
                        'time': '2018.10.10'
                    }, {
                        'id': 'id_2_1539138177000_10004',
                        'isExist': true,
                        'isExpire': false,
                        'money': '-1.49',
                        'name': '提现',
                        'time': '2018.10.10'
                    }, {
                        'id': 'id_2_1539138176000_10005',
                        'isExist': true,
                        'isExpire': false,
                        'money': '-1.59',
                        'name': '提现',
                        'time': '2018.10.10'
                    }, {
                        'id': 'id_2_1539138175000_10079',
                        'isExist': true,
                        'isExpire': false,
                        'money': '-1.69',
                        'name': '提现',
                        'time': '2018.10.10'
                    }, {
                        'id': 'id_3_1539051781000_6',
                        'isExist': true,
                        'isExpire': false,
                        'money': '-2.09',
                        'name': '兑换商品',
                        'time': '2018.10.09'
                    }, {
                        'id': 'id_3_1539051780000_10001',
                        'isExist': true,
                        'isExpire': false,
                        'money': '-2.19',
                        'name': '兑换商品',
                        'time': '2018.10.09'
                    }, {
                        'id': 'id_3_1539051779000_10002',
                        'isExist': true,
                        'isExpire': false,
                        'money': '-2.29',
                        'name': '兑换商品',
                        'time': '2018.10.09'
                    }, {
                        'id': 'id_3_1539051778000_10003',
                        'isExist': true,
                        'isExpire': false,
                        'money': '-2.39',
                        'name': '兑换商品',
                        'time': '2018.10.09'
                    }, {
                        'id': 'id_3_1539051777000_10004',
                        'isExist': true,
                        'isExpire': false,
                        'money': '-2.49',
                        'name': '兑换商品',
                        'time': '2018.10.09'
                    }, {
                        'id': 'id_3_1539051776000_10005',
                        'isExist': true,
                        'isExpire': false,
                        'money': '-2.59',
                        'name': '兑换商品',
                        'time': '2018.10.09'
                    }, {
                        'id': 'id_3_1539051775000_10079',
                        'isExist': true,
                        'isExpire': false,
                        'money': '-2.69',
                        'name': '兑换商品',
                        'time': '2018.10.09'
                    }, {
                        'id': 'id_4_1538965381000_6',
                        'isExist': true,
                        'isExpire': true,
                        'money': '+3.09',
                        'name': '摇一摇新手红包',
                        'time': '2018.10.08'
                    }, {
                        'id': 'id_4_1538965380000_10001',
                        'isExist': true,
                        'isExpire': true,
                        'money': '+3.19',
                        'name': '摇一摇任务红包',
                        'time': '2018.10.08'
                    }, {
                        'id': 'id_4_1538965379000_10002',
                        'isExist': true,
                        'isExpire': true,
                        'money': '+3.29',
                        'name': '摇一摇任务红包',
                        'time': '2018.10.08'
                    }, {
                        'id': 'id_4_1538965378000_10003',
                        'isExist': true,
                        'isExpire': true,
                        'money': '+3.39',
                        'name': '摇一摇任务红包',
                        'time': '2018.10.08'
                    }, {
                        'id': 'id_4_1538965377000_10004',
                        'isExist': true,
                        'isExpire': true,
                        'money': '+3.49',
                        'name': '摇一摇任务红包',
                        'time': '2018.10.08'
                    }, {
                        'id': 'id_4_1538965376000_10005',
                        'isExist': true,
                        'isExpire': true,
                        'money': '+3.59',
                        'name': '摇一摇任务红包',
                        'time': '2018.10.08'
                    }, {
                        'id': 'id_4_1538965375000_10079',
                        'isExist': true,
                        'isExpire': true,
                        'money': '+3.69',
                        'name': 'QQ春节红包',
                        'time': '2018.10.08'
                    }],
                    'total': 28
                }
            });
        });
```
