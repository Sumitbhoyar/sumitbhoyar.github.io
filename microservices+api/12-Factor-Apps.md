12-Factor Apps
=============

Popular platform-as-a-service provider Heroku maintains a manifesto of sorts called The Twelve-Factor App. It outlines a methodology for developers to follow when building modern web-based applications.
The 12-factor app methodology specifically created for building **Software as a Service (SaaS)** apps, while avoiding the headaches that has typically bedeviled long-term enterprise software projects.

- **Codebase — One codebase tracked in revision control, many deploys**

A twelve-factor app is always tracked in a version control system.

If there are multiple codebases, it’s not an app – it’s a distributed system. Each component in a distributed system is an app, and each can individually comply with twelve-factor.
Multiple apps sharing the same code is a violation of twelve-factor. The solution here is to factor shared code into libraries which can be included through the dependency manager.

- **Dependencies — Explicitly declare and isolate dependencies.**

All the environments your code runs in need to have some dependencies, like a database, or an image processing library, or a command-line tool. Never let your application assume those things will be in place on a given machine. Ensure it by baking those dependencies into your software system.

You list all the versions of all the libraries you expect to have in place, and when the code is deployed, a command is run to download all the right versions and put them in place. No guesswork, everything as it needs to be.

- **Config — Store config in the environment**

All configuration data should be stored in a separate place from the code, and read in by the code at runtime. Usually this means when you deploy code to an environment, you copy the correct configuration files into the codebase at that time.

- **Backing Services — Treat backing services as attached resources**

Your code will talk to many services, like a database, a cache, an email service, a queueing system, etc. These should all be referenced by a simple endpoint (URL) and maybe a username and password. They might be running on the same machine, or they might be on a different host, in a different datacenter, or managed by a cloud SaaS company. The point is, your code shouldn’t know the difference.

- **Build, release, run — Strictly separate build and run stages**

The process of turning the code into a bundle of scripts, assets and binaries that run the code is the build. 

The release sends that code to a server in a fresh package together. Then the code is run so the application is available on those servers.

The run stage should be simple and bullet-proof so that your team can sleep soundly through the night, knowing that the application is running well, and that if a machine gets restarted (say, a power failure happens) that the app will start up again on launch without the need for human intervention.

- **Processes — Execute the app as one or more stateless processes**

It’s likely you will have your application running on many servers, because that makes it more fault tolerant, and because you can support more traffic. As a rule, you want each of those instances of running code to be stateless. In other words, the state of your system is completely defined by your databases and shared storage, and not by each individual running application instance.

Let’s say you have a signup workflow, where a user has to enter 3 screens of information to create their profile. One (wrong) model would be to store each intermediate state in the running code, and direct the user back to the same server until the signup process is complete. The right approach is to store intermediate data in a database or persistent key-value store, so even if the web server goes down in the middle of the user’s signup, another web server can handle the traffic, and the system is none-the-wiser.

- **Port binding — Export services via port binding**

Just like all the backing services you are consuming, your application also interfaces to the world using a simple URL.

Most runtime frameworks will give you this for free.

- **Concurrency — Scale out via the process model**

When running your code, the idea is that lots of little processes are handling specific needs. So you might have dozens of handlers at the ready to process web requests, and another dozen to handle API calls for your enterprise users. And still another half-dozen processing background welcome-emails going to new users, or sending tweets for your users sharing things on your social media service.

By keeping all these small parts working independently, and running them as separate processes (in a low-level technical sense), your application will scale better. In particular, you’ll be able to do more stuff concurrently, by smoothly adding additional servers, or additional CPU/RAM and taking full advantage of it through the use of more of these small, independent processes.

- **Disposability — Maximize robustness with fast startup and graceful shutdown**

The twelve-factor app’s processes are disposable, meaning they can be started or stopped at a moment’s notice. This facilitates fast elastic scaling, rapid deployment of code or config changes, and robustness of production deploys.

- **Dev/prod parity — Keep development, staging, and production as similar as possible**

- **Logs — Treat logs as event streams**

Logs provide visibility into the behavior of a running app. In server-based environments they are commonly written to a file on disk (a “logfile”); but this is only an output format.

Logs are the stream of aggregated, time-ordered events collected from the output streams of all running processes and backing services.

In an ideal situation, those logs are viewed by developers in their local consoles, and in production they are automatically captured as a stream of events and pushed into a real-time consolidated system for long-term archival and data-mining like Hadoop.

At the very least, you should be capturing errors and sending them to an error reporting service like New Relic or AirBrake. You can take a more general approach and send your logs to a service like PaperTrail or Splunk Storm.

If you are relying on logs as a primary forensic tool, you are probably already missing out on better solutions.

- **Admin processes — Run admin/management tasks as one-off processes**

You’ll want to do lots of one-off administrative tasks once you have a live app. For example, doing data cleanup on bad data you discover; running analytics for a presentation you are putting together, or turning on and off features for A/B testing.

Run one-off admin tasks from an identical environment as production. Don’t run updates directly against a database, don’t run them from a local terminal window.

Having console access to a production system is a critical administrative and debugging tool, and every major language/framework provides it.

**References**:

https://12factor.net/

http://www.clearlytech.com/2014/01/04/12-factor-apps-plain-english/
