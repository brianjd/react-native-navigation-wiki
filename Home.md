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







## Styling the navigator

You can style the navigator appearance and behavior by passing a `navigatorStyle` object. This object can be passed when the screen is originally created; can be defined per-screen by setting `static navigatorStyle = {};` on the screen component; and can be overridden when a screen is pushed.

The easiest way to style your screen is by adding `static navigatorStyle = {};` to your screen React component definition.

```js
export default class StyledScreen extends Component {
  static navigatorStyle = {
    drawUnderNavBar: true,
    navBarTranslucent: true
  };
  constructor(props) {
    super(props);
  }
  render() {
    return (
      <View style={{flex: 1}}>...</View>
     );
  }
```

#### Style object format

```js
{
  navBarTextColor: '#000000', // change the text color of the title (remembered across pushes)
  navBarBackgroundColor: '#f7f7f7', // change the background color of the nav bar (remembered across pushes)
  navBarButtonColor: '#007aff', // change the button colors of the nav bar (eg. the back button) (remembered across pushes)
  navBarHidden: false, // make the nav bar hidden
  navBarHideOnScroll: false, // make the nav bar hidden only after the user starts to scroll
  navBarTranslucent: false, // make the nav bar semi-translucent, works best with drawUnderNavBar:true
  navBarTransparent: false, // make the nav bar transparent, works best with drawUnderNavBar:true
  navBarNoBorder: false, // hide the navigation bar bottom border (hair line). Default false
  drawUnderNavBar: false, // draw the screen content under the nav bar, works best with navBarTranslucent:true
  drawUnderTabBar: false, // draw the screen content under the tab bar (the tab bar is always translucent)
  statusBarBlur: false, // blur the area under the status bar, works best with navBarHidden:true
  navBarBlur: false, // blur the entire nav bar, works best with drawUnderNavBar:true
  tabBarHidden: false, // make the screen content hide the tab bar (remembered across pushes)
  statusBarHideWithNavBar: false // hide the status bar if the nav bar is also hidden, useful for navBarHidden:true
  statusBarHidden: false, // make the status bar hidden regardless of nav bar state
  statusBarTextColorScheme: 'dark' // text color of status bar, 'dark' / 'light' (remembered across pushes)
}
```

> Note: If you set any styles related to the Status Bar, make sure that in Xcode > project > Info.plist, the property `View controller-based status bar appearance` is set to `YES`.

