---
title: "Navigator: globalPrivacyControl property"
short-title: globalPrivacyControl
slug: Web/API/Navigator/globalPrivacyControl
page-type: web-api-instance-property
status:
  - experimental
browser-compat: api.Navigator.globalPrivacyControl
---

{{APIRef("DOM")}}{{SeeCompatTable}}

The **`Navigator.globalPrivacyControl`** read-only property returns the user's [Global Privacy Control](https://globalprivacycontrol.org/) setting for the current website.
This setting indicates whether the user consents to the website or service selling or sharing their personal information with third parties.

The value of the property reflects that of the {{httpheader("Sec-GPC")}} HTTP header.

## Value

`true` if the user explicitly _does not_ provide consent to sell or share their data.
`false` if the user either grants consent, or has not indicated a preference.

## Example

```js
console.log(navigator.globalPrivacyControl);
// "true" if the user has specifically indicated they do not want their data shared or sold, otherwise "false".
```

## Specifications

{{Specifications}}

## Browser compatibility

{{Compat}}

## See also

- {{HTTPHeader("Sec-GPC")}} header
- [globalprivacycontrol.org](https://globalprivacycontrol.org/)
- [Do Not Track on Wikipedia](https://en.wikipedia.org/wiki/Do_Not_Track)
