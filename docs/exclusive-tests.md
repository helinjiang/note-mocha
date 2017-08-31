# 测试用例管理

大型项目有很多测试用例。有时，我们希望只运行其中的几个，这时可以用 `only` 方法（表示只运行某个测试套件或测试用例）或者 `skip` 方法（表示跳过某个测试套件或测试用例）。

`describe` 块和 `it` 块都允许调用 `only` 方法和 `skip` 方法。

> 本文的示例代码在 [08.exclusive-tests]。更多阅读请看 https://mochajs.org/#exclusive-tests 和 https://mochajs.org/#inclusive-tests。

## 1. it 块使用 only

在 `add-it-only.test.js` 中，我们为其中一个 `it` 块使用 `only`：

```javascript
it.only('1 加 1 应该等于 2', function() {
  expect(add(1, 1)).to.be.equal(2);
});

it('任何数加0应该等于自身', function() {
  expect(add(1, 0)).to.be.equal(1);
});

```

运行以下命令之后，只有带有`only`方法的测试用例会运行。

```bash
mocha test/add-it-only.test.js
```

![](index_files/68310f88-6f64-43f6-a1a5-70268812d69e.png)

## 2. describe 块使用 only

除了 `it` 块可以使用之后，`describe` 块也可以使用，见 `add-describe-only.js`。

```javascript
describe.only('加法函数的测试', function () {
    it('1 加 1 应该等于 2', function () {
        expect(add(1, 1)).to.be.equal(2);
  });

  it('任何数加0应该等于自身', function () {
        expect(add(1, 0)).to.be.equal(1);
  });
});

describe('加法函数的测试[no only]', function () {
    it('2 加 2 应该等于 4', function () {
        expect(add(2, 2)).to.be.equal(4);
  });
});
```

![](index_files/1add807f-2636-4535-8f24-53cae5f967d6.png)


## 3. skip 和 only

`only` 方法和 `skip` 方法含义刚好相反，但用法是一样的。

[08.exclusive-tests]:https://github.com/helinjiang/pro-mocha/tree/master/08.exclusive-tests