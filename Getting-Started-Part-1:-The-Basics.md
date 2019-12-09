LWR is published on NPM so you don't need to go through Nexus, although not all Salesforce features are publicly available so some optional features may require that. Here are the steps to set that up.

In a new folder, start a new npm project and install the LWR CLI. (We will use yarn for all our examples)

```console
user@sfdc:~/my-app$ yarn init -y
user@sfdc:~/my-app$ yarn add --dev @webruntime/cli

```

Let's also edit our package.json to add a start script to our application:

```json
"scripts": {
  "start": "webruntime run"
}
```

Note: you can choose to install the CLI globally but we will leave that up to you. (And this way we can show you how to add some commands to your application!)

Run your start command:

```console
user@sfdc:~/my-app$ yarn start

```

You should see some output like below:

```console
Error: srcDir does not exist: ./src
```

Oops that's because we forgot to add some information about our application! We have a tool `create-webruntime-app` which can help us create some boilerplate code to get started, but that project isn't currently maintained so we'll just have to do it the old-fashioned way.

Create a directory for your app source - the default is `src`. 

### routes.json

Inside `src` we will first define our routes. Create a `routes.json` file like the following:

```json
[
  {
    "id": "home",
    "name": "home",
    "path": "/",
    "view": "home",
    "isRoot": true,
    "isDefault": true
  }
]
```

We will go into this fle later when we talk more about routing. For now we can see that by running `yarn start` again, we now get:

```console
Error: theme does not exist: ./src/theme.json
```

### theme.json

Every LWR app must contain a theme, this is what will help us define the shape of our SPA. We will talk about theme more in-depth later but for now what we need to know is that a theme contains a reference to a branding file and also defines some theme layouts.

A theme layouts is a view which typically defines a header and a footer, plus a content section which is defined by each route's view.

```json
{
    "name": "my-theme",
    "branding": "branding.json",
    "themeLayouts": {
        "default": {
            "view": "headerAndFooter"
        }
    }
}
```

### branding.json

Let's create a file with a single branding property:

```json
[
    {
        "name": "HeaderColor",
        "tokens": ["--color-header"],
        "value": "#FF5A00"
    }
]
```

Run `yarn start` and see the following console output:

```console
Error: indexHtml does not exist: ./src/index.html
```

### index.html

Your app will obviously need a html document of some sort, so let's create an `index.html` since that's the default:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8" />
    <title>My first LWR app!</title>
    {{ webruntimeInit }}
    {{ webruntimeViews }}
</head>

<body id="main">
    {{ webruntimeApp "main" }}
</body>

</html>
```

Don't worry about the semantics yet - that's the first thing we'll discuss after we get our app up and running!

### Views

Previously we made reference to some views in our routes and our theme layout. **`home`**, **`contact`** and **`headerAndFooter`** For now, we can think of views as pages and all pages need to point to a UI component. Let's create the views in `src/views`:

**views/home.json** 

```json
{
    "name": "home",
    "component": {
        "name": "app/home"
    },
    "themeLayoutType": "default"
}
```

In our home view, we will point to the home component and use the default theme layout we defined in `theme.json`.

**views/headerAndFooter.json** 

```json
{
    "name": "headerAndFooter",
    "component": {
        "name": "app/headerAndFooter"
    }
}
```

Notice that a theme layout view also points to a component except it does not need a `themeLayoutType` because it _is_ a theme layout.

### Components

Our final step is to create the LWC components that power our application. These components are usually placed in `src/modules` so we will do the same! But before creating the components, we need our application to specify where our components live. The LWC convention for doing this is adding an `lwc.config.json` to our package root (adjacent to the `package.json`):

**lwc.config.json**

```json
{
   "modules": ["src/modules"]
}
```

In addition to specifying which components we contain, this config file also defines which components we depend on, but we'll come back to that later when we add some component dependencies.

**src/modules/app/home/home.html**

```html
<template>
  <h1>My first LWR app!</h1>
</template>
```

**src/modules/app/home/home.js**

```js
import { LightningElement } from 'lwc';

export default class Home extends LightningElement {

}
```

**src/modules/app/home/home.css**

```css
h1 {
  color: var(--color-header)
}
```

That's our home component and now we make our theme layout component:

**src/modules/app/headerAndFooter/headerAndFooter.html**

```html
<template>
  <header></header>
  <main>
    <slot></slot>
  </main>
  <footer></footer>
</template>
```

Don't worry about populating the header or footer just yet, but the slot is important, because this is where your view will swap your content when you route from view to view.

**src/modules/app/headerAndFooter/headerAndFooter.js**

```js
import { LightningElement } from 'lwc';

export default class HeaderAndFooter extends LightningElement {

}
```

Ok it looks like we're all set! Our file structure should now look like this:

[[https://git.soma.salesforce.com/communities/webruntime/blob/master/docs/img/file-structure.png|alt=file structure]]

Let's run `yarn start` again and this time we should see something like the following:

```console
Template version key cdaa45cad1
Server up on http://localhost:3000
```

Let's open `http://localhost:3000` in our browser and we should see:

[[https://git.soma.salesforce.com/communities/webruntime/blob/master/docs/img/first-lwr-message.png|alt=first lwr message]]

Beautiful! Let's recap what we did:

1. Created a new project and installed the LWR CLI.
2. Gave our app a `start` command that invokes the LWR CLI to start our app.
3. We created a home route, an associated view and an associated LWC component.
4. We created a theme with a single branding property and a theme layout.

Congratulations! 

----

In [Getting Started Part 2](https://git.soma.salesforce.com/communities/webruntime/wiki/Getting-Started-Part-2:-Routing-and-Layouts) we'll go over theme layouts in a little more detail and we'll add some more functionality to our app.

----