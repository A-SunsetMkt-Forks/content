---
title: Attribute
slug: Glossary/Attribute
page-type: glossary-definition
---

{{GlossarySidebar}}

An **attribute** extends an {{Glossary("HTML")}} or {{Glossary("XML")}} {{Glossary("element")}}, changing its behavior or providing metadata.

An attribute always has the form `name="value"` (the attribute's identifier followed by its associated value). You may see attributes without an equals sign or a value. That is a shorthand for providing the empty string in HTML. However, this is not valid in XML: XML requires all attributes to have an explicit value.

A number of HTML attributes are {{Glossary("Boolean/HTML", "boolean attributes")}}. These attributes' values are only controlled by the presence or absence of the attribute. See {{Glossary("Boolean/HTML", "boolean attributes")}} for more information.

## Reflection of an attribute

Attributes may be _reflected_ into a particular property of the specific interface.
It means that the value of the attribute can be read by accessing the property,
and can be modified by setting the property to a different value.

For example, the `placeholder` below is reflected into {{domxref("HTMLInputElement.placeholder")}}.

Considering the following HTML:

```html
<input placeholder="Original placeholder" />
```

We can check the reflection between {{domxref("HTMLInputElement.placeholder")}} and the attribute using:

```js
const input = document.querySelector("input");
const attr = input.getAttributeNode("placeholder");
console.log(attr.value);
console.log(input.placeholder); // Prints the same value as `attr.value`

// Changing placeholder value will also change the value of the reflected attribute.
input.placeholder = "Modified placeholder";
console.log(attr.value); // Prints `Modified placeholder`
```

## See also

- [HTML attribute reference](/en-US/docs/Web/HTML/Reference/Attributes)
- Information about HTML's [global attributes](/en-US/docs/Web/HTML/Reference/Global_attributes)
- XML StartTag Attribute Recommendation in [W3C XML Recommendation](https://www.w3.org/TR/xml#sec-starttags)
- Related glossary terms:
  - {{Glossary("Element")}}
  - {{Glossary("Tag")}}
  - {{Glossary("HTML")}}
  - {{Glossary("XML")}}
  - {{Glossary("Boolean/HTML", "Boolean attributes")}}
  - {{Glossary("Enumerated", "Enumerated attributes")}}
