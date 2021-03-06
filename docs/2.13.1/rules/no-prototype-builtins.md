---
title: Rule no-prototype-builtins
layout: doc
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->

# Disallow use of Object.prototypes builtins directly (no-prototype-builtins)

In ECMAScript 5.1, `Object.create` was added, which enables the creation of objects with a specified `[[Prototype]]`. `Object.create(null)` is a common pattern used to create objects that will be used as a Map. This can lead to errors when it is assumed that objects will have properties from `Object.prototype`. This rule prevents calling `Object.prototype` methods directly from an object.

## Rule Details

This rule disallows calling some `Object.prototype` methods directly on object instances.

Examples of **incorrect** code for this rule:

```js
/*eslint no-prototype-builtins: "error"*/

var hasBarProperty = foo.hasOwnProperty("bar");

var isPrototypeOfBar = foo.isPrototypeOf(bar);

var barIsEnumerable = foo.propertyIsEnumerable("bar");
```

Examples of **correct** code for this rule:

```js
/*eslint no-prototype-builtins: "error"*/

var hasBarProperty = {}.hasOwnProperty.call(foo, "bar");

var isPrototypeOfBar = {}.isPrototypeOf.call(foo, bar);

var barIsEnumerable = {}.propertyIsEnumerable.call(foo, "bar");
```

## When Not To Use It

You may want to turn this rule off if you will never use an object that shadows an `Object.prototype` method or which does not inherit from `Object.prototype`.

## Version

This rule was introduced in ESLint 2.11.0.

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/master/lib/rules/no-prototype-builtins.js)
* [Documentation source](https://github.com/eslint/eslint/tree/master/docs/rules/no-prototype-builtins.md)
