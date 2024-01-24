# HyperRequest

Though the [`HyperBuilder`](hyperbuilder.md) is the component you will most likely inject, `HyperRequest` is the component will you interact with the most. `HyperRequest` provides a fluent interface to configure your HTTP call.

```cfscript
hyper.get( "https//api.github.com/users" );

hyper.setMethod( "PUT" )
    .withHeaders( { "Authorization" = "Bearer #token#" } )
    .setUrl( "https://jsonplaceholder.typicode.com/posts/1" )
    .setBody( {
        title: "New Title"
    } )
    .send();
```

## Defaults

The following are default properties for a `HyperRequest`:

```json
{
    "method": "GET"
    "resolveUrls": false,
    "encodeUrl": true,
    "timeout": 10, // in seconds
    "maximumRedirects": "*", // follow redirects indefinitely
    "bodyFormat": "json",
    "throwOnError": false
}
```

## Executing Requests

### `get`

Execute a `GET` request and return a [`HyperResponse`](hyperresponse.md).

| Name        | Type   | Required | Default | Description                                                    |
| ----------- | ------ | -------- | ------- | -------------------------------------------------------------- |
| url         | string | false    | null    | An optional URL to set for the request.                        |
| queryParams | struct | false    | null    | An optional struct of query parameters to set for the request. |

**Return**: [`HyperResponse`](hyperresponse.md)

### `getAsync`

