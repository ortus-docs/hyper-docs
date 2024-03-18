# Interceptors

Hyper announces two [interception points through ColdBox](https://coldbox.ortusbooks.com/the-basics/interceptors): `onHyperRequest` and `onHyperResponse`.

### onHyperRequest

This interception point is announced before the request is sent.  It receives the `request` as the only parameter inside `data`.

### onHyperResponse

This interception point is announced after the response is received.  It receives the `response` and the `request` inside `data`.

