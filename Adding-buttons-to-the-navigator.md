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

#### Floating Action Button (FAB) - Android only
Each screen can contain a single Fab which is displayed at the bottom right corner of the screen.

1. Simple Fab:
```js
  static navigatorButtons = {
    fab: {
      collapsedId: 'share',
      collapsedIcon: require('../../img/ic_share.png'),
      backgroundColor: '#607D8B'
    }
  };
```

2. Fab with expanded state
[Example](https://material-design.storage.googleapis.com/publish/material_v_9/0B8v7jImPsDi-ZmQ0UnFPZmtiSU0/components-buttons-fab-transition_speeddial_02.mp4)
```js
    fab: {
      collapsedId: 'share',
      collapsedIcon: require('../../img/ic_share.png'),
      expendedId: 'clear',
      expendedIcon: require('../../img/ic_clear.png'),
      backgroundColor: '#3F51B5',
      actions: [
        {
          id: 'mail',
          icon: require('../../img/ic_mail.png'),
          backgroundColor: '#03A9F4'
        },
        {
          id: 'twitter',
          icon: require('../../img/ic_twitter.png'),
          backgroundColor: '#4CAF50'
        }
      ]
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