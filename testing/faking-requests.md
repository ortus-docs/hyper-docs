# Faking Requests

Hyper has the ability to fake requests and return fake responses as a result.  This is perfect for [testing](https://testbox.ortusbooks.com/) scenarios where you don't actually want to make an HTTP request.

{% hint style="warning" %}
Non-ColdBox users will need to add a mapping to the [`Globber`](https://forgebox.io/view/globber) dependency included with Hyper.

```cfscript
// Application.cfc
component {
    this.mappings[ "/globber" ] = "/path/to/hyper" & "/modules/globber";
}
```
{% endhint %}

## Faking All Requests

Faking is enabled on a [`HyperBuilder`](../making-requests/hyperbuilder.md) instance, either the built-in one provided by Hyper or a [custom Hyper client](../customizing-hyper/custom-http-clients/) you have created.

To enable faking requests, call the `fake` method:

```cfscript
var hyper = new Hyper.models.HyperBuilder();
hyper.fake();
```

After calling the `fake` method, all requests created by this `HyperBuilder` will be faked.  By default, they will return `200 OK` responses with empty bodies.

```cfscript
hyper.fake();
var res = hyper.get( "https://google.com" );
expect( res.getStatus() ).toBe( "200 OK" );
```

## Fake Configuration

When calling the `fake` method, you can provide a struct mapping URL patterns to response generator functions.

```cfscript
hyper.fake( {
    "https://google.com/*": function( newFakeResponse, req ) {
         return newFakeResponse( 404, "Not Found" );
    }
} );
```

The key is a URL pattern.  The pattern can be any valid glob. If the pattern is matched by the [`fullUrl`](../making-requests/hyperrequest.md#getfullurl) of the `HyperRequest`, then the response generator function will be called and the results returned.

A helper function, `newFakeResponse`, is provided as the first argument to the response generator function.  The current request is provided as the second argument.

## FakeHyperResponse

The resposne generator function must return a `FakeHyperResponse` instance.  A `FakeHyperResponse` instance acts similar to a normal `HyperResponse` except the properties are not read only.  Once you have an instance of your `FakeHyperResponse`, you can continue to set any properties you need.

```cfscript
hyper.fake( {
    "https://jsonplaceholder.typicode.com/posts": function( newFakeResponse, req ) {
         return newFakeResponse()
             .setStatusCode( 201 )
             .setStatusText( "Created" )
             .setData( serializeJSON( {
                 "id": 101,
                 "title": "foo",
                 "body": "bar",
                 "userId": 1
             } ) );
    }
} );
```

You can also pass the values to the `newFakeResponse` function, if you'd like.

```cfscript
hyper.fake( {
    "https://jsonplaceholder.typicode.com/posts": function( newFakeResponse, req ) {
         return newFakeResponse( 201, "Created", serializeJSON( {
             "id": 101,
             "title": "foo",
             "body": "bar",
             "userId": 1
         } ) );
    }
} );
```

### `newFakeResponse`

Creates a new `FakeHyperResponse` instance.

<table><thead><tr><th width="160">Name</th><th>Type</th><th>Required</th><th>Default</th><th>Description</th></tr></thead><tbody><tr><td>statusCode</td><td><code>numeric</code></td><td><code>false</code></td><td>200</td><td>The status code for the fake response.</td></tr><tr><td>statusText</td><td><code>string</code></td><td><code>false</code></td><td><code>"OK"</code></td><td>The status text for the fake response.</td></tr><tr><td>data</td><td><code>string</code></td><td><code>false</code></td><td><code>""</code></td><td>The data for the fake response.</td></tr><tr><td>headers</td><td><code>{ string: string }</code></td><td><code>false</code></td><td><code>{}</code></td><td>The headers for the fake response.</td></tr><tr><td>executionTime</td><td><code>numeric</code></td><td><code>false</code></td><td>0</td><td>The execution time for the fake response.</td></tr><tr><td>charset</td><td><code>string</code></td><td><code>false</code></td><td><code>"UTF-8"</code></td><td>The charset for the fake response.</td></tr><tr><td>timestamp</td><td><code>datetime</code></td><td><code>false</code></td><td><code>now()</code></td><td>The timestamp of the fake response.</td></tr></tbody></table>

**Return**: `FakeHyperResponse`

## Sequencing Fake Responses

In addition to returning a single `FakeHyperResponse` per pattern, you can return an array of `FakeHyperResponse` instances.  These will be returned in a sequence.

```cfscript
hyper.fake( {
    "https://jsonplaceholder.typicode.com/posts": function( newFakeResponse, req ) {
         return [
             newFakeResponse( 201, "Created", serializeJSON( {
                 "id": 101,
                 "title": "foo",
                 "body": "bar",
                 "userId": 1
             } ) ),
             newFakeResponse( 422, "Unprocessable Entity", "Duplicate title" )
         ];
    }
} );

var resA = hyper.post( "https://jsonplaceholder.typicode.com/posts", { /* ... */ } );
expect( resA.getStatus() ).toBe( "201 Created" );

var resB = hyper.post( "https://jsonplaceholder.typicode.com/posts", { /* ... */ } );
expect( resA.getStatus() ).toBe( "422 Unprocessable Entity" );
```

If you continue to make requests to the same pattern after the sequence has been exhausted, an exception will be thrown.

```cfscript
hyper.fake( {
    "https://jsonplaceholder.typicode.com/posts": function( newFakeResponse, req ) {
         return [
             newFakeResponse( 201, "Created", serializeJSON( {
                 "id": 101,
                 "title": "foo",
                 "body": "bar",
                 "userId": 1
             } ) ),
             newFakeResponse( 422, "Unprocessable Entity", "Duplicate title" )
         ];
    }
} );

var resA = hyper.post( "https://jsonplaceholder.typicode.com/posts", { /* ... */ } );
expect( resA.getStatus() ).toBe( "201 Created" );

var resB = hyper.post( "https://jsonplaceholder.typicode.com/posts", { /* ... */ } );
expect( resA.getStatus() ).toBe( "422 Unprocessable Entity" );

// THROWS a `HyperFakeSequenceExhausted` exception
var resC = hyper.post( "https://jsonplaceholder.typicode.com/posts", { /* ... */ } );
```

## Preventing Stray Requests

By default, Hyper returns a default `FakeHyperResponse` for every request that doesn't match one of your configured patterns.  You can instead cause Hyper to throw an exception if it encounters one of these stray requests by calling the `preventStrayRequests` method.

```cfscript
hyper.fake( {
    "https://google.com/*": function( newFakeResponse, req ) {
         return newFakeResponse( 404, "Not Found" );
    }
} ).preventStrayRequests();

// THROWS a `HyperFakeStrayRequest` exception
var res = hyper.get( "https://github.com" );
```

## Making Assertions

In addition to assertions made against the `FakeHyperResponse` instances returned, you can also make assertions using the `HyperBuilder` instance you faked.  These come in the form of methods on the `HyperBuilder` instance as well as custom TestBox Assertions.

### HyperBuilder Method Assertions

The following methods are available to make assertions in your tests about the requests that were sent.

#### getFakeRequestCount

Returns the number of fake requests that have been made.

| Name         | Type | Required | Default | Description |
| ------------ | ---- | -------- | ------- | ----------- |
| No arguments |      |          |         |             |

**Return**: `numeric`

#### wasRequestSent

Returns whether a request has been made that matches the `predicate`. Each request that has been made is passed to the `predicate` in order. If the `predicate` returns `true`, the request is considered a match and `true` is returned. If no request passes the `predicate`, `false` is returned.

| Name      | Type       | Required | Default | Description                                                                                            |
| --------- | ---------- | -------- | ------- | ------------------------------------------------------------------------------------------------------ |
| predicate | `function` | `true`   |         | A callback function that returns true if the request matches the criteria and returns false otherwise. |

**Return**: `boolean`

### Custom TestBox Assertions

You can register [custom TestBox assertions](https://testbox.ortusbooks.com/in-depth/expectations/custom-matchers) provided by Hyper for more readable tests and test failure messages.

You must [register](https://testbox.ortusbooks.com/in-depth/expectations/custom-matchers#cfc-matchers) these assertions before using them.

```cfscript
component extends="testbox.system.BaseSpec" {

    function beforeAll() {
        addMatchers( "hyper.models.TestBoxMatchers" )
    }
    
    function run() {
        // ...
    }

}
```

The following custom assertions are provided:

#### toHaveSentRequest

This takes in the `HyperBuilder` instance as the actual and a predicate function as the expected. The predicate function is passed to the `HyperBuilder` instance's `wasRequestSent` method.

```cfscript
hyper.fake();

hyper.get( "https://google.com" );

expect( hyper ).toHaveSentRequest( function( req ) {
    return req.getFullUrl( "https://google.com" );
} );

expect( hyper ).notToHaveSentRequest( function( req ) {
    return req.getFullUrl( "https://github.com" );
} );
```

#### toHaveSentCount

This takes in the `HyperBuilder` instance as the actual and an integer number of requests that should have been sent.

```cfscript
hyper.fake();

hyper.get( "https://google.com" );

expect( hyper ).toHaveSentCount( 1 );
expect( hyper ).notToHaveSentCount( 2 );
```

#### toHaveSentNothing

This takes in the `HyperBuilder` instance as the actual and no other parameters.

```cfscript
hyper.fake();

expect( hyper ).toHaveSentNothing();

hyper.get( "https://google.com" );

expect( hyper ).notToHaveSentNothing();
```

## Resetting the Builder

To reset the `HyperBuilder` instance to normal operation call the `clearFakes` method:

```cfscript
hyper.fake();

hyper.get( "https://google.com" );

hyper.clearFakes();
```

{% hint style="info" %}
This is a useful method to call in an [`afterEach`](https://testbox.ortusbooks.com/in-depth/life-cycle-methods/bdd#aftereach-body-data) block in TestBox to make sure you are only faking requests when you want to.
{% endhint %}
