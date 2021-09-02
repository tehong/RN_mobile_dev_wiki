# Mobile Continuous Integration and Continuous Delivery Guide

## Git branching model

The mobile project uses the *Scaled Trunk-Based Development* git branching model as described below.  This is to enable Continuous Integration and by extension Continuous Delivery.

- [Scaled Trunk-Based Development](https://trunkbaseddevelopment.com/#scaled-trunk-based-development)
- [Continuous Integration (CI)](https://trunkbaseddevelopment.com/continuous-integration/)
- [Continuous Delivery (CD)](https://trunkbaseddevelopment.com/continuous-delivery/)

This differs from the conventional [GitFlow](https://nvie.com/posts/a-successful-git-branching-model/) model that favors long-running branches, multiple merges and multiple integrations in branches.  As you can see from the original GitFlow author's new 2020 note of reflection in the [link](https://nvie.com/posts/a-successful-git-branching-model/), even the author Vincent Driessen himself now recommends a more modern git branching model such as [GitHub Flow](https://guides.github.com/introduction/flow/).

The major differences between the [Scaled Trunk-Based Development](https://trunkbaseddevelopment.com/#scaled-trunk-based-development) and the [GitHub Flow](https://guides.github.com/introduction/flow/) is stated here:

- [Differences between GitHub Flow and Trunk-based Development](https://trunkbaseddevelopment.com/alternative-branching-models/index.html#modern-claimed-high-throughput-branching-models)

The GitHub Flow branching model is lighter than the GitFlow model and provides good improvements over the GitFlow and it is well suited for open-sourced development.  However, the GitHub Flow can still lead to high number of merges and become a barrier to CI and thus CD.  Here is another article that compares the pros and cons of all three models:

- [Git Branching Strategies vs. Trunk-Based Development](https://launchdarkly.com/blog/git-branching-strategies-vs-trunk-based-development/)

The mobile project has successfully implemented the [Scaled Trunk-Based Development](https://trunkbaseddevelopment.com/#scaled-trunk-based-development) branching model thus far.

## Continuous Integration (CI)

mobile project has the following CI practices:

- Unit tests are performed prior to commit via [Jest](https://jestjs.io).
- Mandatory code review is performed in pull request when merging a short-lived branch into the trunk.
- Code quality analysis is performed during integration via [SonarQube](https://www.sonarqube.org).
- Integration sanity and regression tests are performed on release builds in a release branch.
- [FastLane CLI](../Fastlane/Readme.md) is then used to deploy beta to iOS TestFlight and Android Beta.
- QA release tests are performed on iOS TestFlight and Android Beta releases.

## Continuous Delivery (CD)

- New major or maintenance release versions are released via iOS TestFlight and Android Beta program.
- New minor releases can be released vis [App Center Code Push](../AppCenter/Readme.md) or via iOS TestFlight and Android Beta program.
