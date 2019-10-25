# What is Lightning Web Runtime?

Lightning Web Runtime is an LWC-first application framework designed for speed and customizability. LWR is built and maintained by Communities and the UI Platform. LWR is formerly known as Talon and Universal Container.

LWR at its simplest is a non-opinionated way to build a SPA (Single Page App) using LWC. Some benefits of LWR right out of the box are:

1. Performance. Our bar is set at sub-second full page loads.
2. Enjoyable local development experience
3. All the power of LWC and the Salesforce platform at your disposal

## Lightning Web Runtime at Salesforce

LWR was first built as a Community runtime replacement for Aura. Communities are simply websites with Salesforce metadata on top. We wanted building a community to be as simple as building a website outside of Salesforce. Although there are some Community concepts present in an LWR app -- like [themes](link here) -- they only serve to give you the full power you need to build real-world web applications and are not necessarily community specific.

### Timeline

- LWR is currently an official open source project. It is used by the Lightning Tooling team in their [LWC Local Development](https://developer.salesforce.com/blogs/2019/10/announcing-lwc-local-development-beta.html) project (Beta).
- Communities is releasing a new LWR app in the form of a new Build-Your-Own Community. This community is customer pilot in 222 and is expected to go GA in 226.
- We plan to announce LWR at TrailheadDX '20.
- LWR is working closely with LWC and UI Platform to standardize the way we build apps at Salesforce, expect some official announcements soon.

### Development Experience

We want building an LWR app to be just as fun and easy as building on other industry-standard frameworks like Ember or Next.js. Although **LWR was conceived with developer experience in mind**, we are still working through what we call the "programmatic experience". What this means for you as a Salesforce developer is that for now you will have to spend an extra 10 minutes of setup time vs having a full out-of-the-box app with one command. In the very near future we plan to have:

- One-line boilerplate code generation à la [`create-react-app`](https://create-react-app.dev/)
- Generation commands in our CLI to add new routes or views
- Tutorials and better documentation on a fancy website

### Is LWR Right For Me?

If you're looking for an enjoyable development experience then LWR is right for you. LWR is still in its early stages though, so there are a few things you need to know:

1. We love LWC, which means including components from other frameworks can be difficult or in some cases impossible.
2. LWR has 3 server runtime implementations: Core, Scone and Node.js. The only one to be deployed to production today is Core. Talk to us about your deployment, we can help.
3. LWR is still very new so if you can't hack us, [join us](Contributing.md)!

If this sounds right for you [let's get started building your first LWR app](getting-started)! (estimated time, 15 minutes!)