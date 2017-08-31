# 测试用例的钩子 HOOKS

本文的示例代码在 [07.hook]。

## 1. 四个钩子（hook）

Mocha在 `describe` 块之中，提供测试用例的四个钩子：`before()`、`after()`、`beforeEach()` 和 `afterEach()`。它们会在指定时机下执行。

```javascript
describe('hooks', function() {

  before(function() {
    // 在本区块的所有测试用例之前执行
  });

  after(function() {
    // 在本区块的所有测试用例之后执行
  });

  beforeEach(function() {
    // 在本区块的每个测试用例之前执行
  });

  afterEach(function() {
    // 在本区块的每个测试用例之后执行
  });

  // test cases
});
```

## 2. 示例一，beforeEach

在 `beforeEach.test.js` 测试用例中，我们使用 `beforeEach` 方法在每个测试用例执行之前进行重置 `foo` 变量。

```
describe('beforeEach示例', function () {
    var foo = false;

    beforeEach(function () {
        foo = true;
    });

    it('修改全局变量应该成功', function () {
        expect(foo).to.be.equal(true);
    });
});
```

执行命令：

```bash
mocha test/beforeEach.test.js
```

![](/assets/hooks-beforeeach.jpg)



## 3. 示例二，beforeEach 中进行异步操作

在 `beforeEach-async.test.js` 测试用例中， `beforeEach` 方法内使用了异步操作，依然需要调用 `done` 方法来通知。

```javascript
describe("beforeEach示例-异步操作", function() {
    var foo = false;

    beforeEach(function(done) {
        setTimeout(function() {
            foo = true;
            done();
        }, 50);
    });

    it("全局变量异步修改应该成功", function() {
        expect(foo).to.be.equal(true);
    });
});

```

执行命令：

```bash
mocha test/beforeEach-async.test.js
```

![](/assets/hooks-beforeeach-async.jpg)

[07.hook]: https://github.com/helinjiang/pro-mocha/tree/master/07.hook

