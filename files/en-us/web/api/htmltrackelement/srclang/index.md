---
title: "HTMLTrackElement: srclang property"
short-title: srclang
slug: Web/API/HTMLTrackElement/srclang
page-type: web-api-instance-property
browser-compat: api.HTMLTrackElement.srclang
---

{{APIRef("HTML DOM")}}

The **`srclang`** property of the {{domxref("HTMLTrackElement")}} interface reflects the value of
the {{HTMLElement("track")}} element's [`srclang`](/en-US/docs/Web/HTML/Reference/Elements/track#srclang) attribute or the empty string if not defined.

The `srclang` attribute is a {{glossary("BCP 47 language tag")}} indicating the language of the text track's data.

## Value

A string.

## Example

```js
const trackElement = document.getElementById("exampleTrack");
console.log(`Track's language: ${trackElement.srclang}`);
trackElement.srclang = "en-US";
```

## Specifications

{{Specifications}}

## Browser compatibility

{{Compat}}

## See also

- {{domxref("HTMLTrackElement")}}
- {{HTMLElement("track")}}
