# 异步测试

Mocha 支持异步测试。

> 请打开 [06.async]，并进入该目录中。

## 1. done() 方法

如果是异步测试，需要额外调用 `done()` 方法，例如 `timeout.test.js` 文件中：

```javascript
it('测试应该5000毫秒后结束', function(done) {
  var x = true;
  var f = function() {
    x = false;
    expect(x).to.be.not.ok;
    done(); // 通知Mocha测试结束
  };
  setTimeout(f, 4000);
});
```

当回调参数中传入了 `done` 之后，Mocha 就会认为这是异步方法，必须显式调用 `done()`，以便通知 Mocha “测试已结束”。可以 [查看此处](https://mochajs.org/#asynchronous-code) 获得更多信息。

## 2. 测试用例执行超时

上面提到异步方法测试时，Mocha 会等到被调用了 `done()` 方法之后才认为测试已结束，但显然这个“等待”不会是无限长的。Mocha 默认每个测试用例最多执行 [2000 毫秒](https://mochajs.org/#t---timeout-ms)，如果到时没有得到结果，就报错。

对于涉及异步操作的测试用例，这个时间往往是不够的，需要用 `-t` 或 `--timeout` 参数指定超时门槛。如果单位为秒，则需要使用 `s`，例如 `--timeout 2s` or `--timeout 2000`。

当我们执行如下命令时，被提示 `Timeout`，原因是 `timeout.test.js` 中的用例需要在 `4000 ms` 之后才运行结果，已经超过了  `2000 ms` 。

```bash
mocha test/timeout.test.js
```

![](/assets/async-timeout.jpg)


使用 `-t` 或 `--timeout` 参数，改变默认的超时设置。

```bash
mocha test/timeout.test.js --timeout 5000
```

![](/assets/async-timeout-solution.jpg)

## 3. 高亮显示超时的测试用例时间

Mocha 默认会高亮显示超过 `75` 毫秒的测试用例（比如上面的执行时间就变为了红色），可以用 `-s` 或 `--slow` 调整这个参数。

```bash
mocha test/timeout.test.js --timeout 5000 -s 5000
```

上面的命令指定高亮显示耗时超过 `5000` 毫秒的测试用例。

![](/assets/async-timeout-s.jpg)

## 4. CGI 请求的例子

在 `async.test.js` 这个例子中，我们演示了 CGI 请求的例子，这是非常典型的异步场景测试。

``` javascript
it('异步请求应该返回一个对象', function(done) {
    request
        .get('https://api.github.com')
        .end(function(err, res) {
            expect(res).to.be.an('object');
            done();
        });
});
```

执行命令：

```bash
mocha test/async.test.js --timeout 10000
```

![](/assets/async-cgi.jpg)

## 5. Mocha 内置对 Promise 的支持

Mocha 内置 [对 Promise 的支持](https://mochajs.org/#working-with-promises)，允许直接返回 Promise，等到它的状态改变，再执行断言，而不用显式调用 `done` 方法。

我们对上例的CGI请求做一些修改，请看`promise.test.js`。

``` javascript
it('异步请求应该返回一个对象', function() {
    return fetch('https://api.github.com')
        .then(function(res) {
            return res.json();
        }).then(function(json) {
            expect(json).to.be.an('object');
        });
});
```

执行命令：

```bash
mocha test/promise.test.js --timeout 10000
```

![](/assets/async-promise.jpg)

[06.async]: https://github.com/helinjiang/pro-mocha/tree/master/06.async