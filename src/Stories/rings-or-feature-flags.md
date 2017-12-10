# Is the relationship between feature flags and the ring deployment model symbiotic?

DevOps enables us to deliver at speed, learn from production feedback, make better decisions, and increase customer satisfaction, acquisition and retention. We need to fail fast on features that result in indifference or negative user experience and focus on features that make a positive difference. **Progressive exposure** is a DevOps practise, based on **feature flags** and **ring-based deployment** that allows us to expose features to selected users in production, to observe and validate, before exposing all users.

You're probably asking yourself whether to use ring-based deployments, or feature flags, or both to support progressive exposure in your environment. Let's start by exploring both strategies.

## Let's understand what feature flags and rings are for

**Feature Flags** - The earliest reference to feature flags we've found comes from [Martin Fowler](https://martinfowler.com/bliki/FeatureToggle.html). Flags decouple deployment and exposure, give run-time control down to the individual user, and enable hypothesis-driven development. Using and tying feature flags back to telemetry, allows you to decide if a feature helped to increase user satisfaction, acquisition, and retention. You can also use feature flags to do an emergency roll-back, hide a feature in a region where it shouldn't be available, or enable telemetry as needed.

![Feature flags](_img/rings-or-feature-flags/FF-switch.png)

A typical feature flag implementation is based on (1) a feature flag implementation service that defines the flag, (2) a run-time query to determine value of the flag, and (3) an if-else programming construct, as shown:

![Feature flags](_img/rings-or-feature-flags/feature-flags.png)

**Ring-based deployment** was first discussed in Jez Humble's book [Continuous Delivery](https://www.continuousdelivery.com/), as Canary-deployments. Rings limit impact on end-users, while gradually deploying and confirming change in **production**. With rings we evaluate the impact, "blast radius", through observation, testing, diagnosis of telemetry, and most importantly, user feedback. Rings make it possible to have multiple production releases running in parallel. You can gather feedback without being at risk of affecting all users, decommission old releases, and distribute new releases when you are confident that everything is working properly.

The following diagram show an implementation of the ring-based deployment process:

![Ring-based deployment process](_img/rings-or-feature-flags/ring-based-deployment.png)

When your developers commit a pull request with proposed changes to the master branch, (1) a continuous integration build performs the build, unit testing, and triggers an automatic release to the Canary environment in production. When you're confident that the release is ready for user acceptance and exploratory testing in production (2) you approve the release to the Early Adopter ring. Similarly when you're confident that the release is ready for prime time, (3) you approve the release to the Users ring. The names and number of rings depends on your preferences, but it's important that all rings are using the same production environment.

Both strategies are invaluable, whether you're working with a part-time community working on open source [extensions](https://aka.ms/vsarsolutions#Extensions) we introduced in [how DevOps eliminates development bottlenecks](https://opensource.com/article/17/11/devops-rangers-transformation), or [moving 65,000 engineers to DevOps](https://aka.ms/devops).

## Back to the question. Should you use the feature flags, or rings, or both?



@@@@@@@@@@@A key advantage of the cloud service is that it provides a continuous feedback loop with our users. Here Buck discusses how we use feature flags to progressively reveal new functionality and to experiment in production.> XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
> TBD XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
> XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX

Happy flagging and ringing!

---

Table comparing rings with flags within the context of our open source [extensions](https://aka.ms/vsarsolutions#Extensions):

|     |DEPLOYMENT RING|FEATURE FLAG|
|-----|---------------|------------|
|Progressive exposure|Yes|Yes|
|A/B Testing|All users within ring|All or selected users within ring|
|Cost|Production environment maintenance|Feature Flag database and code maintenance|
|Primary use|Manage impact "blast radius"|Show or hide features in a release|
|Blast radius - Canaries|0-9 users|0, all, or specific canary users|
|Blast radius - Early Adopters|10-100 users|0, all, or specific early adopter users|
|Blast radius - Users|10000+ of users|0, all, or specific users|