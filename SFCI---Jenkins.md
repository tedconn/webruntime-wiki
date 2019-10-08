## Resources

-   [Release jobs](https://sfcirelease.dop.sfdc.net/job/communities/job/communities-talon/job/talon/) - `sfcirelease` Jenkins instance runs all the release jobs, i.e., CI/CD for branches that releases either to Nexus as jars or npm packages. It also handles things like auto-integration and core submissions.

-   [Development jobs](https://communitiesci.dop.sfdc.net/job/communities-managed-pipeline/job/talon/) - `communitiesci` Jenkins instance runs all the non-release jobs, i.e., non-release branches and PRs.

## Where is the `Jenkinsfile` for this repo?

> TL;DR, its at [communities/sfci-pipeline](https://git.soma.salesforce.com/communities/sfci-pipelines).

`Lightning Web Runtime` uses SFCI's [managed pipeline](https://confluence.internal.salesforce.com/pages/releaseview.action?pageId=73513271) for maintainability and scaleability. It allows us to use standard library definitions and lessens the burden on us to maintain our own, unique pipeline.

Source code for this pipeline can be found at [communities/sfci-pipeline](https://git.soma.salesforce.com/communities/sfci-pipelines).

Each branch consuming the managed pipeline will have their own `sfci.yaml` which provides configurability without the need to maintain their respective `Jenkinsfile`.
