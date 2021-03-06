# Simple Wrapping of CommonJS to AMD

All this module does is wrap your CommonJS modules into the
[simplified CommonJS wrapper](https://github.com/amdjs/amdjs-api/wiki/AMD#simplified-commonjs-wrapping-) format, i.e.:

```js
define(function (require, exports, module) {
    // your CommonJS code here
});
```

It takes in a string and gives back a string:

```js
var amdWrap = require("amd-wrap-legacy");

var wrapped = amdWrap("module.exports = 5;");
var wrapThis = amdWrap(fs.readFileSync(__filename));
```

Line numbers will line up, although the first column will be shifted by
`"define (function (require, exports, module) {".length` characters.

## Difference from amd-wrap

This is similar to [amd-wrap](https://www.npmjs.com/package/amd-wrap) but adds features that can help transition from a non-CommonJS style RequireJS codebase.

It will not wrap if:
- the file is already wrapped
- the file begins with function( that suggests a module on Window
- the file starts with a comment `// amd-wrap:disable`

Limitations:
- if comments preceded the require() or define(), it will wrap (I tried strip-comments lib, but [it chokes](https://github.com/jonschlinkert/strip-comments/issues/18) in some cases, and the only reliable solution is a parser, which seems like overkill)
