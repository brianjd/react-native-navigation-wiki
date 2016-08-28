## Installation - iOS

 * Make sure you are using react-native version 0.25.1

 * In your project folder run `npm install react-native-navigation --save`
> Note: We recommend using npm ver 3+. If you insist on using npm ver 2 please notice that the location for react-native-controllers in node_modules will be under the react-native-navigation folder and you'll need to change the paths in Xcode below accordingly.

 * Add the native files of the dependency [react-native-controllers](https://github.com/wix/react-native-controllers) to your Xcode project:

   * In Xcode, in Project Navigator (left pane), right-click on the `Libraries` > `Add files to [project name]`. Add `./node_modules/react-native-controllers/ios/ReactNativeControllers.xcodeproj` ([screenshots](https://facebook.github.io/react-native/docs/linking-libraries-ios.html#step-1))

   * In Xcode, in Project Navigator (left pane), click on your project (top) and select the `Build Phases` tab (right pane). In the `Link Binary With Libraries` section add `libReactNativeControllers.a` ([screenshots](https://facebook.github.io/react-native/docs/linking-libraries-ios.html#step-2))

   * In Xcode, in Project Navigator (left pane), click on your project (top) and select the `Build Settings` tab (right pane). In the `Header Search Paths` section add `$(SRCROOT)/../node_modules/react-native-controllers/ios`. Make sure on the right to mark this new path `recursive` ([screenshots](https://facebook.github.io/react-native/docs/linking-libraries-ios.html#step-3))

 * In Xcode, under your project files, modify `AppDelegate.m` according to this [example](https://github.com/wix/react-native-navigation/blob/master/example/ios/example/AppDelegate.m)