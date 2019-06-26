# Maven

### snapshot versions Vs release versions
The term “SNAPSHOT” means the build is a snapshot of your code at a given time, which means downloading 1.0-SNAPSHOT today might give a different file than downloading it tomorrow or day after. When you are ready to release your project, you will change 1.0-SNAPSHOT to 1.0 in the pom.xml file. The 1.0 is the release version. After release, any new development work will stat using 1.1-SNAPSHOT and so on.
Unlike regular versions, Maven checks for a new SNAPSHOT version in a remote repository at least once a day by default or if you use -U flag to every time you build. A team working on a cash-service module will release SNAPSHOT of its updated code every day to repository – let’s say cash-service:1.0-SNAPSHOT replacing an older cash-service:1.0-SNAPSHOT jar. In case of released versions, if Maven once downloaded the version say cash-service:1.0, it will never try to download a newer 1.0 available in repository. In order to download the updated code, the cash-service version needs to be upgraded to 1.1.
When you release artifacts to nexus, you can have separate snapshotRepository and a repository for the releases.
Need: In large projects, it is not easy to keep communicating these version changes. Using the older versions can cause unforeseen build issues.

### Parent pom vs Corporate pom vs Reactor pom vs Super pom
**Super pom**: parent of all poms, irrespective of inheritance
**Corporate pom**: pom with company specific configuration like repository, plugins etc
**Parent pom**: Common pom inherited by other poms.

**Reactor pom**: The mechanism in Maven that handles multi-module projects is referred to as the reactor. A reactor pom is a pom.xml file you define with , and Maven will read all of these modules and build then in the correct order based on dependencies.


**attached artifact:**
Attached artifacts are additional related artifacts that get installed and deployed along with the “main” (e.g jar, war, or ear) artifact. These are most often, javadocs, sources, resouce bundles, properties files, etc, but can actually be any file.
Attached artifacts automatically share the same groupId, ArtifactId and version as the main artifact but they are distinguished with an additional Classifier field.


**effective-pom:**
When you build a child of parent, Maven will retrieve parent to merge the parent pom with the child pom. You can have a look to the entire pom.xml by running the command mvn help:effective-pom.

### Is inheritance of dependencies a good idea?
A. It is a good idea when you only have say 5-10 sub modules (i.e. child modules). But, if you have 50+ child modules inheriting from the parent dependency management or plugin management will cause a re-release of anything inheriting from it.


### What are the different dependency scopes have you used?
A. compile, provided, test, and import.

**Compile** means that you need the JAR for compiling and running the app. For a web application, as an example, the JAR will be placed in the WEB-INF/lib directory.

**Provided** means that you need the JAR for compiling, but at run time there is already a JAR provided by the environment so you don’t need it packaged with your app. For a web app, this means that the JAR file will not be placed into the WEB-INF/lib directory.

**Test** scope indicates that the dependency is not required for normal use of the application, and is only available for the test compilation and execution phases.

**import** scope is used to aggregate the specified POM with the dependencies in that POM’s “DependencyManagement” section. This scope is only used on a dependency of type pom in the section and available only from Maven version 2.0.9.


### What is the purpose of Maven assembly plugin?
There are 3 steps to create an assembly:

1) choose or write the assembly descriptor files to use like dev-assembly.xml, prod-assembly.xml, etc
2) configure the Assembly Plugin in your project’s pom.xml, and include the above descriptor files
3) run “mvn assembly:single” on your project.