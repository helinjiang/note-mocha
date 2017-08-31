# 使用 ES6

如果你习惯使用 ES6 来写代码，在 mocha 中也是支持的。

## 1. 使用 ES6 来写测试脚本

如果测试脚本是用ES6写的，那么运行测试之前，需要先用Babel转码。进入 [05.es6] 目录，打开 `test/add.test.js` 文件，可以看到这个测试用例是用ES6 写的。

```javascript
import add from '../src/add.js';
import chai from 'chai';

let expect = chai.expect;

describe('加法函数的测试', function () {
    it('1 加 1 应该等于 2', function () {
        expect(add(1, 1)).to.be.equal(2);
  });
});
```

## 2. 安装 Babel

ES6转码，需要安装Babel。

```bash
npm install babel-core babel-preset-es2015 --save-dev
```

然后，在项目目录下面，新建一个 `.babelrc` 配置文件。

```json
{
  "presets": [ "es2015" ]
}
```

## 3. 执行测试脚本

使用 `--compilers` 参数指定测试脚本的转码器。

```bash
../node_modules/mocha/bin/mocha --compilers js:babel-core/register
```

上面代码中，`--compilers` 参数后面紧跟一个用冒号分隔的字符串，冒号左边是文件的后缀名，右边是用来处理这一类文件的模块名。上面代码表示，运行测试之前，先用 `babel-core/register` 模块，处理一下 `.js` 文件。由于这里的转码器安装在项目内，所以要使用项目内安装的Mocha；如果转码器安装在全局，就可以使用全局的Mocha。


## 4. babel-polyfill

注意，Babel默认不会对Iterator、Generator、Promise、Map、Set等全局对象，以及一些全局对象的方法（比如 `Object.assign`）转码。如果你想要对这些对象转码，就要安装 [babel-polyfill](https://www.npmjs.com/package/babel-polyfill)。

```bash
npm install babel-polyfill --save
```

然后，在你的脚本头部加上一行。

```javascript
import 'babel-polyfill'
```

[05.es6]: https://github.com/helinjiang/pro-mocha/tree/master/05.es6