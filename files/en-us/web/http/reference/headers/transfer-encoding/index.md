---
title: Transfer-Encoding header
short-title: Transfer-Encoding
slug: Web/HTTP/Reference/Headers/Transfer-Encoding
page-type: http-header
browser-compat: http.headers.Transfer-Encoding
sidebar: http
---

The HTTP **`Transfer-Encoding`** {{glossary("request header", "request")}} and {{glossary("response header")}} specifies the form of encoding used to transfer messages between nodes on the network.

`Transfer-Encoding` is a [hop-by-hop header](/en-US/docs/Web/HTTP/Reference/Headers#hop-by-hop_headers), that is applied to a message between two nodes, not to a resource itself.
Each segment of a multi-node connection can use different `Transfer-Encoding` values.
If you want to compress data over the whole connection, use the end-to-end {{HTTPHeader("Content-Encoding")}} header instead.

In practice this header is rarely used, and in those cases it is almost always used with `chunked`.

That said, the specification indicates that when present in a message it indicates the compression used on the message in that hop, and/or whether the message has been chunked.
For example, `Transfer-Encoding: gzip, chunked` indicates that the content has been compressed using the gzip coding and then chunked using the chunked coding while forming the message body.

The header is optional in responses to a {{HTTPMethod("HEAD")}} request as these messages have no body and, therefore, no transfer encoding.
When present it indicates the value that would have applied to the corresponding response to a {{HTTPMethod("GET")}} message, if that `GET` request did not include a preferred `Transfer-Encoding`.

> [!WARNING]
> HTTP/2 disallows all uses of the `Transfer-Encoding` header.
> HTTP/2 and later provide more efficient mechanisms for data streaming than chunked transfer.
> Usage of the header in HTTP/2 may likely result in a specific `protocol error`.

<table class="properties">
  <tbody>
    <tr>
      <th scope="row">Header type</th>
      <td>
        {{Glossary("Request header")}}, {{Glossary("Response header")}}, {{Glossary("Content header")}}
      </td>
    </tr>
    <tr>
      <th scope="row">{{Glossary("Forbidden request header")}}</th>
      <td>Yes</td>
    </tr>
  </tbody>
</table>

## Syntax

```http
Transfer-Encoding: chunked
Transfer-Encoding: compress
Transfer-Encoding: deflate
Transfer-Encoding: gzip

// Several values can be listed, separated by a comma
Transfer-Encoding: gzip, chunked
```

## Directives

- `chunked`
  - : Data is sent in a series of chunks.
    Content can be sent in streams of unknown size to be transferred as a sequence of length-delimited buffers, so the sender can keep a connection open, and let the recipient know when it has received the entire message.
    The {{HTTPHeader("Content-Length")}} header must be omitted, and at the beginning of each chunk, a string of hex digits indicate the size of the chunk-data in octets, followed by `\r\n` and then the chunk itself, followed by another `\r\n`.
    The terminating chunk is a zero-length chunk.
- `compress`
  - : A format using the [Lempel-Ziv-Welch](https://en.wikipedia.org/wiki/LZW) (LZW) algorithm.
    The value name was taken from the UNIX _compress_ program, which implemented this algorithm.
    Like the compress program, which has disappeared from most UNIX distributions, this content-encoding is used by almost no browsers today, partly because of a patent issue (which expired in 2003).
- `deflate`
  - : Using the [zlib](https://en.wikipedia.org/wiki/Zlib) structure (defined in [RFC 1950](https://datatracker.ietf.org/doc/html/rfc1950)), with the [_deflate_](https://en.wikipedia.org/wiki/DEFLATE) compression algorithm (defined in [RFC 1951](https://datatracker.ietf.org/doc/html/rfc1952)).
- `gzip`
  - : A format using the [Lempel-Ziv coding](https://en.wikipedia.org/wiki/LZ77_and_LZ78#LZ77) (LZ77), with a 32-bit CRC.
    This is originally the format of the UNIX _gzip_ program.
    The HTTP/1.1 standard also recommends that the servers supporting this content-encoding should recognize `x-gzip` as an alias, for compatibility purposes.

## Examples

### Response with chunked encoding

Chunked encoding is useful when larger amounts of data are sent to the client and the total size of the response may not be known until the request has been fully processed.
For example, when generating a large HTML table resulting from a database query or when transmitting large images.
A chunked response looks like this:

```http
HTTP/1.1 200 OK
Content-Type: text/plain
Transfer-Encoding: chunked

7\r\n
Mozilla\r\n
11\r\n
Developer Network\r\n
0\r\n
\r\n
```

## Specifications

{{Specifications}}

## Browser compatibility

{{Compat}}

## See also

- {{HTTPHeader("Accept-Encoding")}}
- {{HTTPHeader("Content-Encoding")}}
- {{HTTPHeader("Content-Length")}}
- [Chunked transfer encoding](https://en.wikipedia.org/wiki/Chunked_transfer_encoding)
