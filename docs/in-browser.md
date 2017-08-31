# 在浏览器中执行测试用例

除了在命令行运行，Mocha还可以在浏览器运行。

> 本文的示例代码在 [09.in-browser]。更多阅读请看 https://mochajs.org/#running-mocha-in-the-browser。


## 1. mocha init 自动生成初始化文件

使用 `mocha init <path>` 命令在指定目录生成初始化文件。

> 注意该命令执行之后，会在当前目录中新建一个文件夹，初始化的文件就放在这个文件夹中。

```javascript
mocha init 09.in-browser
```

## 2. 新增源码文件

新建一个源码文件 `add.js`（也就是待测的文件），内容如下。

```javascript
function add(x, y) {
  return x + y;
}
```

然后在 `index.html` 中引入这个文件，以及断言库 `chai.js` 。

```html
<script src="mocha.js"></script>
<script>mocha.setup('bdd');</script>
<script src="add.js"></script>
<script src="http://chaijs.com/chai.js"></script>
<script src="tests.js"></script>
<script>
  mocha.run();
</script>
```

## 3. 编写测试脚本

在 `tests.js` 新增测试脚本，内容如下。

```javascript
var expect = chai.expect;

describe('加法函数的测试', function() {
    it('1 加 1 应该等于 2', function() {
        expect(add(1, 1)).to.be.equal(2);
    });

    it('任何数加0等于自身', function() {
        expect(add(1, 0)).to.be.equal(1);
        expect(add(0, 0)).to.be.equal(0);
    });
});
```

> 由于 `index.html` 中默认引入了该文件，所以不需要手动引入了，除非是自己新写了另外的文件。

## 4. 浏览器中执行测试

在浏览器里面打开 `index.html`，就可以看到测试脚本的运行结果。

![](/assets/in-browser.jpg)

[09.in-browser]:https://github.com/helinjiang/pro-mocha/tree/master/09.in-browser