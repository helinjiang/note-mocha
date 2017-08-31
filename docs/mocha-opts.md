# 配置文件 mocha.opts

Mocha允许在 `test` 目录下面，放置配置文件 `mocha.opts`，把命令行参数写在里面。

## 1. 使用 mocha.opts 配置文件保存参数

请先进入 [04.mocha-opts] 目录，运行下面的命令。

```bash
mocha --recursive --reporter tap
```

上面这个命令有两个参数 `--recursive`、`--reporter tap`，每次执行命令时都要手动输入，非常不方便，且容易出错。在 `test` 目录下新增 `mocha.opts` 文件，并将这些参数写入其中：

```
--reporter tap
--recursive
```

然后，执行 `mocha` 就能取得与第一行命令一样的效果。

```
mocha
```

![](/assets/mocha-opts.jpg)

## 2. 使用 mocha.opts 配置文件改变测试文件目录

如果你的测试用例的代码不是在 `test` 目录，而是在其子目录中，例如在 `dir` 内，则需要指定 `test/dir`：

```
test/dir
--reporter tap
--recursive
```

如果你的测试用例的代码不是在 `test` 目录，而是在与之平级的目录结构中，例如在 `test-in-other-dir` 内，则需要在 `test/macha.opts` 中指定 `test-in-other-dir`：

```
test-in-other-dir
--reporter tap
--recursive
```

> 注意 `mocha.opts` 只在 `test` 目录下生效。你在 `test-in-other-dir` 定义了这个文件不会有任何效果。

[04.mocha-opts]: https://github.com/helinjiang/pro-mocha/tree/master/04.mocha-opts