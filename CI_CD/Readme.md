# Mobile Continuous Integration and Continuous Delivery Guide

## Git branching model

This mobile wiki favors the *Scaled Trunk-Based Development* git branching model as described below.  This is to enable Continuous Integration and by extension Continuous Delivery.

- [Scaled Trunk-Based Development](https://trunkbaseddevelopment.com/#scaled-trunk-based-development)
- [Continuous Integration (CI)](https://trunkbaseddevelopment.com/continuous-integration/)
- [Continuous Delivery (CD)](https://trunkbaseddevelopment.com/continuous-delivery/)

This differs from the conventional [GitFlow](https://nvie.com/posts/a-successful-git-branching-model/) model that favors long-running branches, multiple merges and multiple integrations in branches.  As you can see from the original GitFlow author's new 2020 note of reflection in the [link](https://nvie.com/posts/a-successful-git-branching-model/), even the original author Vincent Driessen himself now recommends a more modern git branching model such as [GitHub Flow](https://guides.github.com/introduction/flow/).

The major differences between the [Scaled Trunk-Based Development](https://trunkbaseddevelopment.com/#scaled-trunk-based-development) and the [GitHub Flow](https://guides.github.com/introduction/flow/) is stated here:

- [Differences between GitHub Flow and Trunk-based Development](https://trunkbaseddevelopment.com/alternative-branching-models/index.html#modern-claimed-high-throughput-branching-models)

The GitHub Flow branching model is lighter than the GitFlow model and provides good improvements over the GitFlow and it is well suited for open-sourced development.  However, the GitHub Flow can still lead to high number of merges and become a barrier to CI and thus CD.  Here is another article that compares the pros and cons of all three models:

- [Git Branching Strategies vs. Trunk-Based Development](https://launchdarkly.com/blog/git-branching-strategies-vs-trunk-based-development/)

I has successfully implemented the [Scaled Trunk-Based Development](https://trunkbaseddevelopment.com/#scaled-trunk-based-development) branching model in several apps thus far.

## Test Driven Development (TDD)

Test Driven Development is one of the important best practices for continuous delivery. TDD is one of those very rare software engineering practices that can make a real difference to the quality of your code. As we know, a defect that can be caught in 5 minutes in the coding phase would take much more times to be detected in the Q/A phrase.  TDD is a iterative and incremental design and development strategy to develop robust code and remove defects in the coding phase. If you are an agile software developer, TDD is a best practice you should include in your software development life cycle.

Here is a quick synthesis of TDD:

- [IBM 5-steps of TDD](https://developer.ibm.com/articles/5-steps-of-test-driven-development/)

Here are some videos for some ins and outs on TDD:

- [Test Driven Development - What? Why? And How?](https://www.youtube.com/watch?v=llaUBH5oayw)
- [Test Driven Development Tutorial For Beginners](https://www.youtube.com/watch?v=yfP_v6qCdcs&t=179s)
- [When Test Driven Development Goes Wrong](https://www.youtube.com/watch?v=UWtEVKVPBQ0)

**In this author's opinion, it is highly recommended that TDD is utilized in any software development best practices.**

## Continuous Integration (CI)

This mobile wiki promotes the following CI practices:

- Unit tests are performed prior to commit via [Jest](https://jestjs.io).
- Mandatory code review is performed in pull request when merging a short-lived branch into the main trunk.
- Code quality analysis is performed during integration via coverage analysis tool such as [SonarQube](https://www.sonarqube.org).
- Integration sanity and regression tests can be performed on release builds in a release branch off the main trunk.
- [FastLane CLI](../Fastlane/Readme.md) can then used to deploy beta to iOS TestFlight and Android Beta.
- QA release tests can be performed on iOS TestFlight and Android Beta releases or other QA release CI pipeline.

## Continuous Delivery (CD)

This mobile wiki promotes continuous delivery on a per sprint or every 2-3 weeks basis:

- New major or maintenance release versions are released via iOS TestFlight and Android Beta program.
- New minor releases can be released vis [App Center Code Push](../AppCenter/Readme.md) or via iOS TestFlight and Android Beta program.
