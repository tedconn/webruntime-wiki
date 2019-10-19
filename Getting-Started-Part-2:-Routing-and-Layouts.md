In the previous step we created a theme layout with a default slot. Let's add a header with a quick navigation bar to our new app. This will help demonstrate how theme layouts work. Also - there is no need to restart your server when working on LWR, it runs automatically in watch mode. 

**src/modules/app/header/header.html**

```html
<template>
  <nav>
    <ul>
      <li><a href="#">Home</a></li>
      <li><a href="#">Contact</a></li>
    </ul>
 </nav>
</template>
```

Yes, the links won't actually be functional just yet!

**src/modules/app/header/header.js**

```javascript
import { LightningElement } from 'lwc';

export default class Header extends LightningElement {

}
```

**src/modules/app/header/header.css**

```css
ul {
  list-style-type: none;
  margin: 0;
  padding: 0;
  overflow: hidden;
  background-color: #333;
}

li {
  float: left;
}

li a {
  color: #fff;
  display: block;
  text-decoration: none;
  padding: 8px;
  text-align: center;
}

li a:hover {
  background-color: #FF5A00;
}
```

Ok, that will give us a decent looking navigation bar in our header. If we go back to our browser and refresh, you will notice that nothing has changed. That is because we didn't add the header UI module to our markup yet. Let's add it to our lonely theme layout:

**src/modules/app/headerAndFooter/headerAndFooter.html**

```html
<template>
  <header>
    <!-- this is our new ui module -->
    <app-header></app-header>
  </header>
  <main>
    <slot></slot>
  </main>
  <footer></footer>
</template>
```

Take a look at your changes and you should see our header appearing at the top. Ok great, now let's make the header actually functional. In order to demonstrate routing and theme layouts, let's add the following route to our `routes.json`,  so the contact link actually works.

```json
{
  "id": "contact",
  "name": "contact",
  "path": "/contact",
  "view": "view"
}
```

We're also going to need a contact view and corresponding UI module.

> For simple use cases like these, you might think "Why do I need a view, why not just route directly to a ui module?" **And you would be right**. We tend to refer to this as "component routing" and we don't currently support it. It is currently being worked on however, so stay tuned!

Create your contact view:

**src/views/contact.json**

```json
{
  "name": "contact",
  "component": {
    "name": "app/contact"
  },
  "themeLayoutType": "default"
}
```

We want our new contact page to use the `app/contact` component which we are about to create and we want to set the `themeLayoutType` to our only theme layout so that it will also have the same header.

> **Module Namespaces:** When we see a reference to a module like `app/contact` we say that the part before the `/` is the namespace and the part after is the module name. In this case `app` is the module namespace and `contact` is the module name. LWC encourages namespacing by default so as not to pollute the global namespace.

Let's create the contact module:

**src/modules/app/contact/contact.html**

```html
<template>
  <p>Call me: (555) 555-1234</p>
  <a href="mailto:anon@xample.com">Email me</a>
</template>
```

**src/modules/app/contact/contact.js**

```javascript
import { LightningElement } from 'lwc';

export default class Contact extends LightningElement {

}
```

The last thing we have to do is -- you guessed it -- wire up our navigation menu. LWR provides a link component you can use in your application for basic routing. Let's change our header markup to use that:

**src/modules/app/headr/header.html**

```html
<template>
  <nav>
    <ul>
      <li>
        <universal_container-router-link href="/">Home</universal_container-router-link>
      </li>
      <li>
        <universal_container-router-link href="/contact">Contact</universal_container-router-link>
      </li>
    </ul>
 </nav>
</template>
```

Fantastic! If you look at your page you will notice that you can click back and forth between Contact and Home. [What happened to my link styling?](#lightning-web-runtime-is-still-in-alpha)

----

In the next section, we'll expand on some of the concepts above: [Getting Started 2.1: SPA Basics and Programmatic Routing]()

----

### Lightning Web Runtime is still in Alpha

At the time of writing of this page there are a couple of basic things being sorted out:

1. `<universal_container-router-link>` is a temporary name which will change to something like `<lwr-link>` very shortly. Please follow [this issue](https://git.soma.salesforce.com/communities/webruntime/issues/933).

2. **The styles I defined in my header for my `<a>` tag are gone!** Web Components provide native shadow DOM encapsulation. This means that I cannot style an LWC UI module from outside. In our example above we are targeting the `a` element inside `universal_container-router-link` using the `li a` and `li a:hover` selectors from the parent UI module's CSS (header.css). This worked when we had a simple `<a>` in header's markup, but once it became a part of its own UI module, it now belongs to a new shadow root and cannot be styled in the same way.  
This is expected since Web Components give us natural encapsulation via Shadow DOM. It's purposefully difficult to style components from other namespaces. This prevents global styles from leaking into your components or from other components to be able to modify your internal look and feel.  
The answer is for the `<universal_container-router-link>` component to expose some CSS variables we can modify that will allow us to style only the parts of the component the component owner allows. [Issue #933](https://git.soma.salesforce.com/communities/webruntime/issues/933) covers this work in progress as well.