# egg-validate

See [parameter](https://github.com/node-modules/parameter) for more information such as custom rule.

# 源码分析

## 文件结构

``` bash
├── app
|  └── extend
|     └── context.js - 封装ctx.validate方法，基于app.validator，进行校验和异常报错
├── app.js - 给app.validator挂上parameter模块暴露的校验器
├── config
|  └── config.default.js
```

## 外部模块依赖

主要是基于[parameter模块](https://github.com/node-modules/parameter) - 参数校验工具，被egg-validator使用，苏千开发。



## Install

```bash
$ npm i egg-validate --save
```

## Usage

```js
// config/plugin.js
exports.validate = {
  enable: true,
  package: 'egg-validate',
};
```

### Configurations

egg-validate support all parameter's configurations, check [parameter documents](https://github.com/node-modules/parameter) to get more infomations.

```js
// config/config.default.js
exports.validate = {
  // convert: false,
  // validateRoot: false,
};
```

### Validate Request Body

```js
// app/controller/home.js
exports.index = function* () {
  this.validate({ id: 'id' }); // will throw if invalid
  // or
  const errors = this.app.validator.validate({ id: 'id' }, this.request.body);
};
```

### Extend Rules

- app.js

```js
app.validator.addRule('jsonString', (rule, value) => {
  try {
    JSON.parse(value);
  } catch (err) {
    return 'must be json string';
  }
});
```

## Questions & Suggestions

Please open an issue [here](https://github.com/eggjs/egg/issues).

## License

[MIT](LICENSE)
