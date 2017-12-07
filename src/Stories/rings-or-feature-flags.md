open source 
# Should we use the ring deployment model, feature flags, or both?

## We evaluated both concepts

Progressive exposure is an important DevOps practice. It allows us to exposure features with only a few users in production, observe and validate, and progressively have more and more users exposed. Two progressive exposure strategies we explored are [feature flags](https://docs.microsoft.com/en-us/vsts/articles/phase-features-with-feature-flags) and [ring-based deployment](https://docs.microsoft.com/en-us/vsts/articles/phase-rollout-with-rings).

Before you invest in either practice, you need to understand the value of both practices. It's also important to realize that both will introduce new complexity and cost to your environment.

**Ring-based deployment** is used to limit impact on end-users, while gradually deploying and validating change in **production**. The impact, "blast radius", is evaluated through observation, testing, diagnosis of telemetry, and most importantly, user feedback. Rings make it possible to have multiple production releases running in parallel. You can gather feedback without being at risk of impacting all users, decommission old releases, and distribute new releases when you are confident that everything is working properly.

The following diagram summarizes our implementation of the ring-based deployment process:

![Ring-based deployment process](_img/rings-or-feature-flags/ring-based-deployment.png)

1. When our developers commit a pull request with proposed changes to the master branch, a continuous integration build performs the build, unit testing, and triggers an automatic release to the Canary environment in production. It's important to emphasize that the canary and other rings are using the same production environment.
2. When we are confident that the release is ready for user acceptance and exploratory testing in production, we approve the release to the Early Adopter ring.
3. Similarly when we are confident that the release is ready for prime time, we approve the release to the Users ring. In an emergency we have the option of [rolling back](https://blogs.msdn.microsoft.com/visualstudioalmrangers/2017/11/02/how-do-i-roll-back-a-vsts-extension-when-i-am-using-a-cicd-pipeline/). Over the past 2.5 years we only had to roll back once, which speaks volume to the value of the ring-based deployment process.

**Feature Flags** are used to **show** or **hide** an encapsulated feature, to deliver a different experience for new versus advanced users, and to support hypothesis-driven development. Using and tying feature flags back to telemetry, allows us to determine if a feature helped to increase user satisfaction, acquisition, and retention. We can also use feature flags to do an emergency roll-back, or hide a feature in a region where it shouldn't be available.

Here's a simple diagram of a feature flag:

![Feature flags](_img/rings-or-feature-flags/feature-flags.png)

1. We're using a software as a service (Saa) feature flag solution. It typically comes as a cost, but abstracts complexity of the flag database, maintenance, and security from our team. Turning a feature on or or is as simple as toggling a radio button. ![Feature flags](_img/rings-or-feature-flags/FF-switch.png)
2. We query the state of the flags at run-time when launching the solution, or if the user opts to configure features.
3. At the code level feature flags are based on the basic if-then-else control flow statement. As shown, if the flag is **true** we send an email, else we print.

**Blue-green** deployment is another practice that you can consider. It's based on two identical production environments. The trusted release is the "green" environment. You expose a new release to the "blue" environment for smoke testing. When you're confident with the new release you swap the environments. We have not evaluated this practice as we favoured one over a number of identical production environments, and we're not confident with the environment "swap".

## Back to the question. One or the other, or both?

You're probably asking yourself whether to use ring-based deployments or feature flags to support progressive exposure in your environment.

> XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
> TBD XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
> XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX

Happy flagging and ringing!

---

Table comparing rings with flags:

|     |DEPLOYMENT RING|FEATURE FLAG|
|-----|---------------|------------|
|Progressive exposure|Yes|Yes|
|A/B Testing|All users within ring|All or selected users within ring|
|Cost|Production environment maintenance|Feature Flag database and code maintenance|
|Primary use|Manage impact "blast radius"|Show or hide features in a release|
|Our blast radius - Canaries|5-20 users|0, all, or specific users|
|Our blast radius - Early Adopters|50-100 users|0, all, or specific users|
|Our blast radius - Users|1000-10000+ users|0, all, or specific users|
