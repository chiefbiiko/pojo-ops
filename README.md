# pojo-ops

[![build status](http://img.shields.io/travis/chiefBiiko/pojo-ops.svg?style=flat)](http://travis-ci.org/chiefBiiko/pojo-ops) [![AppVeyor Build Status](https://ci.appveyor.com/api/projects/status/github/chiefBiiko/pojo-ops?branch=master&svg=true)](https://ci.appveyor.com/project/chiefBiiko/pojo-ops)

***

Operate on objects as you do on arrays.

***

## Get it

```js
npm install --save pojo-ops
```

***

## Usage

Essentially the same as all the equivalent `Array.prototype` methods.

```js
const ops = require('pojo-ops')

ops.keys({ a: 1, b: 2 })
// -> [ 'a', 'b' ]
ops.values({ a: 1, b: { c: 2 } })
// -> [ 1, { c: 2 } ]
ops.props({ a: 1, b: { c: 2 } })
// -> [ [ 'a', 1 ], [ 'b', { c: 2 } ] ]

ops.forEach({ a: 1, b: 2 }, (val, key, obj) => console.log(`${key}:${val}`))
// > a:1
// > b:2

ops.every({ a: 5, b: 4 }, (val, key, obj) => val % 2 === 0)
// -> false
ops.some({ a: 1, b: null, c: 3 }, (val, key, obj) => val === null)
// -> true

ops.map({ a: 1, b: 2 }, (val, key, obj) => 2 * val)
// -> { a: 2, b: 4 }
ops.filter({ a: 1, b: 2 }, (val, key, obj) => val % 2 === 0)
// -> { b: 2 }
ops.reduce({ a: 1, b: 2, c: 3 }, (acc, cur, key, obj) => acc += cur, 0)
// -> 6

ops.randomProp({ a: 1, b: 2 })
// -> [ ?, ? ]
ops.randomKey({ a: 1, b: 2 })
// -> ?
ops.randomVal({ a: 1, b: 2 })
// -> ?

ops.keysOf({ a: 1, g: 7, z: 7 }, 7)
// -> [ 'g', 'z' ]

ops.hasProp({ a: 1, z: 99 }, 'z', 99)
// -> true
ops.hasKey({ z: 9 }, 'a')
// -> false
ops.hasVal({ a: 1, z: 99 }, 99)
// -> true

ops.extend({ t: 0 }, { u: 1 }, { v: 2 }, { v: 8 })
// -> { t: 0, u: 1, v: 8 }
ops.extendLock({ t: 0 }, { u: 1 }, { v: 2 }, { v: 8 })
// -> { t: 0, u: 1, v: 2 }
```
None of the methods mutate the input object. `ops.extend` overwrites recurring keys, whereas `ops.extendLock` does not.

***

## License

[MIT](./license.md)
