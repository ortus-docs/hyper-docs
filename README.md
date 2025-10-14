# Introduction

## A CFML HTTP Builder

### Inspiration

Hyper was built after coding several API SDK's for various platforms — [S3SDK](https://github.com/coldbox-modules/s3sdk), [cbstripe](https://github.com/coldbox-modules/cbox-stripe), and [cbgithub](https://github.com/elpete/cbgithub), to name a few. We noticed that we spent a lot of time setting up the plumbing for the requests and a wrapper around `cfhttp`. Each implementation was mostly the same but slightly different. It was additionally frustrating because we really only needed to tweak a few values, usually just the `Authorization` header. It would be nice to create an HTTP client pre-configured for each of these SDK's. It seemed the perfect fit for a module.

### The problem it solves

Hyper exists to provide a fluent builder experience for HTTP requests and responses. It also provides a powerful way to create clients, i.e. Builder objects with pre-configured defaults like a base URL or certain headers.
