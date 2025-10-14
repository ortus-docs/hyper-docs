# Installation

Hyper is most easily installed via ForgeBox and CommandBox.

```sh
box install hyper
```

If you install Hyper in a non-ColdBox application, make sure to create a mapping in your `Application.cfc`

```cfscript
this.mappings[ "/hyper" ] = expandPath( "/modules/hyper" );
```
