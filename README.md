Node.js: customizable-fs-extra
==============================

[`fs-extra`](https://github.com/jprichardson/node-fs-extra/) but customizable by overriding modules using monkey patching.

Api
---

`customizable-fs-extra` has exactly the same API as fs-extra.

Customization
-------------

### The fs module

Just replace the `fs` module with the custom `fs`. The custom `fs` module must have the same properties and methods as the `fs` module.

### Adjusting to the custom file system api

One of the following modules can be replaced using proxyquire. The paths are relative to the `proxyquire-fs-extra` root. 

- `./lib/override/node-version`: An `object` containing the following property
    - `value`: A `string` being the node file system api the custom file system api is equivalent to.
- `./lib/override/options`: An `object` containting the following properties:
    - `useBigInt`: A `boolean` whether the custom file system supports big-ints. Normally, this value is derived by comparing the current node version.
    - `useNativeRecursiveOption`: A `boolean` whether the custom file system supports the recursive option. Normally, this value is derived by comparing the current node version.

Examples
--------

### Using proxyquire

```js
const proxyquire = require('proxyquire')
const memfs = require('memfs')

proxyquire("fs-extra", {
    'fs': {
        ...memfs,
        '@global': true
    },
    './lib/override/node-version': {
        value: '14.0.0',
        '@global': true
    }
});
```

### Using webpack

TODO
