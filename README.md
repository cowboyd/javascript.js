# ecma.js

[![npm version](https://badge.fury.io/js/ecma.svg)](https://badge.fury.io/js/ecma)
[![Build Status](https://travis-ci.org/cowboyd/ecma.js.svg?branch=master)](https://travis-ci.org/cowboyd/ecma.js)

How often do you have code like this?

```js
import Thing from 'my/thing';
import OtherThing from 'other/thing';

// :-/
const { assign, keys } = Object;

//....

function assignThings() {
  return assign(new Thing(), new OtherThings());
}

```

For every other piece of code out there, it's very straight
forward. You import a name from a module, and then you use it later.
However, for builtin functions, which are really no different, you
have to either use them from a dynamically scoped global
object. e.g. `Object.assign`, or destructure them as a constant
assignment from the dynamically scoped global object.

The `ecma` module lets you treat all of your symbolic imports
the same, no exceptions:

``` javascript
import Thing from 'my/thing';
import OtherThing from 'other/thing';
import { assign, keys } from 'ecma/object';
```


### Details

For each JavaScript global supported, that global is the default
export, then, any properties of that global are exported as named
values.

So for example, the `Math` global has the properties `Math.PI` (the
constant), and `Math.pow` (raise any number to a power). We could
define a function to compute the area of a circle like so:

``` javascript
import { PI, pow } from 'ecma/math';

export function area(radius) {
  return PI * pow(radius, 2);
}
```

By the same token, you could also define it this way:

``` javascript
import Math from 'ecma/math';

export function area(radius) {
  return Math.PI * Math.pow(radius, 2);
}
```

Although that wouldn't have much value over just using the global,
dynamically scoped constant.

There are currently exports for:

* `ecma/array`
* `ecma/number`
* `ecma/object`
* `ecma/string`
