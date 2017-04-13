# 用户属性

# 1.需求

在开发的过程中，有一些用户变量需要能够存储到服务器端，例如用户对界面表格宽度的修改，用户对字段显示隐藏属性的修改，这些变量需要系统能够"记忆住"，即使更换了浏览器，更换了电脑，也要能够记忆这些变量。

# 2.设计原理

用户变量存储浏览器的LocalStorage中，浏览器定时将用户变量存储至服务器。具体流程如下图所示。

![](/assets/UserStorage1.png)

# 3.开发

1.首先引用JS

> var UserStorage = require\("../../common/UserStorage.js"\);

2.调用set方法

> var key = "\#Field\_1";
>
> UserStorage.setItem\(key,field.isVisible\);

### _注意_

1.需要保存到数据库的数据，其键必须以"\#"开头，否则不会存储到数据。

2.正常情况下数据不会立刻存储到数据。数据每隔10秒上传一次，只上传发生改变的数据。

3.如果需要手动上传存储数据，则先调用

> UserStorage.setItem\(key,field.isVisible\);

然后再调用

> UserStorage.uploadStorageImmediate\(\);



