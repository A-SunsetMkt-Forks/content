---
title: RegExp.prototype[Symbol.matchAll]()
short-title: "[Symbol.matchAll]()"
slug: Web/JavaScript/Reference/Global_Objects/RegExp/Symbol.matchAll
page-type: javascript-instance-method
browser-compat: javascript.builtins.RegExp.@@matchAll
sidebar: jsref
---

The **`[Symbol.matchAll]()`** method of {{jsxref("RegExp")}} instances specifies how [`String.prototype.matchAll`](/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/matchAll) should behave.

{{InteractiveExample("JavaScript Demo: RegExp.prototype[Symbol.matchAll]()", "taller")}}

```js interactive-example
class MyRegExp extends RegExp {
  [Symbol.matchAll](str) {
    const result = RegExp.prototype[Symbol.matchAll].call(this, str);
    if (!result) {
      return null;
    }
    return Array.from(result);
  }
}

const re = new MyRegExp("-\\d+", "g");
console.log("2016-01-02|2019-03-07".matchAll(re));
// Expected output: Array [Array ["-01"], Array ["-02"], Array ["-03"], Array ["-07"]]
```

## Syntax

```js-nolint
regexp[Symbol.matchAll](str)
```

### Parameters

- `str`
  - : A {{jsxref("String")}} that is a target of the match.

### Return value

An [iterable iterator object](/en-US/docs/Web/JavaScript/Reference/Global_Objects/Iterator) (which is not restartable) of matches. Each match is an array with the same shape as the return value of {{jsxref("RegExp.prototype.exec()")}}.

## Description

This method is called internally in {{jsxref("String.prototype.matchAll()")}}. For example, the following two examples return the same result.

```js
"abc".matchAll(/a/g);

/a/g[Symbol.matchAll]("abc");
```

Like [`[Symbol.split]()`](/en-US/docs/Web/JavaScript/Reference/Global_Objects/RegExp/Symbol.split), `[Symbol.matchAll]()` starts by using [`[Symbol.species]`](/en-US/docs/Web/JavaScript/Reference/Global_Objects/RegExp/Symbol.species) to construct a new regex, thus avoiding mutating the original regexp in any way. [`lastIndex`](/en-US/docs/Web/JavaScript/Reference/Global_Objects/RegExp/lastIndex) starts as the original regex's value.

```js
const regexp = /[a-c]/g;
regexp.lastIndex = 1;
const str = "abc";
Array.from(str.matchAll(regexp), (m) => `${regexp.lastIndex} ${m[0]}`);
// [ "1 b", "1 c" ]
```

The validation that the input is a global regex happens in [`String.prototype.matchAll()`](/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/matchAll). `[Symbol.matchAll]()` does not validate the input. If the regex is not global, the returned iterator yields the [`exec()`](/en-US/docs/Web/JavaScript/Reference/Global_Objects/RegExp/exec) result once and then returns `undefined`. If the regexp is global, each time the returned iterator's `next()` method is called, the regex's [`exec()`](/en-US/docs/Web/JavaScript/Reference/Global_Objects/RegExp/exec) is called and the result is yielded.

When the regex is sticky and global, it will still perform sticky matches — i.e., it will not match any occurrences beyond the `lastIndex`.

```js
console.log(Array.from("ab-c".matchAll(/[abc]/gy)));
// [ [ "a" ], [ "b" ] ]
```

If the current match is an empty string, the [`lastIndex`](/en-US/docs/Web/JavaScript/Reference/Global_Objects/RegExp/lastIndex) will still be advanced. If the regex has the [`u`](/en-US/docs/Web/JavaScript/Reference/Global_Objects/RegExp/unicode) flag, it advances by one Unicode code point; otherwise, it advances by one UTF-16 code point.

```js
console.log(Array.from("😄".matchAll(/(?:)/g)));
// [ [ "" ], [ "" ], [ "" ] ]

console.log(Array.from("😄".matchAll(/(?:)/gu)));
// [ [ "" ], [ "" ] ]
```

This method exists for customizing the behavior of `matchAll()` in {{jsxref("RegExp")}} subclasses.

## Examples

### Direct call

This method can be used in almost the same way as {{jsxref("String.prototype.matchAll()")}}, except for the different value of `this` and the different order of arguments.

```js
const re = /\d+/g;
const str = "2016-01-02";
const result = re[Symbol.matchAll](str);

console.log(Array.from(result, (x) => x[0]));
// [ "2016", "01", "02" ]
```

### Using `[Symbol.matchAll]()` in subclasses

Subclasses of {{jsxref("RegExp")}} can override the `[Symbol.matchAll]()` method to modify the default behavior.

For example, to return an {{jsxref("Array")}} instead of an [iterator](/en-US/docs/Web/JavaScript/Guide/Iterators_and_generators):

```js
class MyRegExp extends RegExp {
  [Symbol.matchAll](str) {
    const result = RegExp.prototype[Symbol.matchAll].call(this, str);
    return result ? Array.from(result) : null;
  }
}

const re = new MyRegExp("(\\d+)-(\\d+)-(\\d+)", "g");
const str = "2016-01-02|2019-03-07";
const result = str.matchAll(re);

console.log(result[0]);
// [ "2016-01-02", "2016", "01", "02" ]

console.log(result[1]);
// [ "2019-03-07", "2019", "03", "07" ]
```

## Specifications

{{Specifications}}

## Browser compatibility

{{Compat}}

## See also

- [Polyfill of `RegExp.prototype[Symbol.matchAll]` in `core-js`](https://github.com/zloirock/core-js#ecmascript-string-and-regexp)
- [es-shims polyfill of `RegExp.prototype[Symbol.matchAll]`](https://www.npmjs.com/package/string.prototype.matchall)
- {{jsxref("String.prototype.matchAll()")}}
- [`RegExp.prototype[Symbol.match]()`](/en-US/docs/Web/JavaScript/Reference/Global_Objects/RegExp/Symbol.match)
- [`RegExp.prototype[Symbol.replace]()`](/en-US/docs/Web/JavaScript/Reference/Global_Objects/RegExp/Symbol.replace)
- [`RegExp.prototype[Symbol.search]()`](/en-US/docs/Web/JavaScript/Reference/Global_Objects/RegExp/Symbol.search)
- [`RegExp.prototype[Symbol.split]()`](/en-US/docs/Web/JavaScript/Reference/Global_Objects/RegExp/Symbol.split)
- {{jsxref("Symbol.matchAll")}}
