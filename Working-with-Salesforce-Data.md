Wire adapters and components from the `lightning` namespace allow components in Lightning Web Runtime applications to access Salesforce data, see the [Lightning Web Components Dev Guide
](https://developer.salesforce.com/docs/component-library/documentation/lwc/lwc.data).

The Core server runtime include a servlet that will handle UI API calls.

When developping or running off-core, you have the option to proxy UI API calls to a running Core Lightning Web Runtime community instance. When doing so you can also record the API call responses and replay them later for testing purpose.

In the target community in Core you can give the guest user profile CRUD access to any entity.

We use an `Express` middleware to proxy, record and replay API calls, see `packages/@webruntime/compiler/src/api-middleware.js`. The code handles GET calls, assuming the responses are JSON, as well as UI API aggregate-ui POST calls which are handled specifically.

## Proxy API calls to a running Core Lightning Web Runtime community instance

Enable proxying of API calls to a target endpoint by using the `API_ENDPOINT` environment variable:

```bash
API_ENDPOINT=http://main.nrobertde-wsl2.t.force.com:6109/webruntime/s/ yarn start
```

## Record proxied API calls responses

Enable recording of the proxied API calls responses by setting the `RECORD_API_CALLS` environment variable to `true`:

```bash
RECORD_API_CALLS=true API_ENDPOINT=http://main.nrobertde-wsl2.t.force.com:6109/webruntime/s/ yarn start
```

API calls responses will be saved to disk under `<template dir>/api` e.g. `packages/webruntime-template-flashhelp/api`.

## Replay recorded API calls

By default, proxying is disabled and previously recorded API calls are served.

```bash
yarn start
```
