---
title: "URLPattern: hash property"
short-title: hash
slug: Web/API/URLPattern/hash
page-type: web-api-instance-property
browser-compat: api.URLPattern.hash
---

{{APIRef("URL Pattern API")}} {{AvailableInWorkers}}

The **`hash`** read-only property of the {{domxref("URLPattern")}} interface is a
string containing the pattern used to match the fragment part
of a URL. This value may differ from the input to the constructor due to
normalization.

## Value

A string.

## Examples

The below example creates a {{domxref("URLPattern")}} object with `books/:id`
for the `hash` part. This pattern matches any fragment that starts with `books/`
and ends with an arbitrary string identifier.

```js
const pattern = new URLPattern("https://example.org#books/:id");
console.log(pattern.hash); // 'books/:id'
```

## Specifications

{{Specifications}}

## Browser compatibility

{{Compat}}
