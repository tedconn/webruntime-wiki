# Git and Github Enterprise

We won't spend too much time going over how to use Git, but we will discuss how it will affect us while developing on this off-core repository.

> For a great git resource, please go to [Atlassian's git tutorial site](https://www.atlassian.com/git/tutorials/what-is-git)

## Enable Commit Signing

> **_THIS IS REQUIRED!_**

See [the Salesforce guide on Commit Signing](https://confluence.internal.salesforce.com/pages/viewpage.action?pageId=79771036) to activate your GPG keys and configure your system.

### Commit Signing Tooling

-   [GPG Suite](https://gpgtools.org/) so that you can add your GPG key to your keychain.
-   VSCode supports commit signing with the following setting `"git.enableCommitSigning": true`
