# Mobile Fastlane CLI Developer Guide

## Purpose

Fastlane CLI is used to deploy React Native .

## Fastlane CLI Setup

You will need to install fastlane cli in the link below:

- [Fastlane Docs](https://docs.fastlane.tools/)

## Fastlane App Release

There are three main ways of releasing mobile app via Fastlane tools.  They are invoked via npm scripts.

1. Release major revision to iOS and Android beta release (has native changes).

    ```yarn major-beta-release```

2. Release minor revision to iOS and Android beta release (has native changes).

    ```yarn minor-beta-release```

3. Release maintenance/patch revision to iOS and Android codepush release (No native changes).

    ```yarn patch-beta-release```
