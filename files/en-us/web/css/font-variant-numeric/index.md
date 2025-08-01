---
title: font-variant-numeric
slug: Web/CSS/font-variant-numeric
page-type: css-property
browser-compat: css.properties.font-variant-numeric
sidebar: cssref
---

The **`font-variant-numeric`** [CSS](/en-US/docs/Web/CSS) property controls the usage of alternate glyphs for numbers, fractions, and ordinal markers.

{{InteractiveExample("CSS Demo: font-variant-numeric")}}

```css interactive-example-choice
font-variant-numeric: normal;
```

```css interactive-example-choice
font-variant-numeric: slashed-zero;
```

```css interactive-example-choice
font-variant-numeric: tabular-nums;
```

```css interactive-example-choice
font-variant-numeric: oldstyle-nums;
```

```html interactive-example
<section id="default-example">
  <div id="example-element">
    <table>
      <tr>
        <td><span class="tabular">0</span></td>
      </tr>
      <tr>
        <td><span class="tabular">3.54</span></td>
      </tr>
      <tr>
        <td><span class="tabular">1.71</span></td>
      </tr>
    </table>
  </div>
</section>
```

```css interactive-example
@font-face {
  font-family: "Fira Sans";
  src:
    local("FiraSans-Regular"),
    url("/shared-assets/fonts/FiraSans-Regular.woff2") format("woff2");
  font-weight: normal;
  font-style: normal;
}

section {
  font-family: "Fira Sans", sans-serif;
  margin-top: 10px;
  font-size: 1.5em;
}

#example-element table {
  margin-left: auto;
  margin-right: auto;
}

.tabular {
  border: 1px solid;
}
```

## Syntax

```css
font-variant-numeric: normal;
font-variant-numeric: ordinal;
font-variant-numeric: slashed-zero;
font-variant-numeric: lining-nums; /* <numeric-figure-values> */
font-variant-numeric: oldstyle-nums; /* <numeric-figure-values> */
font-variant-numeric: proportional-nums; /* <numeric-spacing-values> */
font-variant-numeric: tabular-nums; /* <numeric-spacing-values> */
font-variant-numeric: diagonal-fractions; /* <numeric-fraction-values> */
font-variant-numeric: stacked-fractions; /* <numeric-fraction-values> */
font-variant-numeric: oldstyle-nums stacked-fractions;

/* Global values */
font-variant-numeric: inherit;
font-variant-numeric: initial;
font-variant-numeric: revert;
font-variant-numeric: revert-layer;
font-variant-numeric: unset;
```

This property can take one of two forms:

- either the keyword value `normal`
- or one or more of the other values listed below, space-separated, in any order.

### Values

- `normal`
  - : This keyword leads to the deactivation of the use of such alternate glyphs.

- `ordinal`
  - : This keyword forces the use of special glyphs for the ordinal markers, like 1st, 2nd, 3rd, 4th in English or a 1a in Italian. It corresponds to the OpenType values `ordn`.

- `slashed-zero`
  - : This keyword forces the use of a 0 with a slash; this is useful when a clear distinction between O and 0 is needed. It corresponds to the OpenType values `zero`.

- _`<numeric-figure-values>`_
  - : These values control the figures used for numbers. Two values are possible:
    - `lining-nums` activating the set of figures where numbers are all lying on the baseline. It corresponds to the OpenType values `lnum`.
    - `oldstyle-nums` activating the set of figures where some numbers, like 3, 4, 7, 9 have descenders. It corresponds to the OpenType values `onum`.

- _`<numeric-spacing-values>`_
  - : These values controls the sizing of figures used for numbers. Two values are possible:
    - `proportional-nums` activating the set of figures where numbers are not all of the same size. It corresponds to the OpenType values `pnum`.
    - `tabular-nums` activating the set of figures where numbers are all of the same size, allowing them to be easily aligned like in tables. It corresponds to the OpenType values `tnum`.

- _`<numeric-fraction-values>`_
  - : These values controls the glyphs used to display fractions. Two values are possible:
    - `diagonal-fractions` activating the set of figures where the numerator and denominator are made smaller and separated by a slash. It corresponds to the OpenType values `frac`.
    - `stacked-fractions` activating the set of figures where the numerator and denominator are made smaller, stacked and separated by a horizontal line. It corresponds to the OpenType values `afrc`.

## Formal definition

{{cssinfo}}

## Formal syntax

{{csssyntax}}

## Examples

### Setting ordinal numeric forms

Click "Play" in the code blocks below to edit the example in the MDN Playground:

```html live-sample___font-variant-numeric-example
<p class="ordinal">1st, 2nd, 3rd, 4th, 5th</p>
```

```css live-sample___font-variant-numeric-example
@font-face {
  font-family: "Source Sans Pro";
  src: url("https://mdn.github.io/shared-assets/fonts/SourceSansPro-Regular.otf")
    format("opentype");
  font-weight: 400;
  font-style: normal;
}

.ordinal {
  font-family: "Source Sans Pro", sans-serif;
  font-size: 2rem;
  font-variant-numeric: ordinal;
}
```

{{EmbedLiveSample("font-variant-numeric-example")}}

## Specifications

{{Specifications}}

## Browser compatibility

{{Compat}}

## See also

- [`font-variant`](/en-US/docs/Web/CSS/font-variant)
- [`font-variant-alternates`](/en-US/docs/Web/CSS/font-variant-alternates)
- [`font-variant-caps`](/en-US/docs/Web/CSS/font-variant-caps)
- [`font-variant-east-asian`](/en-US/docs/Web/CSS/font-variant-east-asian)
- [`font-variant-emoji`](/en-US/docs/Web/CSS/font-variant-emoji)
- [`font-variant-ligatures`](/en-US/docs/Web/CSS/font-variant-ligatures)
- [`font-variant-position`](/en-US/docs/Web/CSS/font-variant-position)
