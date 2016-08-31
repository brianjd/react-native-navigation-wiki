# React Native Navigation

App-wide support for 100% native navigation with an easy cross-platform interface. For iOS, this package is a wrapper around [react-native-controllers](https://github.com/wix/react-native-controllers), but provides a simplified more abstract API over it. This abstract API will be unified with the Android solution which is currently work in progress. It also fully supports redux if you use it.

## Overview

* [Why use this package](#why-use-this-package)
* [Installation - iOS](#installation---ios)
* [Installation - Android](#installation---android)
* [Usage](#usage)
* [Top Level API](#top-level-api)
* [Screen API](#screen-api)
* [Styling the navigator](#styling-the-navigator)
* [Adding buttons to the navigator](#adding-buttons-to-the-navigator)
* [Styling the tab bar](#styling-the-tab-bar)
* [Deep links](#deep-links)
* [Third party libraries support](#third-party-libraries-support)
* [Release Notes](RELEASES.md)
* [License](#license)

## Why use this package

One of the major things missing from React Native core is fully featured native navigation. Navigation includes the entire skeleton of your app with critical components like nav bars, tab bars and side menu drawers.

If you're trying to deliver a user experience that's on par with the best native apps out there, you simply can't compromise on JS-based components trying to fake the real thing.

For example, this package replaces the native [NavigatorIOS](https://facebook.github.io/react-native/docs/navigatorios.html) that has been [abandoned](https://facebook.github.io/react-native/docs/navigator-comparison.html) in favor of JS-based solutions that are easier to maintain. For more details see in-depth discussion [here](https://github.com/wix/react-native-controllers#why-do-we-need-this-package).















## Third party libraries support

### react-native-vector-icons

If you would like to use [react-native-vector-icons](https://github.com/oblador/react-native-vector-icons) for your Toolbar icons, you can follow [this example](https://github.com/wix/react-native-navigation/issues/43#issuecomment-223907515) or [this](https://gist.github.com/dropfen/4a2209d7274788027f782e8655be198f) gist.

### Mobx
If you prefer Mobx over Redux, show your interest in this [thread](https://github.com/wix/react-native-navigation/issues/187). Also checkout @mastermoo's [POC](https://github.com/mastermoo/navigation-mobx-example) of using navigation with Mobx.

## License

The MIT License.

See [LICENSE](LICENSE)
