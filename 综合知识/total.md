###1.vconsole 的配置

###2.core.js
在安卓 4.3 手机兼容的问题时遇到了 webview 无法显示的问题,于是想到是兼容性的问题，在 core.js 中有方法能够进行兼容。

[core.js](https://github.com/zloirock/core-js#readme)

###3.babel-polyfill
babel 是一个广泛使用的转码器，可以 ES6 的语法转化成 ES5 的语法。但是 babel 只能转换新的语法，不能转化新的 Api 以及一些全局对象例如 map、set、assign 等等。

举例来说，ES6 在 Array 对象上新增了 Array.from 方法。Babel 就不会转码这个方法。如果想让这个方法运行，必须使用 babel-polyfill，为当前环境提供一个垫片。

安装命令----cnpm install --save babel-polyfill

因为这是一个 polyfill （它需要在你的源代码之前运行），我们需要让它成为一个  dependency,

而不是一个  devDependency.
然后，在脚本头部，加入如下一行代码。

import 'babel-polyfill';

// 或者

require('babel-polyfill');

Babel 默认不转码的 API 非常多，详细清单可以查看 babel-plugin-transform-runtime 模块的[definitions.js](https://github.com/babel/babel/blob/master/packages/babel-plugin-transform-runtime/src/definitions.js)文件。

由于 babel-polyfill 的包非常大，所以就需要使用 core-js 和 raf 等方法

import 'core-js/modules/es6.object.assign'
import 'core-js/es6/promise'
import 'core-js/es6/map'
import 'core-js/es6/set'
import 'raf/polyfill'
