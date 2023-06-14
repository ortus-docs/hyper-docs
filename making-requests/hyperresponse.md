# HyperResponse

The `HyperResponse` component is a read-only wrapper to easily grab different information about the response.

### `getResponseId`

Gets the unique response ID representing this response.

| Name         | Type | Required | Default | Description |
| ------------ | ---- | -------- | ------- | ----------- |
| No arguments |      |          |         |             |

**Return**: `String`

### `getStatusCode`

Gets the status code for the response.

| Name         | Type | Required | Default | Description |
| ------------ | ---- | -------- | ------- | ----------- |
| No arguments |      |          |         |             |

**Return**: `numeric`

### `getStatusText`

Gets the status text for the response.

| Name         | Type | Required | Default | Description |
| ------------ | ---- | -------- | ------- | ----------- |
| No arguments |      |          |         |             |

**Return**: `String`

### `getStatus`

Returns the status code and status text as a single string.

| Name         | Type | Required | Default | Description |
| ------------ | ---- | -------- | ------- | ----------- |
| No arguments |      |          |         |             |

**Return**: `String`

### `getData`

Gets the data for the response.

| Name         | Type | Required | Default | Description |
| ------------ | ---- | -------- | ------- | ----------- |
| No arguments |      |          |         |             |

**Return**: `String`

### `getRequestID`

Returns the id of the request to which this response is related.

| Name         | Type | Required | Default | Description |
| ------------ | ---- | -------- | ------- | ----------- |
| No arguments |      |          |         |             |

**Return**: `String`

### `getRequest`

Gets the [HyperRequest](hyperrequest.md) instance associated with this response.

| Name         | Type | Required | Default | Description |
| ------------ | ---- | -------- | ------- | ----------- |
| No arguments |      |          |         |             |

**Return**: [`HyperRequest`](hyperrequest.md)

### `getCharset`

Gets the charset value for the response.

| Name         | Type | Required | Default | Description |
| ------------ | ---- | -------- | ------- | ----------- |
| No arguments |      |          |         |             |

**Return**: `String`

### `getTimestamp`

Gets the timestamp for when this response was received.

| Name         | Type | Required | Default | Description |
| ------------ | ---- | -------- | ------- | ----------- |
| No arguments |      |          |         |             |

**Return**: `DateTime`

### `getExecutionTime`

Gets the execution time of the request, in milliseconds.

| Name         | Type | Required | Default | Description |
| ------------ | ---- | -------- | ------- | ----------- |
| No arguments |      |          |         |             |

**Return**: `numeric`

### `json`

Returns the data of the request as deserialized `JSON`.

{% hint style="danger" %}
**Throws**: `DeserializeJsonException` if the response is not `JSON`.
{% endhint %}

| Name         | Type | Required | Default | Description |
| ------------ | ---- | -------- | ------- | ----------- |
| No arguments |      |          |         |             |

**Return**: `any`

### `isSuccess`

Returns true if the request status code is considered successful.

| Name         | Type | Required | Default | Description |
| ------------ | ---- | -------- | ------- | ----------- |
| No arguments |      |          |         |             |

**Return**: `boolean`

### `isOK`

Returns true if the request status code is `200 OK`.

| Name         | Type | Required | Default | Description |
| ------------ | ---- | -------- | ------- | ----------- |
| No arguments |      |          |         |             |

**Return**: `boolean`

### `isCreated`

Returns true if the request status code is `201 Created`.

| Name         | Type | Required | Default | Description |
| ------------ | ---- | -------- | ------- | ----------- |
| No arguments |      |          |         |             |

**Return**: `boolean`

### `isRedirect`

Returns true if the request status code is considered a redirect.

| Name         | Type | Required | Default | Description |
| ------------ | ---- | -------- | ------- | ----------- |
| No arguments |      |          |         |             |

**Return**: `boolean`

### `isError`

Returns true if the request status code is considered either a client error (4xx status code) or a server error (5xx status code).

| Name         | Type | Required | Default | Description |
| ------------ | ---- | -------- | ------- | ----------- |
| No arguments |      |          |         |             |

**Return**: `boolean`

### `isClientError`

Returns true if the request status code is considered a client error (4xx status code).

| Name         | Type | Required | Default | Description |
| ------------ | ---- | -------- | ------- | ----------- |
| No arguments |      |          |         |             |

**Return**: `boolean`

### `isUnauthorized`

Returns true if the request status code is `401 Unauthorized`.

| Name         | Type | Required | Default | Description |
| ------------ | ---- | -------- | ------- | ----------- |
| No arguments |      |          |         |             |

**Return**: `boolean`

### `isForbidden`

Returns true if the request status code is `403 Forbidden`.

| Name         | Type | Required | Default | Description |
| ------------ | ---- | -------- | ------- | ----------- |
| No arguments |      |          |         |             |

**Return**: `boolean`

### `isNotFound`

Returns true if the request status code is `404 Not Found`.

| Name         | Type | Required | Default | Description |
| ------------ | ---- | -------- | ------- | ----------- |
| No arguments |      |          |         |             |

**Return**: `boolean`

### `isServerError`

Returns true if the request status code is considered a server error (5xx status code).

| Name         | Type | Required | Default | Description |
| ------------ | ---- | -------- | ------- | ----------- |
| No arguments |      |          |         |             |

**Return**: `boolean`

### `hasHeader`

Checks if a header exists in the response.

| Name | Type     | Required | Default | Description                      |
| ---- | -------- | -------- | ------- | -------------------------------- |
| name | `String` | `true`   |         | The name of the header to check. |

**Return**: `boolean`

### `getHeader`

Gets the value of a header from the response.

| Name         | Type     | Required | Default | Description                                       |
| ------------ | -------- | -------- | ------- | ------------------------------------------------- |
| name         | `String` | `true`   |         | The name of the header to retrieve.               |
| defaultValue | `any`    | `false`  | `""`    | The value to return if the header does not exist. |

**Return**: `any`

### `getMemento`

Gets a serializable representation of the response.

| Name         | Type | Required | Default | Description |
| ------------ | ---- | -------- | ------- | ----------- |
| No arguments |      |          |         |             |

**Return**:

```json
{
    "responseID"    : getResponseID(),
    "requestID"     : getRequestID(),
    "statusCode"    : getStatusCode(),
    "statusText"    : getStatusText(),
    "status"        : getStatus(),
    "data"          : getData(),
    "charset"       : getCharset(),
    "headers"       : getHeaders(),
    "timestamp"     : getTimestamp(),
    "executionTime" : getExecutionTime()
}
```
