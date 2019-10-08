Salesforce hosts an internal NPM registry which also proxies to the public NPM registry. Some projects are only published on the internal NPM. Follow the steps to setup access:

### 1) Configure access to git.soma.salesforce.com

[Set up SSH access to git.soma.salesforce.com][setup-github-ssh] if you haven't done so already.

### 2) Configure access to internal Nexus

[https://git.soma.salesforce.com/modularization-team/maven-settings][maven-settings]

If you get a `sun.security.validator.ValidatorException` exception, then you
will need to [add a trusted certificate authority to Java][how-to-add-cert].

### 3) Configure access to internal NPM registry

[https://sfdc.co/npm-nexus](https://sfdc.co/npm-nexus)

[how-to-add-cert]: https://sites.google.com/a/salesforce.com/security/services/requests/new-certificate-and-certificate-renewal-requests/creating-or-revoking-an-internal-certificate/internal-root-certificate-information/adding-a-trusted-certificate-authority/how-to-add-a-trusted-certificate-authority-to-java
[setup-github-ssh]: https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/
[maven-settings]: https://git.soma.salesforce.com/modularization-team/maven-settings