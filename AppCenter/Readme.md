# Mobile App Center Developer Guide

## App Center CLI

You will need to install app center cli as a global yarn packages in your mac

```
yarn global add appcenter-cli
```

## CodePush

Codepush documentations:

- [App Center CodePush](https://docs.microsoft.com/en-us/appcenter/distribution/codepush/)
- [App Center CLI](https://docs.microsoft.com/en-us/appcenter/cli/)
- [React Native CodePush on Github](https://github.com/Microsoft/react-native-code-push)

### Purpose

Codepush is used to deploy React Native Javascript only changes to the already deployed App store and Google store apps without going through the App store and Google play store release processes. Thus CodePush is **NOT** for any native changes or changes resulted from adding/changing NPM packages in the package.json.

### Release and CodePush Versions

The mobile release versioning have the following convention:

`major.minor.maintenance/patch` (e.g. 3.90.101)

There is also a separate build number in the form of multiple numbers, such as `2489`

These are the version management convention for mobile app:

#### App store and Google play store releases

- version format is `x.y.0`, where x is the major release number and y is the minor release number.
  - **Maintenance/patch version number is always 0 and is reserved for non-native Javascript change release only.**
  - Stores' releases are only due to native changes, that is, any native changes (new NPM package updates, iOS or Android code changes) will trigger a new store release.
- build number is incremented for the App store or Google play store releases.
- These changes happens in *Info.plist* file for App store and *android/app/build.gradle* file for Google play store.

#### App center codepush releases

- version format is `x.y.z`, where x is the major release number, y is the minor release number and z is the maintenance/patch release number.
  - **Codepush releases will only be used for React Native Javascript only changes.**
  - **Major and minor release numbers are the same as the codepush target native release.  So codepush release only modifies the maintenance/patch release number.**
  - **Maintenance version number for a codepush release is always a non-zero number.**
- build number is **NOT** incremented for the codepush release.
- The codepush releases are integrated in the Fastlane CLI via ```yarn patch-beta-release``` cli command.  See Fastlane documentation for details.

### CodePush Work Flow

1. Build staging release app and perform regression test on simulators or devices locally.
2. Use codepush script or Fastlane CLI to codepush to Staging deployment.
3. Build the target native staging release app and run it on a simulator or a device.
4. Restart the target native staging release app and see if it gets codepushed.
5. Verify a successful codepushed JS bundle is in place via inspection of the new maintenance release number and testing of the JS functional changes.
6. Use codepush cli to promote Staging deployment to Production deployment and deploy the tested JS codepush changes to the field.

### CodePush Parameters

- App Name: Name of an app.  We have separate iOS and Android app for each mobile app.
- Deployment: App Center CodePush deployment targets.  In our case, we have  "Staging" or "Production" deployments.
  - Staging - staging release build for local codepush testing.
  - Production - production release build for codepushing to the field.
- CodePush Command:
  - release-react - codepush a react native release build to a deployment
  - promote - promote from one release build deployment to another.  In our case, we would always promote from "Staging" deployment to "Production" deployment
- Update mode
  - Mandatory - mandatory codepush.
  - Optional - optional codepush.

  >By default, CodePush will check for updates on every app start. If an update is available, it will be silently downloaded, and installed the next time the app is restarted (either explicitly by the end user or by the OS), which ensures the least invasive experience for your end users. If an available update is mandatory, then it will be installed immediately, ensuring that the end user gets it as soon as possible.
- Minimum target base version: The base target native or codepushed release version you want to codepush to.  **The major and minor release numbers should be the same as the codepush major and minor release numbers.**
- Description: Change description.

### CodePush Yarn Scripts

- To retrieve a list of mobile codepush apps, use

```
yarn code-push-apps
```

- To retrieve a mobile codepush app's deployment history, use

```
yarn code-history
```

- To deploy a codepush react native release or promote from Staging to Production deployment of a app

```
yarn code-push
```

- To roll back a codepush target release (**Not working**)

```
yarn code-rollback
```

    (Instead of rolling back a codepush, an alternative is to disable trouble codepush release on the app center and then push out a new version to the user.)

- To clear all deployment history for an app (**Use sparingly**)

```
yarn code-clear-deployment
```

> When an app's deployment history is cleared, App Center admin will need to manually re-enable the codepush set up again in the App Center's -> App -> Distribute -> CodePush page.  This action will produce two new **Staging** and **Production** deployment keys for that app.  Admin will need to first rename the new ones in the CodePush setting page and delete those new deployment keys to reset the codepush deployments or else the App Center CLI would unable to codepush correctly.
