---
title: "BluetoothRemoteGATTCharacteristic: writeValue() method"
short-title: writeValue()
slug: Web/API/BluetoothRemoteGATTCharacteristic/writeValue
page-type: web-api-instance-method
status:
  - deprecated
browser-compat: api.BluetoothRemoteGATTCharacteristic.writeValue
---

{{APIRef("Bluetooth API")}}{{Deprecated_header}}{{SecureContext_Header}}

Use {{DOMxRef("BluetoothRemoteGATTCharacteristic.writeValueWithResponse()")}} and {{DOMxRef("BluetoothRemoteGATTCharacteristic.writeValueWithoutResponse()")}} instead.

The **`BluetoothRemoteGATTCharacteristic.writeValue()`** method sets a {{domxref("BluetoothRemoteGATTCharacteristic")}} object's `value` property to the bytes contained in a given {{JSxRef("ArrayBuffer")}}, [writes the characteristic value with optional response](https://webbluetoothcg.github.io/web-bluetooth/#writecharacteristicvalue), and returns the resulting {{JSxRef("Promise")}}.

## Syntax

```js-nolint
writeValue(value)
```

### Parameters

- `value`
  - : An {{jsxref("ArrayBuffer")}}.

### Return value

A {{jsxref("Promise")}}.

## Specifications

{{Specifications}}

## Browser compatibility

{{Compat}}
