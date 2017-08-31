# 关于 test 目录

如果你关注过一些开源项目，就可以看到项目中会有一个名为 `test` 目录，这除了约定俗成的缘故之外，还因为有些测试框架会对这个目录有额外的处理。

## 1. 默认运行 test 子目录中的测试脚本

Mocha 默认运行 `test` 子目录里的测试脚本( https://mochajs.org/#the-test-directory )。所以，一般都会把测试脚本放在 `test` 目录里面，然后执行 `mocha` 就不需要参数了。

> By default, `mocha` looks for the glob `./test/*.js` and `./test/*.coffee`, so you may want to put your tests in `test/` folder.


我们拷贝 [01.getting-started] 示例代码到 `02.mocha-test-directory`，并在此基础上，做一些变更：将 `add.js` 放置在 `src` 目录下，且将 `add.test.js` 放置在了 `test` 目录中。最后运行如下命令：

```bash
mocha

# 等同于
mocha test/add.test.js
```

然后我们就可以很清楚的看到 `test` 子目录中的测试脚本运行了。

![](/assets/mocha-test-directory-1.jpg)

## 2. 默认只执行 test 子目录下面第一层的测试用例

Mocha 默认只执行 `test` 子目录下面第一层的测试用例，不会执行更下层的用例。

我们在 `src` 下新增一个“乘法”模块 `multiply.js`，并在 `test/dir` 目录中新建测试脚本 `multiply.test.js`（详见 [02.mocha-test-directory]）。

最后运行 `mocha` 命令，发现它根本就没被执行。

## 3. 执行 test 子目录下所有的测试用例

需要增加 `--recursive` 参数，这时 `test` 子目录下面所有的测试用例(不管在哪一层)都会执行。

![](/assets/mocha-test-directory-recursive.jpg)

> `mocha` 命令的参数说明可以查看 https://mochajs.org/#usage 。

## 4. 执行 test 子目录下特定的测试用例

命令行可以指定使用通配符，同时指定多个文件，例如下面的命令就是执行 `test` 目录下的js文件：

```bash
mocha test/{,**/}*.js
```

![](/assets/mocha-test-directory-glob.jpg)

更多关于通配符的说明，请查看“通配符”一节。


[01.getting-started]: https://github.com/helinjiang/pro-mocha/tree/master/01.getting-started
[02.mocha-test-directory]: https://github.com/helinjiang/pro-mocha/tree/master/02.mocha-test-directory