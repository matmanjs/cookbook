# 爬虫

## 父元素下多个子元素的爬取

检查界面元素，可以看到界面上每一行都是一个`div`，每个`div`的`class`的属性均为`list-item`。如下

```html
<div class="display-transaction-list">
    <div class="list-item " data-id="id_1_1539224581000_6">
        <div class="info">
            <div class="flow-info">摇一摇新手红包</div>
            <div class="flow-time">2018.10.11</div>
        </div>
        <div class="money">
            <span class="plus">+</span>0.09
        </div>
    </div>
    ...
</div>
```

所以爬取脚本的时候可以以 `class` 值为 `display-transaction-list` 的元素，遍历其下的各个子元素信息，如下

```js
/**
 * 列表项信息
 */
function getListTransactionItemInfo(parentSelector) {
    const result = {
        isExist: useJquery.isExist(parentSelector)
    };

    if (result.isExist) {
        result.name = useJquery.getText('.info .flow-info', parentSelector);
        result.time = useJquery.getText('.info .flow-time', parentSelector);
        result.money = useJquery.getText('.money', parentSelector);
        result.isExpire = useJquery.isExist('.dated-icon', parentSelector);
        result.id = $(parentSelector).attr('data-id');
    }

    return result;
}

/**
 * 列表信息
 */
function getTransactionListInfo() {
    const parentSelector = '#root .display-transaction';

    const result = {
        isExist: useJquery.isExist(parentSelector)
    };

    if (result.isExist) {
        // 总数
        result.total = useJquery.getTotal('.display-transaction-list .list-item', parentSelector);

        const list = [];

        $('.display-transaction-list .list-item', parentSelector).each(function () {
            list.push(getListTransactionItemInfo($(this)));
        });

        // 列表内容
        result.list = list;

        // 列表为空时的文字
        result.emptyWording = useJquery.getText('.display-transaction-empty p', parentSelector);
    }
    return result;
}

```

这样就完成了爬虫脚本的书写
