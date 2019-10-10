Modules scoped with `@salesforce` add functionality to Lightning web components at runtime. See [@salesforce Modules](https://developer.salesforce.com/docs/component-library/documentation/lwc/reference_salesforce_modules) in the Lightning Web Components Dev Guide for details.

The following section lists the scoped modules that Lightning Web Runtime supports.

## @salesforce/apex

`@salesforce/apex` allows access to server-side Apex controllers by their namespace, controller, and method names.

See [Call Apex Methods](https://developer.salesforce.com/docs/component-library/documentation/lwc/lwc.apex) for details and example code.

In Lightning Web Runtime, `@salesforce/apex` imports will add a `force/lds` dependency to your component via [a Rollup plugin](../packages/@webruntime/compiler/src/compiler/rollup-plugin-salesforce-resource-url.ts) in order to allow @wire functionality.

Off-core Apex will only work when [API calls are proxied to a core community instance.](https://git.soma.salesforce.com/communities/talon/blob/master/docs/WorkingWithSalesforceData.md#proxy-api-calls-to-a-running-core-talon-community-instance)

## @salesforce/client

`@salesforce/client` is meant to provide information about your client environment. This module currently only returns `formFactor` which will always be `large` until we support mobile. The underlying implementation is read from the `configProvider`.

## @salesforce/contentAssetUrl

`@salesforce/contentAssetUrl` brings access to the URLs of asset files (See [ContentAsset object](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_contentasset.htm)) by their asset names.

See [Access Content Asset Files](https://developer.salesforce.com/docs/component-library/documentation/lwc/create_content_assets) in the Lightning Web Components Dev Guide for details and example code.

In Lightning Web Runtime, the `@salesforce/contentAssetUrl` imports are resolved at compile time by [a Rollup plugin](../packages/@webruntime/compiler/src/compiler/rollup-plugin-salesforce-resource-url.ts) and the corresponding URLs included in the generated JavaScript resource along with the component code.

The generated URLs are in the form `/assets/${versionKey}/${resourceName}`.

The [server runtime](../packages/@webruntime/compiler/src/server/server.js) will read the static resource files from the `${outputDir}/public/assets` directory.

## @salesforce/label

`@salesforce/label` allows to access to labels from within LWC components.

See [Access Labels](https://developer.salesforce.com/docs/component-library/documentation/lwc/lwc.create_labels) in the Lightning Web Components Dev Guide for details and example code.

A labels.json file can be passed to the CLI or configuration. The file should have this format:

```json
{
    "Global_Address": {
        "email": "Email"
    }
}
```

A javascript object with the same structure may also be passed directly to ContextService#startContext programmatically.

## @salesforce/resourceUrl

`@salesforce/resourceUrl` allows to access Salesforce Static Resources URLs from within LWC components.

See [Access Static Resources](https://developer.salesforce.com/docs/component-library/documentation/lwc/lwc.create_resources) in the Lightning Web Components Dev Guide for details and example code.

In Lightning Web Runtime, the `@salesforce/resourceUrl` imports are resolved at compile time by [a Rollup plugin](../packages/@webruntime/compiler/src/compiler/rollup-plugin-resource-url.js) and the corresponding URLs included in the generated JavaScript resource along with the component code.

The generated URLs are in the form `/assets/${versionKey}/${resourceName}`.

The [server runtime](../packages/@webruntime/compiler/src/server/server.js) will read the static resource files from the `${outputDir}/public/assets` directory.

## @salesforce/schema

`@salesforce/schema` provides access to an organization’s objects and fields API names for usage in e.g. wire adapters. It's needed to ensure that objects and fields exist, preventing objects and fields from being deleted, and cascading any renamed objects and fields into your component's source code.

See [Import References to Salesforce Objects and Fields](https://developer.salesforce.com/docs/component-library/documentation/lwc/lwc.data_wire_service_about) in the Lightning Web components Dev Guide
for details and code examples.

## @salesforce/user

`@salesforce/user` brings access to the context users id and whether or not the user is guest or not.

See [Get the Current User's ID](https://developer.salesforce.com/docs/component-library/documentation/lwc/get_current_user) in the Lightning Web Components Dev Guide for details and example code.

The users guest status is accessed in the same way as the user's id. If the user is guest the id of the user will be falsy. Lightning Web Component Dev Guide will have more information in the future.
