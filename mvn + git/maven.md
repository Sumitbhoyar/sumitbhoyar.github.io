
# Maven

### snapshot versions Vs release versions
The term “SNAPSHOT” means the build is a snapshot of your code at a given time, which means downloading 1.0-SNAPSHOT today might give a different file than downloading it tomorrow or day after. When you are ready to release your project, you will change 1.0-SNAPSHOT to 1.0 in the pom.xml file. The 1.0 is the release version. After release, any new development work will stat using 1.1-SNAPSHOT and so on.

Unlike regular versions, Maven checks for a new SNAPSHOT version in a remote repository at least once a day by default or if you use -U flag to every time you build. A team working on a cash-service module will release SNAPSHOT of its updated code every day to repository – let’s say cash-service:1.0-SNAPSHOT replacing an older cash-service:1.0-SNAPSHOT jar. In case of released versions, if Maven once downloaded the version say cash-service:1.0, it will never try to download a newer 1.0 available in repository. In order to download the updated code, the cash-service version needs to be upgraded to 1.1

When you release artifacts to nexus, you can have separate snapshotRepository and a repository for the releases.
Need: In large projects, it is not easy to keep communicating these version changes. Using the older versions can cause unforeseen build issues.

### Parent pom vs Corporate pom vs Reactor pom vs Super pom
**Super pom**: parent of all poms, irrespective of inheritance

**Corporate pom**: pom with company specific configuration like repository, plugins etc

**Parent pom**: Common pom inherited by other poms.

**Reactor pom**: The mechanism in Maven that handles multi-module projects is referred to as the reactor. A reactor pom is a pom.xml file you define with , and Maven will read all of these modules and build then in the correct order based on dependencies.

**effective-pom:**
When you build a child of parent, Maven will retrieve parent to merge the parent pom with the child pom. You can have a look to the entire pom.xml by running the command mvn help:effective-pom.


### attached artifact:
Attached artifacts are additional related artifacts that get installed and deployed along with the “main” (e.g jar, war, or ear) artifact. These are most often, javadocs, sources, resouce bundles, properties files, etc, but can actually be any file.
Attached artifacts automatically share the same groupId, ArtifactId and version as the main artifact but they are distinguished with an additional Classifier field.


### Is inheritance of dependencies a good idea?
A. It is a good idea when you only have say 5-10 sub modules (i.e. child modules). But, if you have 50+ child modules inheriting from the parent dependency management or plugin management will cause a re-release of anything inheriting from it.


### What is dependency scope? Name all the dependency scope.
Dependency scope includes dependencies as per the current stage of the build. Various Dependency Scopes are −

**compile** − This scope indicates that dependency is available in classpath of project. It is default scope.

**provided** − This scope indicates that dependency is to be provided by JDK or web-Server/Container at runtime.

**runtime** − This scope indicates that dependency is not required for compilation, but is required during execution.

**test** − This scope indicates that the dependency is only available for the test compilation and execution phases.

**system** − This scope indicates that you have to provide the system path.

**import** − This scope is only used when dependency is of type pom. This scope indicates that the specified POM should be replaced with the dependencies in that POM's <dependencyManagement> section.


### What is the purpose of Maven assembly plugin?
The Assembly Plugin for Maven is primarily intended to allow users to aggregate the project output along with its dependencies, modules, site documentation, and other files into a single distributable archive.

Assume that a Maven project defines a single JAR artifact that contains both a console application and a Swing application. Such a project could define two "assemblies" that bundle the application with a different set of supporting scripts and dependency sets. One assembly would be the assembly for the console application, and the other assembly could be a Swing application bundled with a slightly different set of dependencies.

There are 3 steps to create an assembly:

1) choose or write the assembly descriptor files to use like dev-assembly.xml, prod-assembly.xml, etc
2) configure the Assembly Plugin in your project’s pom.xml, and include the above descriptor files
3) run “mvn assembly:single” on your project.

### What are the phases of a Maven Build Lifecycle?
**validate** − validate the project is correct and all necessary information is available.

**compile** − compile the source code of the project.

**test** − test the compiled source code using a suitable unit testing framework. These tests should not require the code be packaged or deployed

**package** − take the compiled code and package it in its distributable format, such as a JAR.

**integration-test** − process and deploy the package if necessary into an environment where integration tests can be run.

**verify** − run any checks to verify the package is valid and meets quality criteria.

**install** − install the package into the local repository, for use as a dependency in other projects locally.

**deploy** − done in an integration or release environment, copies the final package to the remote repository for sharing with other developers and projects.


### What is Build Profile?
A Build profile is a set of configuration values which can be used to set or override default values of Maven build. Using a build profile, you can customize build for different environments such as Production v/s Development environments, To give portability to projects ( e.g. windows, linux etc).

### What is local repository?
Maven local repository is a folder location on your machine. It gets created when you run any maven command for the first time. Maven local repository keeps your project's all dependencies (library jars, plugin jars etc).

### What is Central Repository?
It is repository provided by Maven community. It contains a large number of commonly used libraries.

### What is Remote Repository?
Sometimes, Maven does not find a mentioned dependency in central repository as well then it stops the build process and output error message to console. To prevent such situation, Maven provides concept of Remote Repository which is developer's own custom repository containing required libraries or other project jars.

### What is transitive dependency in Maven?
Transitive dependency means to avoid needing to discover and specify the libraries that your own dependencies require, and including them automatically.


### What is the use of optional dependency?
Any transitive dependency can be marked as optional using "optional" element. As example, A depends upon B and B depends upon C. Now B marked C as optional. Then A will not use C.

### What is difference between Apache Ant and Maven?
Ant is simply a toolbox whereas Maven is about the application of patterns in order to achieve an infrastructure which displays the characteristics of visibility, reusability, maintainability, and comprehensibility. It is wrong to consider Maven as a build tool and just a replacement for Ant.

