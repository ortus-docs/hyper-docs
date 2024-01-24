# Upgrade Guide

## Upgrading from v6 to v7

### CFHttp HTTP Client

This client now returns more accurate status codes for `502 Bad Gateway` and `408 Request Timeout` responses.

If you were previously checking specifically for `504` status codes for bad hosts, you need to now either check for `502` status codes or use a more general method, like [`isServerError`](making-requests/hyperresponse.md#isservererror) or [`isError`](making-requests/hyperresponse.md#iserror).

If you were previously checking specifically for `504` status codes or [`isServerError`](making-requests/hyperresponse.md#isservererror) for timed out requests, you need to now either check for `408` status codes, [`isClientError`](making-requests/hyperresponse.md#isclienterror), or the more general [`isError`](making-requests/hyperresponse.md#iserror).

## Upgrading from v5 to v6

* The default `Content-Type` header has been removed. You must set this [manually](making-requests/hyperrequest.md#setcontenttype) or use a format helper, such as [`asJson`](making-requests/hyperrequest.md#asjson).
* Dropped support for Adobe 2016.

## Upgrading from v4 to v5

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

## Upgrading from v3 to v4

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

## Upgrading from v2 to v3

Dropped support for ColdBox 5.

## Upgrading from v1 to v2

Dropped support for Lucee 4.5.
