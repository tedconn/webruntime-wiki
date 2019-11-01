# Developing LWC with Eclipse

Welcome back to the world full of build problems. We missed you.

## Configure Eclipse

If your normal workflow is to run `blt --config --eclipse`, you can easily add your new module to your Eclipse workspace for convenience:

1. Open Eclipse using `blt --eclipse`.
1. Go to File -> Import -> Existing Maven Projects.
    >This requires the M2E Plugin: http://www.eclipse.org/m2e/
1. Select the folder with your module, i.e. the location of your local Git repository.
1. Import the project. Expand "Advanced" in "Import Maven Projects" modal and set "Name template:" to `[artifactId]`. Yes, with the brackets.
1. Run the usual BLT commands you would after Eclipse finished building.

## Troubleshooting

#### The container 'Maven Dependencies' references non existing library '/home/USER/.m2/repository/org/auraframework/aura-interfaces/VERSION/aura-interfaces-VERSION.jar

If the previous statement is showing up in Eclipse as a build error, you likely are missing your `~/.m2/settings.xml` file. To fix this, run:

    blt mvn-build:--config

(Source: https://gus.my.salesforce.com/0D5B000000cANxgKAG)

#### Project configurator "io.takari.m2e.incrementalbuild.mojoExecutionConfigurator" required by plugin execution "io.takari.maven.plugins:takari-lifecycle-plugin:1.12.0:export-package (execution: default-export-package, phase: process-classes)" is not available.

If the previous statement is showing up in Eclipse as a build error, or you are getting a timeout because you are attempting to use the Eclipse quick fix option to install Takari lifecycle connectors, do the following:
1. Install the latest [M2E plugins](http://download.eclipse.org/technology/m2e/releases) using Eclipse | Help | Install new software
    - Make sure "Show only the latest versions of available software" is selected
1. Install the latest M2E takari lifecycle support plugins from Nexus using Eclipse | Help | Install new software, and entering the following:  https://nexus.soma.salesforce.com/nexus/content/sites/eclipse-p2/cbx/takari-lifecycle-m2e/LATEST/
    - Make sure "Show only the latest versions of available software" is selected
    - Make sure "Contact all update sites during install to find required software" is NOT selected
1. Import maven projects into your workspace

(Source: https://gus.lightning.force.com/lightning/r/0D5B000000nVbixKAC/view)

## Intellij Development

:wrench: In progress :wrench: