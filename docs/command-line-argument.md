# Mocha 命令行参数

Mocha 支持较为丰富的命令行参数，其格式为：

``` bash
mocha [debug] [options] [files]
```

在本文，我们挑选了一部分进行简单介绍。详细的请看 https://mochajs.org/#usage 。

> 请在 [03.command-line-argument] 子目录里面，运行下面的命令，查看效果。

## 1. --help, -h

`--help` 或 `-h` 参数，用来查看Mocha的所有命令行参数。

> `-h, --help : output usage information.`

```bash
mocha --help
```

## 2. --reporter, -R

`--reporter` 或 `-R` 参数用来指定测试报告的格式，默认是 `spec` 格式。

> `-R, --reporter <name> : specify the reporter to use.`

```bash
mocha

# 等同于
mocha --reporter spec
```

### 2.1 内置的报告格式
Mocha 提供了包括 `spec` 格式在内的众多报告输出格式。你可以通过运行 `moacha --reporters` 来获得所有内置的报告格式，且可以在官方网站查看这些 [报告格式](http://mochajs.org/#reporters) 的效果。

![](/assets/command-line-argument-reporters.jpg)

### 2.2 第三方的报告格式

这里我们介绍其中一种： 使用 [mochawesome](http://adamgruber.github.io/mochawesome/) 模块，可以生成漂亮的HTML格式的报告。

![](/assets/command-line-argument-reporters2.jpg)

首先安装 mochawesome ：

```bash
npm install --save-dev mochawesome
```

然后执行命令：

```bash
mocha --reporter mochawesome
```
![](/assets/command-line-argument-reporters3.jpg)

执行完成之后，我们会发现在当前项目中新生成了一个文件夹 `mochawesome-reports`:

![](/assets/command-line-argument-reporters4.jpg)

打开其中的 html 文件就可以看到漂亮的结果了。

> 不同的版本和参数会导致实际展示的效果和下面的截图有差异。

![](/assets/command-line-argument-reporters5.jpg)

> 你可能有些疑问，为什么没输出“乘法”模块的测试结果呢？原因可以查看“关于test目录”一节。你也可以直接输入 `mocha --recursive --reporter mochawesome` 看看结果。

## 3. --watch, -w

`--watch` 或 `-w` 参数用来监视文件变化，如有变化则会自动运行 Mocha。

> `-w, --watch : watch files for changes.`

```bash
mocha --watch
```

上面命令执行以后，并不会退出。你可以另外打开一个终端窗口，修改 `test` 目录下面的测试脚本 `add.test.js`，比如删除一个测试用例，一旦保存，Mocha 就会再次自动运行。

## 4. --bail, -b

`--bail` 或 `-b` 参数指定只要有一个测试用例没有通过，就停止执行后面的测试用例。这对 [持续集成](http://www.ruanyifeng.com/blog/2015/09/continuous-integration.html) 很有用。

> `-b, --bail : bail after first test failure.`

```bash
mocha --bail
```

## 5. 只执行匹配的测试用例

有时候我们只需执行匹配的测试用例，可以考虑如下方式：

- `--grep` 或 `-g`： 参数用于“搜索匹配”测试用例的名称。`-g, --grep <pattern> : only run tests matching <pattern>`
- `--fgrep` 或 `-f`： 参数用于“搜索包含”测试用例的名称。`-f, --fgrep <string> : only run tests containing <string>`
- `--invert` 或 `-i`： 参数用于选择 `--grep` 和 `--fgrep` 结果相反的测试用例。`-i, --invert : inverts --grep and --fgrep matches`

> 此处的测试用例的名称即指 `it` 块的第一个参数。

首先我们的测试用例如下：

```javascript
describe('加法函数的测试', function () {
    it('1 加 1 应该等于 2', function () {
        expect(add(1, 1)).to.be.equal(2);
  });

  it('任何数加0应该等于自身', function () {
        expect(add(1, 0)).to.be.equal(1);
  });
});
```

分别执行下面的命令，可以查看结果。

```bash
mocha
mocha --grep " 1 加 1"
mocha --grep " 1 加 1" --invert
```

![](/assets/command-line-argument-grep.jpg)


[03.command-line-argument]: https://github.com/helinjiang/pro-mocha/tree/master/03.command-line-argument