# Native Download Link: `download`

**Role:** let a real link request browser download behavior without a click handler or client-side blob generation.

```html
<a href="/account/recovery-phrase/download" download>
  Download recovery phrase
</a>
```

For sensitive or generated files, prefer a real server endpoint that returns the file as an attachment. The endpoint should authorize the request and set an appropriate `Content-Type` and `Content-Disposition`.

```http
Content-Type: text/plain; charset=UTF-8
Content-Disposition: attachment; filename="recovery-phrase.txt"
```

## State and security boundary

`download` is a browser navigation/download hint. It does not create the file, authorize access, or make a secret safe to expose in a URL.

Do not put recovery phrases, tokens, private keys or other secrets into query strings or `data:` URLs just to manufacture a client-side download. Keep sensitive material in the authenticated server response.

The server remains authoritative for:

- authentication and authorization;
- CSRF protection when the download action is state-sensitive or POST-backed;
- response headers and filename;
- expiry/revocation rules for one-time material.

## Compatibility boundary

The attribute is well established, but browser handling can differ for cross-origin resources and response headers. Same-origin application endpoints with an attachment response are the conservative design.

## Compose

- [real anchor navigation](anchor-navigation.md)
- [server-authoritative state](../principles/server-authoritative-state.md)

## Sources

- https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/a#download
- https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Disposition
