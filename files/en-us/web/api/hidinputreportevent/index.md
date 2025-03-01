---
title: HIDInputReportEvent
slug: Web/API/HIDInputReportEvent
page-type: web-api-interface
status:
  - experimental
browser-compat: api.HIDInputReportEvent
---

{{securecontext_header}}{{APIRef("WebHID API")}}{{SeeCompatTable}}{{AvailableInWorkers("window_and_worker_except_shared")}}

The **`HIDInputReportEvent`** interface of the [WebHID API](/en-US/docs/Web/API/WebHID_API) is passed to {{domxref("HIDDevice.inputreport_event", "inputreport")}} event of `HIDDevice` when an input report is received from any associated HID device.

{{InheritanceDiagram}}

## Instance properties

_This interface also inherits properties from {{domxref("Event")}}._

- {{domxref("HIDInputReportEvent.data")}} {{ReadOnlyInline}} {{Experimental_Inline}}
  - : A {{jsxref("DataView")}} containing the data from the input report, excluding the `reportId` if the HID interface uses report IDs.
- {{domxref("HIDInputReportEvent.device")}} {{ReadOnlyInline}} {{Experimental_Inline}}
  - : The {{domxref("HIDDevice")}} instance that represents the HID interface that sent the input report.
- {{domxref("HIDInputReportEvent.reportId")}} {{ReadOnlyInline}} {{Experimental_Inline}}
  - : The one-byte identification prefix for this report, or 0 if the HID interface does not use report IDs.

## Instance methods

_This interface inherits methods from its parent, {{domxref("Event")}}._

## Examples

The following example demonstrates listening for an `inputReport` that will allow the application to detect which button is pressed on a Joy-Con Right device. You can see more examples, and live demos in the article [Connecting to uncommon HID devices](https://developer.chrome.com/docs/capabilities/hid).

```js
device.addEventListener("inputreport", (event) => {
  const { data, device, reportId } = event;

  // Handle only the Joy-Con Right device and a specific report ID.
  if (device.productId !== 0x2007 && reportId !== 0x3f) return;

  const value = data.getUint8(0);
  if (value === 0) return;

  const someButtons = { 1: "A", 2: "X", 4: "B", 8: "Y" };
  console.log(`User pressed button ${someButtons[value]}.`);
});
```

## Specifications

{{Specifications}}

## Browser compatibility

{{Compat}}
