
# CI / CD

## Continuous Integration
Continuous integration (CI) is a practice where a team of developers integrate their code early and often to the main branch or code repository.

#### Benefits
- Less bugs get shipped to production as regressions are captured early by the automated tests.
- Building the release is easy as all integration issues have been solved early.
- Less context switching as developers are alerted as soon as they break the build and can work on fixing it before they move to another task.
- Testing costs are reduced drastically – your CI server can run hundreds of tests in the matter of seconds.
- Your QA team spend less time testing and can focus on significant improvements to the quality culture.


#### What you need
- Start writing tests for the critical parts of your codebase.
- Get a CI service to run those tests automatically on every push to the main repository.
- Make sure that your team integrates their changes everyday.
- Fix the build as soon as it’s broken.
- Write tests for every new story that you implement.

#### Automated testing
To get the full benefits of CI, you will need to automate your tests to be able to run them for every change that is made to the main repository.
- Unit tests are narrow in scope and typically verify the behaviour of individual methods or functions.
- Integration tests make sure that multiple components behave correctly together. This can involve several classes as well as testing the integration with other services.
- Acceptance tests are similar to the integration tests but they focus on the business cases rather than the components themselves.
- UI tests will make sure that the application functions correctly from a user perspective.

#### Running your tests automatically
To adopt continuous integration, you will need to run your tests on every change that gets pushed back to the main branch. To do so, you will need to have a service that can monitor your repository and listen to new pushes to the codebase. 

## Continuous delivery
Continuous delivery is an extension of continuous integration to make sure that you can release new changes to your customers quickly in a sustainable way. This means that on top of having automated your testing, you also have automated your release process and you can deploy your application at any point of time by clicking on a button. In theory, with continuous delivery, you can decide to release daily, weekly, fortnightly, or whatever suits your business requirements. However, if you truly want to get the benefits of continuous delivery, you should deploy to production as early as possible to make sure that you release small batches that are easy to troubleshoot in case of a problem.

#### What you need
- You need a strong foundation in continuous integration and your test suite needs to cover enough of your codebase.
- Deployments need to be automated. The trigger is still manual but once a deployment is started there shouldn't be a need for human intervention.
- Your team will most likely need to embrace feature flags so that incomplete features do not affect customers in production.

#### Benefits
- The complexity of deploying software has been taken away. Your team doesn't have to spend days preparing for a release anymore.
- You can release more often, thus accelerating the feedback loop with your customers.
- There is much less pressure on decisions for small changes, hence encouraging iterating faster.

## Continuous deployment
Continuous deployment goes one step further than continuous delivery. With this practice, every change that passes all stages of your production pipeline is released to your customers. There's no human intervention, and only a failed test will prevent a new change to be deployed to production.
Continuous deployment is an excellent way to accelerate the feedback loop with your customers and take pressure off the team as there isn't a Release Day anymore. Developers can focus on building software, and they see their work go live minutes after they've finished working on it.

#### What you need
- Your testing culture needs to be at its best. The quality of your test suite will determine the quality of your releases.
- Your documentation process will need to keep up with the pace of deployments.
- Feature flags become an inherent part of the process of releasing significant changes to make sure you can coordinate with other departments (Support, Marketing, PR...).

#### Benefits
- You can develop faster as there's no need to pause development for releases. Deployments pipelines are triggered automatically for every change.
- Releases are less risky and easier to fix in case of problem as you deploy small batches of changes.
- Customers see a continuous stream of improvements, and quality increases every day, instead of every month, quarter or year.

### How the practices relate to each other
To put it simply continuous integration is part of both continuous delivery and continuous deployment. And continuous deployment is like continuous delivery, except that releases happen automatically.

Reference: https://www.atlassian.com/continuous-delivery/principles/continuous-integration-vs-delivery-vs-deployment