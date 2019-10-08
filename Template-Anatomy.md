## Handlebars templates

The [handlebars.js](https://github.com/wycats/handlebars.js) template used to generate the HTML document.

Handlebars variables and functions are available to inject the code needed to initialize and render the Lightning Web Runtime app, see description below.

Here is an example:

`index.html`:

<!-- prettier-ignore -->
```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <title>Red Cross: Disaster Relief</title>
        {{ webruntimeInit }}
        {{ webruntimeViews }}
        
        {{#> mysnippet }}
        {{/ mysnippet }}
    </head>

    <body id="main">
        {{ webruntimeApp "main" }}
    </body>
</html>
```

`partials/mysnippet.html`:

```html
<script type="text/javascript" nonce="{{ sourceNonce }}">
    console.log('This script should NOT be blocked by CSP');
</script>
<link
    rel="stylesheet"
    href="{{ basePath }}/assets/styles/salesforce-lightning-design-system.min.css?{{ versionKey }}"
/>
<link rel="stylesheet" href="{{ basePath }}/assets/styles/styles.css?{{ versionKey }}" />
```

### {{ webruntimeInit }}

This has to appear in the HTML's `head` markup. Generates code that loads and initializes the Lightning Web Runtime framework on the client.

### {{ webruntimeViews }}

This has to appear in the HTML's `head` markup after `{{ init }}`. Generates code that loads the current page views.

### {{ webruntimeApp "main" }}

This has to appear in the HTML's `body` markup. Generates code that renders the app.

### {{#> mysnippet }}{{ mysnippet }}

This is an example of optional partial block, which extends Handlebars.js's [Partial Blocks](https://handlebarsjs.com/partials.html#partial-block).

Partial definitions will be fetch from `partials/`. Partial blocks will share the same context as `index.html`.

### {{ basePath }}

The app base path, used by the framework when navigating and requesting resources.

This can be used to load additional resources from the template.

### {{ versionKey }}

An opaque identifier of the version/state of the app.

This can be added to resource URLs in the template to invalidate cached resources.

### {{ sourceNonce }}

A UUID intended to allow scripts to execute when Content Security Policy is enabled.

This can be added to script tags in the template to allow them to execute. Ex: `<script nonce="{{sourceNonce}}">`.

Content Security Policy is enabled by default. If Content Security Policy is disabled, you don't need to specify the `nonce` attribute.

## webruntime.config.json

Place a `webruntime.config.json` in your template directory to configure the Lightning Web Runtime runtime.

Note that this file will be ignored when deployed to Salesforce.

Here is an example of a `webruntime.config.json` file, see below for the description of the available configuration properties.

```json
{
    "includeLwcModules": ["x/myLibary"],
    "rollup": {
        "external": ["lodash", "jquery"],
        "output": {
            "globals": {
                "lodash": "_"
            }
        },
        "plugins": ["resolveable/CustomRollupPlugin"]
    }
}
```

### includeLwcModules

An array of LWC module identifiers that will be sent as part of the HTML.

This is useful if you're reusing some big component or library in multiple routes and allows for the module to only be downloaded once. LWC modules in `includeLwcModules` will be included in the generated views as AMD module dependencies.

A side effect is that the module will also only be instantiated once, where there would be multiple instances of it if it were included in individual routes.

### rollup.external

An array of module identifiers that will be treated as external when compiling the views.

You are responsible for adding the external modules to the Lightning Web Runtime module registry by calling `Webruntime.moduleRegistry.define(name, dependencies, exporter)` before the view modules are evaluated.

This property is similar to [Rollup's](https://rollupjs.org/guide/en#core-functionality) `external` option.

### rollup.output.globals

A map keyed by module identifiers with global variable names as values.

Module specified in this mapping will be treated as external and read from the global `window` object using the specified variable names.

This property is similar to [Rollup's](https://rollupjs.org/guide/en#core-functionality) `output.globals` option.

#### rollup.plugins

An array of rollup plugins that will be resolved by `require`.

The plugin should define `module.exports = function` where the function is invoked with no arguments and will return a [Rollup plugin object](https://rollupjs.org/guide/en#plugins)

Here is an example of a plugin:

```javascript
function myCustomRollupPlugin(/* no arguments are passed in */) {
    return {
        // return a well-formed Rollup plugin object
        // https://rollupjs.org/guide/en

        name: 'myCustomRollupPlugin',
        resolveId(id) {
            // if this plugin handles / resolves "id"
            // return a non-null value
            if (id) {
                return id;
            }
            return null;
        },
        load(id) {
            // if this plugin can load the source file
            // return either the path to the file or the source contents of it
            if (id) {
                return `/custom/location/of/${id}`;
            }
            return null;
        },
        // full list of Rollup hooks -
        // https://rollupjs.org/guide/en#hooks
    };
}

module.exports = myCustomRollupPlugin;
```