All supported styles are defined [here](https://github.com/wix/react-native-controllers#styling-navigation). There's also an example project there showcasing all the different styles.

## Adding buttons to the navigator

Nav bar buttons can be defined per-screen by adding `static navigatorButtons = {...};` on the screen component definition. This object can also be passed when the screen is originally created; and can be overridden when a screen is pushed. Handle onPress events for the buttons by setting your handler with `navigator.setOnNavigatorEvent(callback)`.

```js
class FirstTabScreen extends Component {
  static navigatorButtons = {
    rightButtons: [
      {
        title: 'Edit', // for a textual button, provide the button title (label)
        id: 'edit', // id for this button, given in onNavigatorEvent(event) to help understand which button was clicked
        testID: 'e2e_rules', // optional, used to locate this view in end-to-end tests
        disabled: true, // optional, used to disable the button (appears faded and doesn't interact)
        disableIconTint: true, // optional, by default the image colors are overridden and tinted to navBarButtonColor, set to true to keep the original image colors
        showAsAction: 'ifRoom' // optional, Android only. Control how the button is displayed in the Toolbar. Accepted valued: 'ifRoom' (default) - Show this item as a button in an Action Bar if the system decides there is room for it. 'always' - Always show this item as a button in an Action Bar. 'withText' - When this item is in the action bar, always show it with a text label even if it also has an icon specified. 'never' - Never show this item as a button in an Action Bar.
      },
      {
        icon: require('../../img/navicon_add.png'), // for icon button, provide the local image asset name
        id: 'add' // id for this button, given in onNavigatorEvent(event) to help understand which button was clicked
      }
    ]
  };
  constructor(props) {
    super(props);
    // if you want to listen on navigator events, set this up
    this.props.navigator.setOnNavigatorEvent(this.onNavigatorEvent.bind(this));
  }
  onNavigatorEvent(event) { // this is the onPress handler for the two buttons together
    if (event.type == 'NavBarButtonPress') { // this is the event type for button presses
      if (event.id == 'edit') { // this is the same id field from the static navigatorButtons definition
        AlertIOS.alert('NavBar', 'Edit button pressed');
      }
      if (event.id == 'add') {
        AlertIOS.alert('NavBar', 'Add button pressed');
      }
    }
  }
  render() {
    return (
      <View style={{flex: 1}}>...</View>
     );
  }
```

#### Buttons object format

```js
{
  rightButtons: [{ // buttons for the right side of the nav bar (optional)
    title: 'Edit', // if you want a textual button
    icon: require('../../img/navicon_edit.png'), // if you want an image button
    id: 'compose', // id of the button which will pass to your press event handler
    testID: 'e2e_is_awesome', // if you have e2e tests, use this to find your button
    disabled: true, // optional, used to disable the button (appears faded and doesn't interact)
    disableIconTint: true, // optional, by default the image colors are overridden and tinted to navBarButtonColor, set to true to keep the original image colors
  }],
  leftButtons: [] // buttons for the left side of the nav bar (optional)
}
```

## Styling the tab bar

You can style the tab bar appearance by passing a `tabsStyle` object when the app is originally created (on `startTabBasedApp`).

```js
Navigation.startTabBasedApp({
  tabs: [ ... ],
  tabsStyle: { // optional, add this if you want to style the tab bar beyond the defaults
    tabBarButtonColor: '#ff0000'
  }
});
```

#### Style object format

```js
{
  tabBarButtonColor: '#ffff00', // change the color of the tab icons and text (also unselected)
  tabBarSelectedButtonColor: '#ff9900', // change the color of the selected tab icon and text (only selected)
  tabBarBackgroundColor: '#551A8B' // change the background color of the tab bar
}
```

All supported styles are defined [here](https://github.com/wix/react-native-controllers#styling-tab-bar). There's also an example project there showcasing all the different styles.

## Deep links

Deep links are strings which represent internal app paths/routes. They commonly appear on push notification payloads to control which section of the app should be displayed when the notification is clicked. For example, in a chat app, clicking on the notification should open the relevant conversation on the "chats" tab.

Another use-case for deep links is when one screen wants to control what happens in another sibling screen. Normally, a screen can only push/pop from its own stack, it cannot access the navigation stack of a sibling tab for example. Returning to our chat app example, assume that by clicking on a contact in the "contacts" tab we want to open the relevant conversation in the "chats" tab. Since the tabs are siblings, you can achieve this behavior by triggering a deep link:

```js
onContactSelected(contactID) {
  this.props.navigator.handleDeepLink({
    link: 'chats/' + contactID
  });
}
```

> Tip: Deep links are also the recommended way to handle side drawer actions. Since the side drawer screen is a sibling to the rest of the app, it can control the other screens by triggering deep links.

#### Handling deep links

Every deep link event is broadcasted to all screens. A screen can listen to these events by defining a handler using `setOnNavigatorEvent` (much like listening for button events). Using this handler, the screen can filter links directed to it by parsing the link string and act upon any relevant links found.

```js
export default class SecondTabScreen extends Component {
  constructor(props) {
    super(props);
    // if you want to listen on navigator events, set this up
    this.props.navigator.setOnNavigatorEvent(this.onNavigatorEvent.bind(this));
  }
  onNavigatorEvent(event) {
    // handle a deep link
    if (event.type == 'DeepLink') {
      const parts = event.link.split('/');
      if (parts[0] == 'tab2') {
        // handle the link somehow, usually run a this.props.navigator command
      }
    }
  }
```

#### Deep link string format

There is no specification for the format of deep links. Since you're implementing the parsing logic in your handlers, you can use any format you wish.

## Third party libraries support

### react-native-vector-icons

If you would like to use [react-native-vector-icons](https://github.com/oblador/react-native-vector-icons) for your Toolbar icons, you can follow [this example](https://github.com/wix/react-native-navigation/issues/43#issuecomment-223907515) or [this](https://gist.github.com/dropfen/4a2209d7274788027f782e8655be198f) gist.

### Mobx
If you prefer Mobx over Redux, show your interest in this [thread](https://github.com/wix/react-native-navigation/issues/187). Also checkout @mastermoo's [POC](https://github.com/mastermoo/navigation-mobx-example) of using navigation with Mobx.

## License

The MIT License.

See [LICENSE](LICENSE)
