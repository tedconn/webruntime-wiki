LWR is published on NPM so you don't need to go through Nexus, although not all Salesforce features are publicly available so some optional features may require that. Here are the steps to set that up.

In a new folder, start a new npm project and install the LWR CLI. (We will use yarn for all our examples)

```console
user@sfdc:~/my-app$ yarn init -y
user@sfdc:~/my-app$ yarn add --dev @webruntime/cli

```

Let's also edit our package.json to add a start script to our application:

```json
scripts: {
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
  },
  {
    "id": "contact",
    "name": "contact",
    "path": "/contact",
    "view": "contact"
  },
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
    "name": "My Theme",
    "branding": "branding.json",
    "themeLayouts": {
        "default": {
            "view": "headerAndFooter"
        }
    }
}
```
