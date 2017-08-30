我们先以一个简单的加法示例开始，完整的源代码在 [01.getting-started](https://github.com/helinjiang/pro-mocha/tree/master/01.getting-started) 中。

## 1. 新建项目

新建一个文件夹，在本例中，我们命名为 `01.getting-started`。

执行 `npm init` ，按提示输入，完成后会自动生成一个 package.josn 文件。

安装相应的 npm 包：

``` bash
npm install mocha chai --save-dev
```

## 2. 新建js模块

新建 `add.js` 文件，并且实现一个简单的加法功能：

```javascript
function add(x, y) {
    return x + y;
}

module.exports = add;
```

## 3. 新建测试文件

新建 `add.test.js` 文件：

```javascript
var add = require('./add.js');
var expect = require('chai').expect;

describe('加法函数的测试', function () {
    it('1 加 1 应该等于 2', function () {
        expect(add(1, 1)).to.be.equal(2);
  });
});
```

> 通常，测试脚本与所要测试的源码脚本同名，但是后缀名为`.test.js`（表示测试）或者`.spec.js`（表示规格）。


在上面的测试脚本中，有一句断言:

```javascript
expect(add(1, 1)).to.be.equal(2);
```

所谓"断言"，就是判断源码的实际执行结果与预期结果是否一致，如果不一致就抛出一个错误。上面这句断言的意思是，调用 `add(1, 1)`，结果应该等于 `2`。

所有的测试用例（`it` 块）都应该含有一句或多句的断言。它是编写测试用例的关键。断言功能由断言库来实现，Mocha 本身不带断言库，所以必须先引入断言库。

```javascript
var expect = require('chai').expect;
```

断言库有很多种，Mocha并不限制使用哪一种。上面代码引入的断言库是[`chai`](http://chaijs.com/)，并且指定使用它的[`expect`](http://chaijs.com/api/bdd/)断言风格。

> 关于断言库和 chai，后续还会有介绍。

## 4. 运行测试命令

进入到 `01.getting-started` 目录下，执行以下命令：

```bash
mocha add.test.js
```

运行结果如下，可以看到测试脚本同构了测试，一共只有 `1` 个测试用例，耗时是 `8` 毫秒。

![](/assets/gettting-started.jpg)

> `mocha` 命令后面紧跟测试脚本的路径和文件名，可以指定多个测试脚本。例如： `mocha file1 file2 file3`