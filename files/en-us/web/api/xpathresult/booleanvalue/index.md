---
title: "XPathResult: booleanValue property"
short-title: booleanValue
slug: Web/API/XPathResult/booleanValue
page-type: web-api-instance-property
browser-compat: api.XPathResult.booleanValue
---

{{APIRef("DOM XPath")}} {{AvailableInWorkers}}

The read-only **`booleanValue`** property of the
{{domxref("XPathResult")}} interface returns the boolean value of a result with
{{domxref("XPathResult.resultType")}} being `BOOLEAN_TYPE`.

## Value

The return value is the boolean value of the `XPathResult` returned by
{{domxref("Document.evaluate()")}}.

### Exceptions

#### TYPE_ERR

In case {{domxref("XPathResult.resultType")}} is not `BOOLEAN_TYPE`, a
{{domxref("DOMException")}} of type `TYPE_ERR` is thrown.

## Examples

The following example shows the use of the `booleanValue` property.

### HTML

```html
<div>XPath example</div>
<p>Text is 'XPath example': <output></output></p>
```

### JavaScript

```js
const xpath = "//div/text() = 'XPath example'";
const result = document.evaluate(
  xpath,
  document,
  null,
  XPathResult.BOOLEAN_TYPE,
  null,
);
document.querySelector("output").textContent = result.booleanValue;
```

### Result

{{EmbedLiveSample('Examples', 400, 70)}}

## Specifications

{{Specifications}}

## Browser compatibility

{{Compat}}
