
# Purpose

Welcome to mobile app development wiki!  This wiki has information pertaining to the app development.

# Development Environments
## Editor
VS code is what we use.  However, you can use other ones but some of the linters and tools might not work well in other editors.

## Yarn scripts

Most of the yarn scripts int the package.json file is pretty straightforward.  Here are some often used ones:

- To clean react native builds, temp files and node modules:
  ```
  yearn clean-rn
  ```
  NOTE: current script will freeze after "npm cache verify task has finished running in ...".  You can just control-C out of it and run `yarn install` afterwards.

- To redo ios pods, run the following
  ```
  yarn podRedo
  ```

- To do jest test on all unit tests:
   ```
   yarn test -u
   ```

- To do jest test on one unit test and watch result in realtime:
  ```
  yarn test -u --watch 'app/lib/__tests__/util.tests.js
  ```

- To run ios app in debug mode on emulator
  ```
  yarn ios-familyfare-dev --simulator="iPhone X"
  ```

- To run ios app in debug mode on device
  ```
  npx react-native run-ios --scheme FamilyFare-dev --device="iPhone X
  ```

- To run android app on emulator/device with emulator already up or device connected via USB
  ```
  yarn android-familyfare
  ```

- To run sonar scanner
  ```
  yarn sonar-scanner
  ```
# Development Tips
## React Native upgrades
Because of the legacy RN iOS Podfile and/or Android gradle setups we have, currently we can't rely on the `npx react-native upgrade` command to upgrade RN.  To upgrade to the next version of RN, developers need to manually change the package.json, iOS Podfile and Android gradle files.

***Note***:

In order to fix this problem, a fresh RN project should be created and then developers would have to manually bring in the NPM packages one by one and also maintain the integrity of the iOS Podfile and Android gradle files to ensure that the automatic RN upgrades can be maintained throughout this process.

## Develop and Test on devices and simulators
### iOS
Usually it is more efficient to develop and test on iOS simulator for non-device related features since iOS simulator can simulator most of the behaviors on iOS devices.

### Android
Because Android emulators are usually more limited in capabilities (albeit it is getting better), it is often more productive to do testing on physical Android devices.
However, sometimes, developers have no choice but to test on Android emulators in order to test functionalities across different Android OS versions via emulators.

- To ensure debug mode runs correctly on Android devices, do the following:

1. Connect the device via USB port.
2. Run the `adb reverse tcp:8081 tcp:8081` to ensure the RN debugger http request is redirected to the device.
3. Run the yarn script, e.g. `yarn android-familyfare-dev` or Android Studio to run the app on the device.
4. When the app is running on the device, shake the device and select "Debug" to connect the debug session to the VS Code debug tool or the Google Chrome devtool debugger.