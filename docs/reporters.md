# 生成规格文件

Mocha支持从测试用例生成规格文件。

> 本文的示例代码在 [10.reporters]。更多阅读请看 https://mochajs.org/#reporters。

## 1. 生成 markdown 文件

从测试用例生成规格文件，格式为 markdown 格式，保存到 `spec.md` 文件中。

> 只有通过了测试的用例才会出现在 `md` 文件中，没有通过测试的用例会被忽略。

```bash
mocha --recursive -R markdown > spec.md
```

![](/assets/reporters-markdown.jpg)

## 2. 生成 html 文件

从测试用例生成规格文件，格式为 HTML 格式，保存到 `spec.html` 文件中。

> 无论是否通过了测试，该测试用例都会出现在 `html` 中。

```bash
mocha --recursive -R doc > spec.html
```

![](/assets/reporters-html.jpg)

[10.reporters]:https://github.com/helinjiang/pro-mocha/tree/master/10.reporters