<h1 align="center">babel-plugin-transform-define</h1>

<p align="center">
  <a title='Build Status' href="https://raw.githubusercontent.com/FormidableLabs/babel-plugin-transform-define/master/LICENSE">
    <img src='https://img.shields.io/badge/license-MIT-blue.svg?style=flat-square' />
  </a>
  <a href="https://badge.fury.io/js/babel-plugin-transform-define">
    <img src="https://badge.fury.io/js/babel-plugin-transform-define.svg" alt="npm version" height="18">
  </a>
  <a href='https://github.com/FormidableLabs/babel-plugin-transform-define/actions'>
    <img src='https://github.com/FormidableLabs/babel-plugin-transform-define/workflows/CI/badge.svg' />
  </a>
  <a href='https://github.com/FormidableLabs/babel-plugin-transform-define#maintenance-status'>
    <img alt="Maintenance Status" src='https://img.shields.io/badge/maintenance-stable-yellow.svg?color=yellow&style=flat' />
  </a>
</p>

<h4 align="center">
  Compile time code replacement for babel similar to Webpack's <a href='https://webpack.js.org/plugins/define-plugin/'>DefinePlugin</a>
</h4>

***

## Quick Start

```shell
$ npm install --save-dev babel-plugin-transform-define
```

**.babelrc**

```json
{
  "plugins": [
    ["transform-define", {
      "process.env.NODE_ENV": "production",
      "typeof window": "object"
    }]
  ]
}
```

**.babelrc.js**

```js
// E.g., any dynamic logic with JS, environment variables, etc.
const overrides = require("./another-path.js");

module.exports = {
  plugins: [
    ["transform-define", {
      "process.env.NODE_ENV": "production",
      "typeof window": "object",
      ...overrides
    }]
  ]
};
```

## Reference Documentation

`babel-plugin-transform-define` can transform certain types of code as a babel transformation.

##### `Identifiers`

*.babelrc*
```json
{
  "plugins": [
    ["transform-define", {
      "VERSION": "1.0.0",
    }]
  ]
}
```

*Source Code*
```js
VERSION;

window.__MY_COMPANY__ = {
  version: VERSION
};
```

*Output Code*
```js
"1.0.0";

window.__MY_COMPANY__ = {
  version: "1.0.0"
};
```
***
##### `Member Expressions`

*.babelrc*
```json
{
  "plugins": [
    ["transform-define", {
      "process.env.NODE_ENV": "production"
    }]
  ]
}
```

*Source Code*
```js
if (process.env.NODE_ENV === "production") {
  console.log(true);
}
```

*Output Code*
```js
if (true) {
  console.log(true);
}
```
***
##### `Unary Expressions`

*.babelrc*
```json
{
  "plugins": [
    ["transform-define", {
      "typeof window": "object"
    }]
  ]
}
```

*Source Code*
```js
typeof window;
typeof window === "object";
```

*Output Code*
```js
'object';
true;
```


***

## License

[MIT License](http://opensource.org/licenses/MIT)


## Maintenance Status

**Stable:** Formidable is not planning to develop any new features for this project. We are still responding to bug reports and security concerns. We are still welcoming PRs for this project, but PRs that include new features should be small and easy to integrate and should not include breaking changes.
