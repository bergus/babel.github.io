---
layout: docs
title: Proto to assign transform
description:
permalink: /docs/plugins/transform-proto-to-assign/
package: babel-plugin-transform-proto-to-assign
---

This plugin allows Babel to transform all `__proto__` assignments to a method that will do a shallow
copy of all properties.

This means that the following **will** work:

```javascript
var foo = { a: 1 };
var bar = { b: 2 };
bar.__proto__ = foo;
bar.a; // 1
bar.b; // 2
```

however the following **will not**:

```javascript
var foo = { a: 1 };
var bar = { b: 2 };
bar.__proto__ = foo;
bar.a; // 1
foo.a = 2;
bar.a; // 1 - should be 2 but remember that nothing is bound and it's a straight copy
```

This is a case that you have to be aware of if you intend to use this
transformer.

## Example

**In**

```javascript
bar.__proto__ = foo;
```

**Out**

```javascript
_defaults(bar, foo);
```

## Installation

```sh
$ npm install babel-plugin-transform-proto-to-assign
```

## Usage

Add the following line to your `.babelrc` file:

```json
{
  "plugins": ["transform-proto-to-assign"]
}
```
