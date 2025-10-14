# CfhttpHttpClient

### `debug`

Return a struct of information showing how the client will execute the [`HyperRequest`](../../making-requests/hyperrequest.md). This will be used by a developer to debug any differences between the generated request values and the expected request values.

| Name | Type                                                    | Required | Default | Description                                                           |
| ---- | ------------------------------------------------------- | -------- | ------- | --------------------------------------------------------------------- |
| req  | [`HyperRequest`](../../making-requests/hyperrequest.md) | `true`   |         | The [`HyperRequest`](../../making-requests/hyperrequest.md) to debug. |

**Return**:

```json
{
    "attributes" : attrCollection,
    "body"       : {
        "headers" : cfhttpHeaders,
        "params"  : cfhttpParams,
        "files"   : cfhttpFiles,
        "body"    : cfhttpBody,
        "cookies" : cfhttpCookies
    }
}
```
