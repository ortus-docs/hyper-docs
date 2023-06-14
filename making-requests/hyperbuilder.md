# HyperBuilder

A `HyperBuilder` is a singleton factory component that will give you a new [`HyperRequest`](hyperrequest.md) any time you call the `new` method.  It will also create a new [`HyperRequest`](hyperrequest.md) any time you call a method on `HyperBuilder` that exists on [`HyperRequest`](hyperrequest.md).

`HyperBuilder` is the component you want to inject into your singleton components, like handlers or services.  It will ensure you get a fresh [`HyperRequest`](hyperrequest.md) instance on each invocation.  This is important since reusing the same [`HyperRequest`](hyperrequest.md) instance will likely produce unintended results.

You can inject a `HyperBuilder` into your application using the `HyperBuilder@hyper` id.

```cfscript
component {
    
    property name="hyper" inject="HyperBuilder@hyper";

    function index( event, rc, prc ) {
        var reqA = hyper.new();
        // reqA is a new HyperRequest instance.
        
        var reqB = hyper.setUrl( "https://swapi.dev/api/people" );
        // reqB is a new HyperRequest instance with the url set.
    }

}
```

If you are not using ColdBox, you can create a `HyperBuilder` manually:

```cfscript
component {

    function init() {
        variables.hyper = new hyper.models.HyperBuilder();
    }

}
```
