🛠 Under Construction 🛠 

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

Ok, that will give us a decent looking navigation bar in our header. If we go back to our browser and refresh, you will notice that nothing has changed. That is because we didn't add the header component to our markup yet. Let's add it to our lonely theme layout:

**src/modules/app/headerAndFooter/headerAndFooter.html**

```html
<template>
  <header>
    <!-- this is our new component -->
    <app-header></app-header>
  </header>
  <main>
    <slot></slot>
  </main>
  <footer></footer>
</template>
```

Save and refresh your browser - our header appears at the top. Ok great, now let's make the header actually functional. In order to demonstrate routing and theme layouts, let's add the following route to our `routes.json`,  so the contact link actually works.

```json
{
  "id": "contact",
  "name": "contact",
  "path": "/contact",
  "view": "view"
}
```

We're also going to need a contact view and component.

Note: for simple use cases like these, you might think "Why do I need a view, why not just route directly to a component?" And you would be right. We don't currently support basic component routing, but we plan on adding it back and we will dig deeper into the use cases for actually having a view later on. 

**src/views/contact.json**

```json
{
  "name": "contact",
  "component": {
    "name": "app/contact"
  }
  "themeLayoutType": "default"
}
```

We want our new contact page to use the app-contact component which we are about to create and we want to set the `themeLayoutType` to our only theme layout so that it will also have the header.

Let's create the contact component:

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






