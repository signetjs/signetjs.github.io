The Signet Type System
======================

## What is Signet? ##

Signet is a fast, expressive documentation and type language for your Javascript source. Signet is not your parents' type system; it is rich, powerful, extensible and supports typed thinking in a way that frees you rather than constraining you to the weakened notion of a class-based type system.

Just like Javascript, Signet treats everything as a first-class type entity including functions, objects, arrays, numbers and others. You read correctly, Signet supports the array type out of the box, along with refined types like int, formatted string, tuple, variant and more!

Algebraic types? Yeah, we have algebraic types. Signet supports sum types as "variant" and product types as "tuple." Signet supports higher-kinded types as well and allows you to extend, add, mix and match your own types any way you see fit. This means you can be as specific or generic as you like without sacrificing expression or the stability of your code.

Signet is a FAST run-time type checker. Instead of waiting for your code to either behave badly or throw some oddball error, Signet will actually verify arguments against your function contract in real time and provide immediate feedback with meaninful messages, all in just a couple microseconds. This means you get an extra helping hand in debugging your code without sacrificing speed or quality. You can even guard against things like argument ordering issues with dependent type declarations.

## Getting Started ##

Using Signet is as simple as an NPM install, and a simple configuration. For node projects, install Signet as follows:

`npm install signet --save-dev`

### Node Usage ###

Signet imports as a factory to ensure projects don't cross pollute the type pool and should be prepared for use as follows:

```
    'use strict';

    const signet = require('signet')();

    // set up your custom types here!

    module.exports = signet;
```

Now you can simply include your configuration file and use Signet anywhere you need to expose an API!

### Client Usage ###

In the browser, Signet will self-instantiate and the appropriate minified file and associated map file can be found in the following location:

```
project-root/node_modules/signet/dist/signet.min.js
project-root/node_modules/signet/dist/signet.min.js.map
```

After the minified file is included in your client-side project, you can simply use signet straight out of the box.

### Type Checking ###

Signet allows for document and enforcing function contracts with the enforce function:

```
    const range = signet.enforce(
        'start < end :: start:number, end:number, increment:[leftBounded<1>] => array<number>',
        function range (start, end, increment = 1) {
            var result = [];

            for(i = start; i <= end; i += increment) {
                result.push(i);
            }

            return result;
        }
    );

    range('1', '20'); // TypeError: range expected a value of type start:number but got 1 of type string

    range(20, 1); // TypeError: range expected a value of type start < end but got start = 20 and end = 1 of type string

    range(1, 20, -1); // TypeError: range expected a value of type increment:[leftBounded<1>] but got -1 of type number

    range(1, 20, 2); // [1, 3, 5, 7, 9, 11, 13, 15, 17 ,19]
```

Signet also allows for in-function type checking with signet.isTypeOf:

```
    const isString = signet.isTypeOf('string');

    isString('foo'); // true
    isString(5); // false

    // You would likely never do this, but
    const isIntOrObject = signet.isTypeOf('variant<int; object>');

    isIntOrObject(99); // true
    isIntOrObject({}); // true
    isIntOrObject(5.5); // false
```