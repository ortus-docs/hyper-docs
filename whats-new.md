# What's New?

## 7.2.0

### Cookies

Hyper can now [send cookies with a request](making-requests/hyperrequest.md#withcookies) and [parse the returned cookies from a response](making-requests/hyperresponse.md#getcookies). See the [HyperRequest](making-requests/hyperrequest.md) and [HyperResponse](making-requests/hyperresponse.md) docs for details.

## 7.1.0

### Fake Requests

Hyper now has the ability to fake requests and return fake responses as a result.  This is perfect for testing scenarios where you don't actually want to make an HTTP request.

{% content-ref url="testing/faking-requests.md" %}
[faking-requests.md](testing/faking-requests.md)
{% endcontent-ref %}

### Custom Hyper Clients

It is now more straightforward to register a [custom Hyper client](customizing-hyper/custom-http-clients/).  Inside your `config/WireBox.cfc` in an `afterAspectsLoad` method, you can get a reference to a `HyperBuilder`, configure it as you would for a request, and then call the `registerAs` method passing in your desired WireBox alias.

```cfscript
// config/WireBox.cfc
component {

   // ...
   
   function afterApsectsLoad() {
       injector.getInstance( "HyperBuilder@hyper" )
           .setBaseUrl( "https://api.github.com" )
           .asJson()
           .withHeaders( {
               "Authorization": coldbox.getUtil().getSystemSetting( "GITHUB_TOKEN" )
           } )
           .registerAs( "GitHubClient" );
   }

}
```

This is a welcome improvement as the `init` arguments do not exactly match the method names.  Also, for defaults like `requestCallbacks`, `responseCallbacks`, or even `queryParams`, passing in arrays of functions or arrays or structs is not as straightforward as calling the related methods.  Now, you can use the Hyper methods you are familiar with when registering your custom Hyper clients.

{% hint style="info" %}
Putting the registration code in `afterAspectsLoad` is required so Hyper can be loaded and available for injection.
{% endhint %}

## 7.0.0

### CFHttp HTTP Client

This client now returns more accurate status codes for `502 Bad Gateway` and `408 Request Timeout` responses.

Previously, these responses were returned as `504 Gateway Timeout` responses. Hyper now normalizes the responses from the different CFML engines into a consistent response. `502 Bad Gateway` is returned instead of `504 Gateway Timeout` for invalid hosts. `408 Request Timeout` is returned if the request takes longer than the configured [`timeout`](making-requests/hyperrequest.md#settimeout) value.

### Breaking Changes

If you were previously checking specifically for `504` status codes for bad hosts, you need to now either check for `502` status codes or use a more general method, like [`isServerError`](making-requests/hyperresponse.md#isservererror) or [`isError`](making-requests/hyperresponse.md#iserror).

If you were previously checking specifically for `504` status codes or [`isServerError`](making-requests/hyperresponse.md#isservererror) for timed out requests, you need to now either check for `408` status codes, [`isClientError`](making-requests/hyperresponse.md#isclienterror), or the more general [`isError`](making-requests/hyperresponse.md#iserror).

## 6.1.0

Add [`head`](making-requests/hyperrequest.md#head) and [`options`](making-requests/hyperrequest.md#options) shortcut methods.

## 6.0.0

* Add `xml` support and an `asXML` method to set the body format and `Content-Type` header.
* Add `adobe@2023` to testing matrix.

### Breaking Changes

* Remove default `Content-Type` header. You must set this [manually](making-requests/hyperrequest.md#setcontenttype) or use a format helper, such as [`asJson`](making-requests/hyperrequest.md#asjson).
* Dropped `adobe@2016` support.

## 5.0.1

Correctly handle cases when the `body` is a string and format is `JSON`.

## 5.0.0

Add a `debug` method to see what the HTTP client generates.

### Breaking Changes

`HyperHttpClientInterface` now requires a `debug` method.

```cfscript
/**
 * Return a struct of information showing how the client will execute the HyperRequest.
 * This will be used by a developer to debug any differences between the generated
 * request values and the expected request values.
 *
 * @req     The HyperRequest to debug.
 *
 * @returns A struct of information detailing how the client would execute the HyperRequest.
 */
public struct function debug( required HyperRequest req );
```

## 4.0.3

* Do not prepend the base url when a full url is passed.
* Add `resolveUrls` and `encodeUrl` properties to the [memento](making-requests/hyperrequest.md#getmemento).
* Correctly set the `encodeUrl` property when cloning a request.

## 4.0.2

Update README for builder `initWith` headers losing `Content-Type`.

## 4.0.1

Fix `HyperBuilder` example in the docs.

## 4.0.0

Allow adding multiple query params with the same key.

### Breaking Changes

Previously, query params were stored as a struct.  Some APIs expect multiple values for the same query param name to be passed as separate arguments.  Hyper now stores the query params as an array and provides new methods for interacting with query params:

* [`getQueryParamByName`](making-requests/hyperrequest.md#getqueryparambyname)
* [`getAllQueryParamsByName`](making-requests/hyperrequest.md#getallqueryparamsbyname)
* [`withQueryParams`](making-requests/hyperrequest.md#withqueryparams)
* [`appendQueryParam`](making-requests/hyperrequest.md#appendqueryparam)
* [`appendQueryParams`](making-requests/hyperrequest.md#appendqueryparams)
* [`hasQueryParam`](making-requests/hyperrequest.md#hasqueryparam)

The following methods still exist, but now interact with arrays of query param structs instead of a simple struct.

* [`getQueryParams`](making-requests/hyperrequest.md#getqueryparams)
* [`setQueryParams`](making-requests/hyperrequest.md#setqueryparams)

The following methods have been deprecated:

| Deprecated Method                                                | Replacement Method                                                           |
| ---------------------------------------------------------------- | ---------------------------------------------------------------------------- |
| [`getQueryParam`](making-requests/hyperrequest.md#getqueryparam) | [`getQueryParamByName`](making-requests/hyperrequest.md#getqueryparambyname) |

## 3.6.2

Convert array values correctly when sending form fields

## 3.6.1

Add a workaround for CommandBox not having the `box:asyncManager` injection DSL.

## 3.6.0

Add async requests using ColdBox's [AsyncManager](https://coldbox.ortusbooks.com/digging-deeper/promises-async-programming).

## 3.5.0

* Provide more useful error than cfhttp when [`throwOnErrors`](making-requests/hyperrequest.md#throwerrors) is enabled.
* Provide mementos for [HyperRequest](making-requests/hyperrequest.md#getmemento) and [HyperResponse](making-requests/hyperresponse.md#getmemento) instances.
* Capture [statusText](making-requests/hyperresponse.md#getstatustext) and provide a [status](making-requests/hyperresponse.md#getstatus) convenience string.

## 3.4.2

Add MIT License file

## 3.4.1

Use `processState` over `announce` until CommandBox can update its `interceptorService`.

## 3.4.0

### HyperRequest

* Add [`forwardHeaders`](making-requests/hyperrequest.md#forwardheaders) shortcut method.

### HyperResponse

* Allow for default values in [`getHeader`](making-requests/hyperresponse.md#getheader).
* Add helper methods for checking for specific status codes:
  * [`isOk`](making-requests/hyperresponse.md#isok)
  * [`isUnauthorized`](making-requests/hyperresponse.md#isunauthorized)
  * [`isForbidden`](making-requests/hyperresponse.md#isforbidden)
  * [`isNotFound`](making-requests/hyperresponse.md#isnotfound)

## 3.3.0

Allowing [attaching](making-requests/hyperrequest.md#attach) file uploads.

## 3.2.1

Support WireBox outside of ColdBox.

## 3.2.0

Include response data as detail in `DeserializeJsonException`.

## 3.1.0

* Add [`clone`](making-requests/hyperrequest.md#clone) to quickly copy `HyperRequest` instances.
* Add interceptors and [local](making-requests/hyperrequest.md#withrequestcallback) [callbacks](making-requests/hyperrequest.md#withresponsecallback) for lifecycle events.

## 3.0.0

Add execution time to `HyperResponse` instances.

### Breaking Changes

Dropped support for ColdBox 5.

## 2.3.11

* Add support for [NTLM authentication](making-requests/hyperrequest.md#withntlmauth).
* Include [`getFullURL`](making-requests/hyperrequest.md#getfullurl) method in docs.

## 2.3.10

Fixed typo of `Bulider` to `Builder`.

## 2.3.9

Add [`withoutEncodingUrl`](making-requests/hyperrequest.md#withoutencodingurl) flag.

## 2.3.8

Do not fail fast on cron job actions on CI.

## 2.3.7

Update fetch-depth for tests and release actions on CI.

## 2.3.6

Attempt to skip committing back changes on CI.

## 2.3.5

Add matrix and cron testing on CI.

## 2.3.4

Use better GitHub token on CI

## 2.3.1

Add workaround for `boolean` values in query strings.

## 2.3.0

Add [certificate](making-requests/hyperrequest.md#withcertificateauth) auth.

## 2.2.1

Use the previous host for redirect if redirect does not include a full URL.

## 2.2.0

Add [`resolveUrls`](making-requests/hyperrequest.md#setresolveurl) flag.

## 2.1.1

* Use OpenJDK instead of OracleJDK on CI.
* Store module in [ForgeBox Storage](https://app.gitbook.com/s/zv049Bp1C22bLDcQ1fZC/developing-for-commandbox/commands).

## 2.1.0

Allow for pluggable [HTTP Clients](customizing-hyper/custom-http-clients/) that follow the `HyperHttpClientInterface`. (Clients do not need to use the `implements` keyword.)

## 2.0.2

Avoid double encoding using [`cfhttpparam`](https://cfdocs.org/cfhttpparam).

## 2.0.1

Remove Lucee 4.5 support from docs. (Support was dropped in [v2.0.0](whats-new.md#2.0.0))

## 2.0.0

* Do not include [`username`](making-requests/hyperrequest.md#setusername) and [`password`](making-requests/hyperrequest.md#setpassword) unless they have values.
* Add `adobe@2018` support to CI builds.

### Breaking Changes

Dropped support for `lucee@4.5`.

## 1.15.0

Add [`throwOnError`](making-requests/hyperrequest.md#throwerrors) flag.

## 1.14.5

Use `504 Gateway Timeout` for incomplete responses.

## 1.14.4

Include equal signs in query param values.

## 1.14.0 – 1.0.0

### New Features

* Add [`when`](making-requests/hyperrequest.md#when) helper to execute conditions without breaking chaining.
* Add [`clear`](making-requests/hyperrequest.md#clear) method to reset HyperRequest instances.
* Add configurable [`timeout`](making-requests/hyperrequest.md#settimeout).

### Bug Fixes

* Fix for Lucee 4 compatibility on `LinkedHashMaps` and `keyArray`.
* Preserve case in header names.
* Preserve case for query parameters.
* Serialize both params from the url and set on the `HyperRequest` instance.
* Default to `UTF-8` charset if none is present in the response.
* Fix withHeaders and withQueryParams for Lucee compatibility.
* Only map HyperBuilder as a singleton in WireBox

### Other

* Migrate to [coldbox-modules](https://github.com/coldbox-modules) organization on GitHub.
* Update `box.json` description.
* Enable [CommandBox Semantic Release](https://forgebox.io/view/commandbox-semantic-release) on CI.