Execute a `GET` request asynchronously. Returns a [ColdBox Future](https://coldbox.ortusbooks.com/digging-deeper/promises-async-programming) that returns a [`HyperResponse`](hyperresponse.md).

<table><thead><tr><th width="40">Name</th><th>Type</th><th>Required</th><th>Default</th><th>Description</th></tr></thead><tbody><tr><td>url</td><td>string</td><td>false</td><td>null</td><td>An optional URL to set for the request.</td></tr><tr><td>queryParams</td><td>struct</td><td>false</td><td>null</td><td>An optional struct of query parameters to set for the request.</td></tr></tbody></table>

**Return**: [`Future`](https://coldbox.ortusbooks.com/digging-deeper/promises-async-programming)`<`[`HyperResponse`](hyperresponse.md)`>`

### `post`

Execute a `POST` request and return a [`HyperResponse`](hyperresponse.md).

| Name | Type   | Required | Default | Description                              |
| ---- | ------ | -------- | ------- | ---------------------------------------- |
| url  | string | false    | null    | An optional URL to set for the request.  |
| body | struct | false    | null    | An optional body to set for the request. |

**Return**: [`HyperResponse`](hyperresponse.md)

### `postAsync`

Execute a `POST` request asynchronously. Returns a [ColdBox Future](https://coldbox.ortusbooks.com/digging-deeper/promises-async-programming) that returns a [`HyperResponse`](hyperresponse.md).

| Name | Type   | Required | Default | Description                              |
| ---- | ------ | -------- | ------- | ---------------------------------------- |
| url  | string | false    | null    | An optional URL to set for the request.  |
| body | struct | false    | null    | An optional body to set for the request. |

**Return**: [`Future`](https://coldbox.ortusbooks.com/digging-deeper/promises-async-programming)`<`[`HyperResponse`](hyperresponse.md)`>`

### `put`

Execute a `PUT` request and return a [`HyperResponse`](hyperresponse.md).

| Name | Type   | Required | Default | Description                              |
| ---- | ------ | -------- | ------- | ---------------------------------------- |
| url  | string | false    | null    | An optional URL to set for the request.  |
| body | struct | false    | null    | An optional body to set for the request. |

**Return**: [`HyperResponse`](hyperresponse.md)

### `putAsync`

Execute a `PUT` request asynchronously. Returns a [ColdBox Future](https://coldbox.ortusbooks.com/digging-deeper/promises-async-programming) that returns a [`HyperResponse`](hyperresponse.md).

| Name | Type   | Required | Default | Description                              |
| ---- | ------ | -------- | ------- | ---------------------------------------- |
| url  | string | false    | null    | An optional URL to set for the request.  |
| body | struct | false    | null    | An optional body to set for the request. |

**Return**: [`Future`](https://coldbox.ortusbooks.com/digging-deeper/promises-async-programming)`<`[`HyperResponse`](hyperresponse.md)`>`

### `patch`

Execute a `PATCH` request and return a [`HyperResponse`](hyperresponse.md).

| Name | Type   | Required | Default | Description                              |
| ---- | ------ | -------- | ------- | ---------------------------------------- |
| url  | string | false    | null    | An optional URL to set for the request.  |
| body | struct | false    | null    | An optional body to set for the request. |

**Return**: [`HyperResponse`](hyperresponse.md)

### `patchAsync`

Execute a `PATCH` request asynchronously. Returns a [ColdBox Future](https://coldbox.ortusbooks.com/digging-deeper/promises-async-programming) that returns a [`HyperResponse`](hyperresponse.md).

| Name | Type   | Required | Default | Description                              |
| ---- | ------ | -------- | ------- | ---------------------------------------- |
| url  | string | false    | null    | An optional URL to set for the request.  |
| body | struct | false    | null    | An optional body to set for the request. |

**Return**: [`Future`](https://coldbox.ortusbooks.com/digging-deeper/promises-async-programming)`<`[`HyperResponse`](hyperresponse.md)`>`

### `delete`

Execute a `DELETE` request and return a [`HyperResponse`](hyperresponse.md).

| Name | Type   | Required | Default | Description                              |
| ---- | ------ | -------- | ------- | ---------------------------------------- |
| url  | string | false    | null    | An optional URL to set for the request.  |
| body | struct | false    | null    | An optional body to set for the request. |

**Return**: [`HyperResponse`](hyperresponse.md)

### `deleteAsync`

Execute a `DELETE` request asynchronously. Returns a [ColdBox Future](https://coldbox.ortusbooks.com/digging-deeper/promises-async-programming) that returns a [`HyperResponse`](hyperresponse.md).

| Name | Type   | Required | Default | Description                              |
| ---- | ------ | -------- | ------- | ---------------------------------------- |
| url  | string | false    | null    | An optional URL to set for the request.  |
| body | struct | false    | null    | An optional body to set for the request. |

**Return**: [`Future`](https://coldbox.ortusbooks.com/digging-deeper/promises-async-programming)`<`[`HyperResponse`](hyperresponse.md)`>`

### `head`

Execute a `HEAD` request and return a [`HyperResponse`](hyperresponse.md).

| Name        | Type   | Required | Default | Description                                                    |
| ----------- | ------ | -------- | ------- | -------------------------------------------------------------- |
| url         | string | false    | null    | An optional URL to set for the request.                        |
| queryParams | struct | false    | null    | An optional struct of query parameters to set for the request. |

**Return**: [`HyperResponse`](hyperresponse.md)

### `headAsync`

Execute a `HEAD` request asynchronously. Returns a [ColdBox Future](https://coldbox.ortusbooks.com/digging-deeper/promises-async-programming) that returns a [`HyperResponse`](hyperresponse.md).

| Name        | Type   | Required | Default | Description                                                    |
| ----------- | ------ | -------- | ------- | -------------------------------------------------------------- |
| url         | string | false    | null    | An optional URL to set for the request.                        |
| queryParams | struct | false    | null    | An optional struct of query parameters to set for the request. |

**Return**: [`Future`](https://coldbox.ortusbooks.com/digging-deeper/promises-async-programming)`<`[`HyperResponse`](hyperresponse.md)`>`

### `options`

Execute an `OPTIONS` request and return a [`HyperResponse`](hyperresponse.md).

| Name        | Type   | Required | Default | Description                                                    |
| ----------- | ------ | -------- | ------- | -------------------------------------------------------------- |
| url         | string | false    | null    | An optional URL to set for the request.                        |
| queryParams | struct | false    | null    | An optional struct of query parameters to set for the request. |

**Return**: [`HyperResponse`](hyperresponse.md)

### `optionsAsync`

Execute an `OPTIONS` request asynchronously. Returns a [ColdBox Future](https://coldbox.ortusbooks.com/digging-deeper/promises-async-programming) that returns a [`HyperResponse`](hyperresponse.md).

| Name        | Type   | Required | Default | Description                                                    |
| ----------- | ------ | -------- | ------- | -------------------------------------------------------------- |
| url         | string | false    | null    | An optional URL to set for the request.                        |
| queryParams | struct | false    | null    | An optional struct of query parameters to set for the request. |

**Return**: [`Future`](https://coldbox.ortusbooks.com/digging-deeper/promises-async-programming)`<`[`HyperResponse`](hyperresponse.md)`>`

### `send`

Send the HTTP request and return a [`HyperResponse`](hyperresponse.md).

| Name         | Type | Required | Default | Description |
| ------------ | ---- | -------- | ------- | ----------- |
| No arguments |      |          |         |             |

**Return**: [`HyperResponse`](hyperresponse.md)

### `sendAsync`

Send the HTTP request asynchronously and return a [ColdBox Future](https://coldbox.ortusbooks.com/digging-deeper/promises-async-programming) that will resolve to a [`HyperResponse`](hyperresponse.md).

| Name         | Type | Required | Default | Description |
| ------------ | ---- | -------- | ------- | ----------- |
| No arguments |      |          |         |             |

**Return**: [`Future`](https://coldbox.ortusbooks.com/digging-deeper/promises-async-programming)`<`[`HyperResponse`](hyperresponse.md)`>`

## Building Requests

### `getRequestId`

Gets the unique request ID representing this request.

| Name         | Type | Required | Default | Description |
| ------------ | ---- | -------- | ------- | ----------- |
| No arguments |      |          |         |             |

**Return**: `String`

### `getFullURL`

Gets the full URL for the request.

| Name            | Type    | Required | Default | Description                                            |
| --------------- | ------- | -------- | ------- | ------------------------------------------------------ |
| withQueryString | boolean | false    | false   | Includes the configured query string with the full URL |

**Return**: `String`

### `getBaseURL`

Gets the base URL for the request. The base URL is combined with the URL when making the request.

| Name         | Type | Required | Default | Description |
| ------------ | ---- | -------- | ------- | ----------- |
| No arguments |      |          |         |             |

**Return**: `String`

### `setBaseURL`

Sets the base URL for the request. The base URL is combined with the URL when making the request.

| Name  | Type   | Required | Default | Description                                                   |
| ----- | ------ | -------- | ------- | ------------------------------------------------------------- |
| value | string | true     |         | The base URL for the request, e.g. `https://api.github.com/`. |

**Return**: `HyperRequest`

### `getURL`

Gets the URL for the request.

| Name         | Type | Required | Default | Description |
| ------------ | ---- | -------- | ------- | ----------- |
| No arguments |      |          |         |             |

**Return**: `String`

### `setURL`

Sets the URL for the request.

| Name  | Type   | Required | Default | Description                                                                                                     |
| ----- | ------ | -------- | ------- | --------------------------------------------------------------------------------------------------------------- |
| value | string | true     |         | The URL for the request. It can either be a full url or a URI resource for use with the baseURL. e.g. `/repos`. |

**Return**: `HyperRequest`

### `setResolveURL`

Sets the resolveURL parameter for the request.

| Name  | Type    | Required | Default | Description                                                                    |
| ----- | ------- | -------- | ------- | ------------------------------------------------------------------------------ |
| value | boolean | false    | false   | Resolves URLs in the response body to absolute URLs, including the port number |

**Return**: `HyperRequest`

### `getMethod`

Gets the HTTP method for the request.

| Name         | Type | Required | Default | Description |
| ------------ | ---- | -------- | ------- | ----------- |
| No arguments |      |          |         |             |

**Return**: `String`

### `setMethod`

Sets the HTTP method for the request.

| Name  | Type   | Required | Default | Description                      |
| ----- | ------ | -------- | ------- | -------------------------------- |
| value | string | true     |         | The HTTP method for the request. |

**Return**: `HyperRequest`

### `withBasicAuth`

Sets the username and password for HTTP Basic Auth.

| Name     | Type   | Required | Default | Description                      |
| -------- | ------ | -------- | ------- | -------------------------------- |
| username | string | true     |         | The username for the basic auth. |
| password | string | true     |         | The password for the basic auth. |

**Return**: `HyperRequest`

### `withCertificateAuth`

Sets the username and password for HTTP Basic Auth.

| Name            | Type   | Required | Default | Description                                              |
| --------------- | ------ | -------- | ------- | -------------------------------------------------------- |
| certificatePath | string | true     |         | The mapped path to the certificate used to authenticate. |
| password        | string | false    |         | The optional password used to decrypt the certificate.   |

**Return**: `HyperRequest`

### `withNTLMAuth`

Sets the username, password, domain and workstation for NTLM Auth.

| Name        | Type   | Required | Default | Description                        |
| ----------- | ------ | -------- | ------- | ---------------------------------- |
| username    | string | true     |         | The username for the NTLM auth.    |
| password    | string | true     |         | The password for the NTLM auth.    |
| domain      | string | true     |         | The domain for the NTLM auth.      |
| workstation | string | true     |         | The workstation for the NTLM auth. |

Workstation can be obtained with `createObject('java','java.net.InetAddress').getLocalHost().getHostName()`

**Return**: `HyperRequest`

### `withRequestCallback`

Schedules a callback to be ran when executing the request.

| Name     | Type     | Required | Default | Description                                     |
| -------- | -------- | -------- | ------- | ----------------------------------------------- |
| callback | function | true     |         | The callback to run when executing the request. |

**Return**: `HyperRequest`

### `withResponseCallback`

Schedules a callback to be ran when receiving the response.

| Name     | Type     | Required | Default | Description                                      |
| -------- | -------- | -------- | ------- | ------------------------------------------------ |
| callback | function | true     |         | The callback to run when receiving the response. |

**Return**: `HyperRequest`

### `getUsername`

Gets the username for the request.

| Name         | Type | Required | Default | Description |
| ------------ | ---- | -------- | ------- | ----------- |
| No arguments |      |          |         |             |

**Return**: `String`

### `setUsername`

Sets the username for the request.

| Name  | Type   | Required | Default | Description                   |
| ----- | ------ | -------- | ------- | ----------------------------- |
| value | string | true     |         | The username for the request. |

**Return**: `HyperRequest`

### `getPassword`

Gets the password for the request.

| Name         | Type | Required | Default | Description |
| ------------ | ---- | -------- | ------- | ----------- |
| No arguments |      |          |         |             |

**Return**: `String`

### `setPassword`

Sets the password for the request.

| Name  | Type   | Required | Default | Description                   |
| ----- | ------ | -------- | ------- | ----------------------------- |
| value | string | true     |         | The password for the request. |

**Return**: `HyperRequest`

### `getTimeout`

Gets the timeout for the request, in seconds.

| Name         | Type | Required | Default | Description |
| ------------ | ---- | -------- | ------- | ----------- |
| No arguments |      |          |         |             |

**Return**: `numeric`

### `setTimeout`

Sets the timeout for the request, in seconds.

| Name  | Type   | Required | Default | Description                              |
| ----- | ------ | -------- | ------- | ---------------------------------------- |
| value | string | true     |         | The timeout for the request, in seconds. |

**Return**: `HyperRequest`

### `withoutRedirecting`

A convenience method to not follow any redirects.

| Name         | Type | Required | Default | Description |
| ------------ | ---- | -------- | ------- | ----------- |
| No arguments |      |          |         |             |

**Return**: `HyperRequest`

### `withoutEncodingUrl`

A convenience method to not encode the url.

{% hint style="warning" %}
**WARNING**: Not supported on Adobe engines.
{% endhint %}

| Name         | Type | Required | Default | Description |
| ------------ | ---- | -------- | ------- | ----------- |
| No arguments |      |          |         |             |

**Return**: `HyperRequest`

### `getMaximumRedirects`

Gets the maximum number of redirects to follow.

| Name         | Type | Required | Default | Description |
| ------------ | ---- | -------- | ------- | ----------- |
| No arguments |      |          |         |             |

**Return**: `numeric | String`

### `setMaximumRedirects`

Sets the maximum number of redirects to follow. A value of `*` will follow redirects infinitely.

| Name  | Type | Required | Default | Description                                |
| ----- | ---- | -------- | ------- | ------------------------------------------ |
| value | any  | true     |         | The maximum number of redirects to follow. |

**Return**: `HyperRequest`

### `getBody`

Gets the body for the request.

| Name         | Type | Required | Default | Description |
| ------------ | ---- | -------- | ------- | ----------- |
| No arguments |      |          |         |             |

**Return**: `any`

### `setBody`

Sets the body for the request. Complex values will be serialized before sending the request.

| Name  | Type | Required | Default | Description               |
| ----- | ---- | -------- | ------- | ------------------------- |
| value | any  | true     |         | The body for the request. |

**Return**: `HyperRequest`

### `hasBody`

Checks if the request has a body.

| Name         | Type | Required | Default | Description |
| ------------ | ---- | -------- | ------- | ----------- |
| No arguments |      |          |         |             |

**Return**: `boolean`

### `getBodyFormat`

Gets the body format for the request.

| Name         | Type | Required | Default | Description |
| ------------ | ---- | -------- | ------- | ----------- |
| No arguments |      |          |         |             |

**Return**: `String`

### `setBodyFormat`

Sets the body format for the request. Recognized values are `formFields`, `json`, or `xml`. It is highly recommended to use `asFormFields`, `asJson`, or `asXML` instead.  If you set this value to a non-recognized value, the body will be passed along as-is to the body of the HTTP request.

| Name  | Type | Required | Default | Description                      |
| ----- | ---- | -------- | ------- | -------------------------------- |
| value | any  | true     |         | The body format for the request. |

**Return**: `HyperRequest`

### `asJson`

A convenience method to set the body format and Content-Type to `json`.

| Name         | Type | Required | Default | Description |
| ------------ | ---- | -------- | ------- | ----------- |
| No arguments |      |          |         |             |

**Return**: `HyperRequest`

### `asFormFields`

A convenience method to set the body format and Content-Type to form fields.

| Name         | Type | Required | Default | Description |
| ------------ | ---- | -------- | ------- | ----------- |
| No arguments |      |          |         |             |

**Return**: `HyperRequest`

### `asXML`

A convenience method to set the body format and Content-Type to `xml`.

| Name         | Type | Required | Default | Description |
| ------------ | ---- | -------- | ------- | ----------- |
| No arguments |      |          |         |             |

**Return**: `HyperRequest`

### `getReferrer`

Gets the referrer for the request, if any.

| Name         | Type | Required | Default | Description |
| ------------ | ---- | -------- | ------- | ----------- |
| No arguments |      |          |         |             |

**Return**: `String`

### `getHeaders`

Gets the headers for the request.

| Name         | Type | Required | Default | Description |
| ------------ | ---- | -------- | ------- | ----------- |
| No arguments |      |          |         |             |

**Return**: `java.util.LinkedHashMap`

### `setHeaders`

Sets the headers for the request.

| Name  | Type   | Required | Default | Description                  |
| ----- | ------ | -------- | ------- | ---------------------------- |
| value | struct | true     |         | The headers for the request. |

**Return**: `HyperRequest`

### `setHeader`

Set a header for the request.

| Name  | Type   | Required | Default | Description              |
| ----- | ------ | -------- | ------- | ------------------------ |
| name  | string | true     |         | The name of the header.  |
| value | string | true     |         | The value of the header. |

**Return**: `HyperRequest`

### `withHeaders`

Add additional headers to the request.

| Name    | Type   | Required | Default | Description                                |
| ------- | ------ | -------- | ------- | ------------------------------------------ |
| headers | struct | true     |         | A struct of headers to add to the request. |

**Return**: `HyperRequest`

### `forwardHeaders`

Adds specified headers to the request if they exist. Usually used in conjunction with the current CFML request headers.

| Name    | Type   | Required | Default                               | Description                                                                           |
| ------- | ------ | -------- | ------------------------------------- | ------------------------------------------------------------------------------------- |
| names   | array  | true     |                                       | An array of header names to add to the request if they exist in the `headers` struct. |
| headers | struct | false    | `getHTTPRequestData( false ).headers` | A struct of headers to inspect.                                                       |

**Return**: `HyperRequest`

### `hasHeader`

Check if the request has a header with the given name.

| Name | Type   | Required | Default | Description                      |
| ---- | ------ | -------- | ------- | -------------------------------- |
| name | string | true     |         | The name of the header to check. |

**Return**: `boolean`

### `getCookies`

Gets the cookies for the request.

| Name         | Type | Required | Default | Description |
| ------------ | ---- | -------- | ------- | ----------- |
| No arguments |      |          |         |             |

**Return**: `struct<ordered>`

### `setCookies`

Sets the cookies for the request.

| Name  | Type   | Required | Default | Description                  |
| ----- | ------ | -------- | ------- | ---------------------------- |
| value | struct | true     |         | The headers for the request. |

**Return**: `HyperRequest`

### `setCookie`

Set a cookie for the request.

| Name  | Type   | Required | Default | Description              |
| ----- | ------ | -------- | ------- | ------------------------ |
| name  | string | true     |         | The name of the header.  |
| value | string | true     |         | The value of the header. |

**Return**: `HyperRequest`

### `withCookies`

Add additional cookies to the request.

| Name    | Type   | Required | Default | Description                                |
| ------- | ------ | -------- | ------- | ------------------------------------------ |
| cookies | struct | true     |         | A struct of headers to add to the request. |

**Return**: `HyperRequest`

### `withCredentials`

Sends all current cookies along with the request.

| Name         | Type | Required | Default | Description |
| ------------ | ---- | -------- | ------- | ----------- |
| No arguments |      |          |         |             |

**Return**: `HyperRequest`

### `hasCookie`

Check if the request has a cookie with the given name.

| Name | Type   | Required | Default | Description                      |
| ---- | ------ | -------- | ------- | -------------------------------- |
| name | string | true     |         | The name of the header to check. |

**Return**: `boolean`

### `setContentType`

A convenience method to set the [`Content-Type` header](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Type).

| Name | Type   | Required | Default | Description                            |
| ---- | ------ | -------- | ------- | -------------------------------------- |
| type | string | true     |         | The Content-Type value for the request |

**Return**: `HyperRequest`

### `setAccept`

A convenience method to set the [`Accept` header](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Accept).

| Name | Type   | Required | Default | Description                      |
| ---- | ------ | -------- | ------- | -------------------------------- |
| type | string | true     |         | The Accept value for the request |

**Return**: `HyperRequest`

### `getQueryParams`

Gets the query parameters for the request.

{% hint style="warning" %}
This method returns an array of param structs that is used under the hood by Hyper. You probably want to use [`getQueryParamByName`](hyperrequest.md#getqueryparambyname) or [`getAllQueryParamsByName`](hyperrequest.md#getallqueryparamsbyname) instead.
{% endhint %}

| Name         | Type | Required | Default | Description |
| ------------ | ---- | -------- | ------- | ----------- |
| No arguments |      |          |         |             |

**Return**: `array<struct<string, any>>`

### `setQueryParams`

Sets the query parameters for the request.

{% hint style="warning" %}
This method accepts an array of param structs that is used under the hood by Hyper. You probably want to use [`withQueryParams`](hyperrequest.md#withqueryparams) or [`appendQueryParams`](hyperrequest.md#appendqueryparams) instead.
{% endhint %}

If needed, param structs have two keys, `name` and `value`.

| Name  | Type  | Required | Default | Description                                                |
| ----- | ----- | -------- | ------- | ---------------------------------------------------------- |
| value | array | true     |         | The query parameters for the as an array of param structs. |

**Return**: `HyperRequest`

### `getQueryParam`

{% hint style="danger" %}
**DEPRECATED:** Use [`getQueryParamByName`](hyperrequest.md#getqueryparambyname)
{% endhint %}

Gets the first value for a certain query parameter. Returns an empty string if the query parameter does not exist.

| Name | Type   | Required | Default | Description                                                  |
| ---- | ------ | -------- | ------- | ------------------------------------------------------------ |
| name | string | true     |         | The name of the query parameter to retrieve the first value. |

**Return**: `any`

### `getQueryParamByName`

Gets the first value for a certian query parameter. Returns an empty string if the query parameter does not exist.

| Name | Type   | Required | Default | Description                                                  |
| ---- | ------ | -------- | ------- | ------------------------------------------------------------ |
| name | string | true     |         | The name of the query parameter to retrieve the first value. |

**Return**: `any`

### `getAllQueryParamsByName`

Get all the values for a certain query parameter. Returns an empty array if the query parameter does not exist.

| Name | Type   | Required | Default | Description                                                    |
| ---- | ------ | -------- | ------- | -------------------------------------------------------------- |
| name | string | true     |         | The name of the query parameter to retrieve all of its values. |

**Return**: `array<any>`

### `setQueryParam`

Set a query parameter for the request.

{% hint style="info" %}
**Note:** This removes all other query params with the same name.
{% endhint %}

| Name  | Type   | Required | Default | Description                       |
| ----- | ------ | -------- | ------- | --------------------------------- |
| name  | string | true     |         | The name of the query parameter.  |
| value | string | true     |         | The value of the query parameter. |

**Return**: `HyperRequest`

### `appendQueryParam`

Append a query parameter for the request.

| Name  | Type   | Required | Default | Description                       |
| ----- | ------ | -------- | ------- | --------------------------------- |
| name  | string | true     |         | The name of the query parameter.  |
| value | string | true     |         | The value of the query parameter. |

**Return**: `HyperRequest`

### `withQueryParams`

Add additional query parameters to the request.&#x20;

{% hint style="info" %}
**Note:** This will remove any values with duplicate keys prior to adding the new struct of params.
{% endhint %}

| Name        | Type   | Required | Default | Description                                         |
| ----------- | ------ | -------- | ------- | --------------------------------------------------- |
| queryParams | struct | true     |         | A struct of query parameters to add to the request. |

**Return**: `HyperRequest`

### `appendQueryParams`

Appends additional query parameters to the request.

| Name        | Type   | Required | Default | Description                                         |
| ----------- | ------ | -------- | ------- | --------------------------------------------------- |
| queryParams | struct | true     |         | A struct of query parameters to add to the request. |

**Return**: `HyperRequest`

### `hasQueryParam`

Check if the request has a query parameter with the given name.

| Name | Type   | Required | Default | Description                               |
| ---- | ------ | -------- | ------- | ----------------------------------------- |
| name | string | true     |         | The name of the query parameter to check. |

**Return**: `boolean`

### `attach`

Attaches a file to the Hyper request. Also sets the Content-Type as `multipart/form-data`. Multiple files can be attached by calling `attach` multiple times before calling a send method.

| Name     | Type   | Required | Default | Description                                       |
| -------- | ------ | -------- | ------- | ------------------------------------------------- |
| name     | string | true     |         | The name of the file being uploaded.              |
| path     | string | true     |         | The absolute path to the file to be uploaded.     |
| mimeType | string | false    |         | An optional mime type to associate with the file. |

**Return**: `HyperRequest`

### `setThrowOnError`

Sets the throw on error property for the request. If true, statuses in the 4xx and 5xx range will be turned in to exceptions.

| Name  | Type    | Required | Default | Description                           |
| ----- | ------- | -------- | ------- | ------------------------------------- |
| value | boolean | true     |         | The value of the throw on error flag. |

**Return**: `HyperRequest`

### `throwErrors`

A convenience method to throw on errors.

| Name         | Type | Required | Default | Description |
| ------------ | ---- | -------- | ------- | ----------- |
| No arguments |      |          |         |             |

**Return**: `HyperRequest`

### `allowErrors`

A convenience method to not throw on errors.

| Name         | Type | Required | Default | Description |
| ------------ | ---- | -------- | ------- | ----------- |
| No arguments |      |          |         |             |

**Return**: `HyperRequest`

### `clone`

Clones the current request into a new HyperRequest.

| Name         | Type | Required | Default | Description |
| ------------ | ---- | -------- | ------- | ----------- |
| No arguments |      |          |         |             |

**Return**: A new `HyperRequest` instance cloned from this one.

### `clear`

Clears the request of any set values, including defaults passed by the builder.

| Name         | Type | Required | Default | Description |
| ------------ | ---- | -------- | ------- | ----------- |
| No arguments |      |          |         |             |

**Return**: `HyperRequest`

### `when`

Helper to conditionally execute a callback for the `HyperRequest`. This method lets you use conditionals without breaking chaining.

| Name            | Type       | Required | Default | Description                                                                                            |
| --------------- | ---------- | -------- | ------- | ------------------------------------------------------------------------------------------------------ |
| condition       | `boolean`  | `true`   |         | The condition to check.                                                                                |
| successCallback | `function` | `true`   |         | The callback to execute if the condition is true. The callback is passed the `HyperRequest` instance.  |
| failureCallback | `function` | `false`  | `null`  | The callback to execute if the condition is false. The callback is passed the `HyperRequest` instance. |

**Return**: `HyperRequest`

### `setProperties`

Quickly set many request properties using a struct. The key should be the name of one of the properties on the request, e.g. `url`, `headers`, `method`, `body`.

| Name       | Type   | Required | Default | Description                                                                                                                                   |
| ---------- | ------ | -------- | ------- | --------------------------------------------------------------------------------------------------------------------------------------------- |
| properties | struct | true     |         | A struct of properties to set. Each property name will be set on the request. Properties that don't exist on the request will throw an error. |

**Return**: `HyperRequest`

### `setHttpClient`

Sets the [HTTP Client](../customizing-hyper/custom-http-clients/) to use for the request. The client should conform to the `HyperHttpClientInterface` (though it does not need to use the `implements` keyword).

| Name       | Type                       | Required | Default | Description                            |
| ---------- | -------------------------- | -------- | ------- | -------------------------------------- |
| httpClient | `HyperHttpClientInterface` | `true`   |         | The httpClient to use for the request. |

**Return**: `HyperRequest`

### `setInterceptorService`

Sets the [ColdBox Interceptor Service](https://coldbox.ortusbooks.com/the-basics/interceptors) to announce request and response interception points. A noop option is provided in the `init` for non-ColdBox usage.

| Name               | Type | Required | Default | Description                                     |
| ------------------ | ---- | -------- | ------- | ----------------------------------------------- |
| interceptorService | any  | `true`   |         | The interceptor service to use for the request. |

**Return**: `HyperRequest`

### `setAsyncManager`

Sets the [ColdBox AsyncManager](https://coldbox.ortusbooks.com/digging-deeper/promises-async-programming) to send requests asynchronously. A noop option is provided in the `init` for non-ColdBox usage.

| Name         | Type | Required | Default | Description                              |
| ------------ | ---- | -------- | ------- | ---------------------------------------- |
| asyncManager | any  | `true`   |         | The asyncManager to use for the request. |

**Return**: `HyperRequest`

### `getMemento`

Returns a struct representing this `HyperRequest`.

| Name         | Type | Required | Default | Description |
| ------------ | ---- | -------- | ------- | ----------- |
| No arguments |      |          |         |             |

**Return**:

```json
{
    "requestID"          : getRequestID(),
    "baseUrl"            : getBaseUrl(),
    "url"                : getUrl(),
    "fullUrl"            : getFullUrl(),
    "method"             : getMethod(),
    "queryParams"        : getQueryParams(),
    "headers"            : getHeaders(),
    "cookies"            : getCookies(),
    "files"              : getFiles(),
    "bodyFormat"         : getBodyFormat(),
    "body"               : getBody(),
    "referrer"           : isNull( variables.referrer ) ? "" : variables.referrer,
    "throwOnError"       : getThrowOnError(),
    "timeout"            : getTimeout(),
    "maximumRedirects"   : getMaximumRedirects(),
    "authType"           : getAuthType(),
    "username"           : getUsername(),
    "password"           : getPassword(),
    "clientCert"         : isNull( variables.clientCert ) ? "" : variables.clientCert,
    "clientCertPassword" : isNull( variables.clientCertPassword ) ? "" : variables.clientCertPassword,
    "domain"             : getDomain(),
    "workstation"        : getWorkstation(),
    "resolveUrls"        : getResolveUrls(),
    "encodeUrl"          : getEncodeUrl()
};
```

### `debug`

Creates a debug representation of the HTTP request for the current HTTP client.

{% hint style="danger" %}
**Throws**: `NoUrlException` when no URL is set.
{% endhint %}

| Name         | Type | Required | Default | Description |
| ------------ | ---- | -------- | ------- | ----------- |
| No arguments |      |          |         |             |

**Return**: Dependent on the configured HTTP Client.  See specific HTTP Client documentation for details.
