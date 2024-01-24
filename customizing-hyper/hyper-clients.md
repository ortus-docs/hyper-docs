# Hyper Clients

Hyper allows you to configure defaults for your requests as custom Hyper Clients. This is particularly useful for reducing boilerplate in your application.

Defaults are set on the `HyperBuilder` instance. The easiest way to do this is to configure it in WireBox. In an `afterAspectsLoad` method, you can get a reference to a `HyperBuilder`, configure it as you would for a request, and then call the `registerAs` method passing in your desired WireBox alias.

```cfscript
// config/WireBox.cfc
component {

   // ...
   
   function afterApsectsLoad() {
       injector.getInstance( "HyperBuilder@hyper" )
           .setBaseUrl( "https://swapi.dev/api" )
           .asJson()
           .registerAs( "StarWarsClient" );
   }

}
```

{% hint style="info" %}
Putting the registration code in `afterAspectsLoad` is required so Hyper can be loaded and available for injection.
{% endhint %}

Now, you can inject this pre-configured builder wherever you need in your application:

```js
component {

    property name="StarWarsClient" inject="StarWarsClient";

    function findUser( id ) {
        return variables.StarWarsClient.get( "/people/#id#" );
    }

}
```

You can alternatively create the clients by passing in the desired defaults to the `initWith` method of a WireBox mapping.  These arguments must match the [`HyperRequest` property names](hyper-clients.md#hyperrequest-property-names).

```js
// config/WireBox.cfc
component {

    function configure() {
        map( "StarWarsClient" )
            .to( "hyper.models.HyperBuilder" )
            .asSingleton()
            .initWith(
                baseUrl = "https://swapi.dev/api"
            );
    }

}
```

You can even create multiple clients using this approach:

```js
// config/WireBox.cfc
component {

    function configure() {
        // ...
    }

    function afterAspectsLoad() {
        injector.getInstance( "HyperBuilder@hyper" )
           .setBaseUrl( "https://swapi.dev/api" )
           .asJson()
           .registerAs( "StarWarsClient" );

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

You can also set or change the defaults by either passing the key / value pairs in to the `init` method or by calling the appropriate `HyperRequest` method on the `HyperBuilder.defaults` property.

```js
var hyper = new Hyper.models.HyperBuilder(
    baseUrl = "https://api.github.com"
);
hyper.defaults.withHeaders( { "Authorization" = token } );
```

#### HyperRequest property names

```cfscript
/**
* The httpClient to use for the request
*/
property name="httpClient";

/**
* The baseURL for the request.
* e.g. https://api.github.com/
*/
property name="baseUrl" default="";

/**
* The URL for the request.
* It can either be a full url
* or a URI resource for use with the baseURL.
* e.g. /repos
*/
property name="url" default="";

/**
* Setting this to true will change all relative urls in the document to absolute.
*/
property name="resolveUrls" default="false";

/**
* Setting this to false will not automatically encode the url passed.
* WARNING: Setting this to false is not supported on Adobe engines.
*/
property name="encodeUrl" default="true";

/**
* The HTTP method for the request.
*/
property name="method" default="GET";

/**
* The username for the request for basic auth.
*/
property name="username" default="";

/**
* The password for the request for basic auth.
*/
property name="password" default="";

/**
* Timeout, in seconds, for the request.
*/
property name="timeout" default="10";

/**
* The maximum number of redirects to follow.
* A value of `*` will follow redirects infinitely.
*/
property name="maximumRedirects" default="*";

/**
* The body to send with the request.
* How the body is serialized is
* determined by the bodyFormat.
*/
property name="body" default="";

/**
* The format to serialize the body.
* e.g. `json` or `formFields`
*/
property name="bodyFormat" default="json";

/**
* The referring response in the case of redirects.
*/
property name="referrer";

/**
* A struct of headers for the request.
*/
property name="headers";

/**
* A struct of query parameters for the request.
*/
property name="queryParams";

/**
* Flag to throw on a cfhttp error.
*/
property name="throwOnError" default="false";

/**
* The full path to a PKCS12 format file that contains the client certificate for the request.
*/
property name="clientCert";

/**
* 	Password used to decrypt the client certificate.
*/
property name="clientCertPassword";

/**
* The domain for the request for NTLM auth.
*/
property name="domain" default="";

/**
* The workstation for the request for NTLM auth.
*/
property name="workstation" default="";

/**
* The authType for the request
*/
property name="authType" default="BASIC";

/**
* An array of callback functions to call
* before firing off a request.
*/
property name="requestCallbacks" type="array";

/**
* An array of callback functions to call
* after receiving a response.
*/
property name="responseCallbacks" type="array";
```

If you need per-request or per-response manipulation of defaults, use the [`requestCallbacks`](../making-requests/hyperrequest.md#withrequestcallback) and [`responseCallbacks`](../making-requests/hyperrequest.md#withresponsecallback) hooks.

```cfscript
map( "ApiClient" )
    .to( "hyper.models.HyperBuilder" )
    .asSingleton()
    .initWith(
        baseUrl = getColdBox().getUtil().getSystemSetting( "API_URL" ),
        requestCallbacks = [
            // provide the current user's token for the request
            function( req ) {
                var auth = getWireBox().getInstance( "AuthenticationService@cbauth" );
                req.withHeaders( "Authorization", auth.user().getApiToken() );
            }
        ],
        responseCallbacks = [
            // map custom `error` property to an exception
            function ( res ) {
                if ( !res.isError() ) {
                    return;
                }
                
                var body = res.json();
                throw(
                    type = "ApiError",
                    message = body.error.message,
                    detail = body.error.code
                );
            }
        ]
    );
```
