---
title: Sec-CH-Prefers-Reduced-Motion header
short-title: Sec-CH-Prefers-Reduced-Motion
slug: Web/HTTP/Reference/Headers/Sec-CH-Prefers-Reduced-Motion
page-type: http-header
status:
  - experimental
browser-compat: http.headers.Sec-CH-Prefers-Reduced-Motion
sidebar: http
---

{{SeeCompatTable}}{{SecureContext_Header}}

The HTTP **`Sec-CH-Prefers-Reduced-Motion`** {{Glossary("request header")}} is a [user agent client hint](/en-US/docs/Web/HTTP/Guides/Client_hints#user_preference_media_features_client_hints) which indicates the user agent's preference for animations to be displayed with reduced motion.

If a server signals to a client via the {{httpheader("Accept-CH")}} header that it accepts `Sec-CH-Prefers-Reduced-Motion`, the client can then respond with this header to indicate the user's preference for reduced motion. The server can send the client appropriately adapted content, for example, JavaScript or CSS, to reduce the motion of any animations presented on subsequent rendered content. This could include reducing the speed or amplitude of movement to reduce discomfort for those with vestibular motion disorders.

This header is modeled on the {{cssxref("@media/prefers-reduced-motion", "prefers-reduced-motion")}} media query.

<table class="properties">
  <tbody>
    <tr>
      <th scope="row">Header type</th>
      <td>
        {{Glossary("Request header")}},
        <a href="/en-US/docs/Web/HTTP/Guides/Client_hints">Client hint</a>
      </td>
    </tr>
    <tr>
      <th scope="row">{{Glossary("Forbidden request header")}}</th>
      <td>Yes (<code>Sec-</code> prefix)</td>
    </tr>
  </tbody>
</table>

## Syntax

```http
Sec-CH-Prefers-Reduced-Motion: <preference>
```

### Directives

- `<preference>`
  - : The user agent's preference for reduced-motion animations. This is often taken from the underlying operating system's setting. The value of this directive can be either `no-preference` or `reduce`.

## Examples

### Using Sec-CH-Prefers-Reduced-Motion

The client makes an initial request to the server:

```http
GET / HTTP/1.1
Host: example.com
```

The server responds, telling the client via {{httpheader("Accept-CH")}} that it accepts `Sec-CH-Prefers-Reduced-Motion`. In this example {{httpheader("Critical-CH")}} is also used, indicating that `Sec-CH-Prefers-Reduced-Motion` is considered a [critical client hint](/en-US/docs/Web/HTTP/Guides/Client_hints#critical_client_hints).

```http
HTTP/1.1 200 OK
Content-Type: text/html
Accept-CH: Sec-CH-Prefers-Reduced-Motion
Vary: Sec-CH-Prefers-Reduced-Motion
Critical-CH: Sec-CH-Prefers-Reduced-Motion
```

> [!NOTE]
> We've also specified `Sec-CH-Prefers-Reduced-Motion` in the {{httpheader("Vary")}} header to indicate to the browser that the served content will differ based on this header value, even if the URL stays the same, so the browser shouldn't just use an existing cached response and instead should cache this response separately. Each header listed in the `Critical-CH` header should also be present in the `Accept-CH` and `Vary` headers.

The client automatically retries the request (due to `Critical-CH` being specified above), telling the server via `Sec-CH-Prefers-Reduced-Motion` that it has a user preference for reduced-motion animations:

```http
GET / HTTP/1.1
Host: example.com
Sec-CH-Prefers-Reduced-Motion: "reduce"
```

The client will include the header in subsequent requests in the current session unless the `Accept-CH` changes in responses to indicate that it is no longer supported by the server.

## Specifications

{{Specifications}}

## Browser compatibility

{{Compat}}

## See also

- [Client hints](/en-US/docs/Web/HTTP/Guides/Client_hints)
- [User-Agent Client Hints API](/en-US/docs/Web/API/User-Agent_Client_Hints_API)
- {{HTTPHeader("Accept-CH")}}
- [`prefers-reduced-motion` CSS Media Query](/en-US/docs/Web/CSS/@media/prefers-reduced-motion)
- [HTTP Caching: Vary](/en-US/docs/Web/HTTP/Guides/Caching#vary) and {{HTTPHeader("Vary")}} header
- [Improving user privacy and developer experience with User-Agent Client Hints](https://developer.chrome.com/docs/privacy-security/user-agent-client-hints) (developer.chrome.com)
