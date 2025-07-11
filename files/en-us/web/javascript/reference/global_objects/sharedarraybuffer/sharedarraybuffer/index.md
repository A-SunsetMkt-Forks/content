---
title: SharedArrayBuffer() constructor
short-title: SharedArrayBuffer()
slug: Web/JavaScript/Reference/Global_Objects/SharedArrayBuffer/SharedArrayBuffer
page-type: javascript-constructor
browser-compat: javascript.builtins.SharedArrayBuffer.SharedArrayBuffer
sidebar: jsref
---

> [!NOTE]
> The `SharedArrayBuffer` constructor may not always be globally available unless certain [security requirements](/en-US/docs/Web/JavaScript/Reference/Global_Objects/SharedArrayBuffer#security_requirements) are met.

The **`SharedArrayBuffer()`** constructor creates {{jsxref("SharedArrayBuffer")}} objects.

{{InteractiveExample("JavaScript Demo: SharedArrayBuffer() constructor", "shorter")}}

```js interactive-example
// Create a SharedArrayBuffer with a size in bytes
const buffer = new SharedArrayBuffer(8);

console.log(buffer.byteLength);
// Expected output: 8
```

## Syntax

```js-nolint
new SharedArrayBuffer(length)
new SharedArrayBuffer(length, options)
```

> [!NOTE]
> `SharedArrayBuffer()` can only be constructed with [`new`](/en-US/docs/Web/JavaScript/Reference/Operators/new). Attempting to call it without `new` throws a {{jsxref("TypeError")}}.

### Parameters

- `length`
  - : The size, in bytes, of the array buffer to create.
- `options` {{optional_inline}}
  - : An object, which can contain the following properties:
    - `maxByteLength` {{optional_inline}}
      - : The maximum size, in bytes, that the shared array buffer can be resized to.

### Return value

A new `SharedArrayBuffer` object of the specified size, with its {{jsxref("SharedArrayBuffer/maxByteLength", "maxByteLength")}} property set to the specified `maxByteLength` if one was specified. Its contents are
initialized to 0.

## Examples

### Always use the new operator to create a SharedArrayBuffer

`SharedArrayBuffer` constructors are required to be constructed with a
{{jsxref("Operators/new", "new")}} operator. Calling a `SharedArrayBuffer`
constructor as a function without `new` will throw a {{jsxref("TypeError")}}.

```js example-bad
const sab = SharedArrayBuffer(1024);
// TypeError: calling a builtin SharedArrayBuffer constructor
// without new is forbidden
```

```js example-good
const sab = new SharedArrayBuffer(1024);
```

### Growing a growable SharedArrayBuffer

In this example, we create an 8-byte buffer that is growable to a max length of 16 bytes, then {{jsxref("SharedArrayBuffer/grow", "grow()")}} it to 12 bytes:

```js
const buffer = new SharedArrayBuffer(8, { maxByteLength: 16 });

buffer.grow(12);
```

> [!NOTE]
> It is recommended that `maxByteLength` is set to the smallest value possible for your use case. It should never exceed `1073741824` (1GB), to reduce the risk of out-of-memory errors.

## Specifications

{{Specifications}}

## Browser compatibility

{{Compat}}

## See also

- {{jsxref("Atomics")}}
- {{jsxref("ArrayBuffer")}}
- [JavaScript typed arrays](/en-US/docs/Web/JavaScript/Guide/Typed_arrays) guide
