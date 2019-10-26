# Enhanced Fluid Bottom Navigation Bar

[![NpmVersion](https://img.shields.io/npm/v/fluidbottomnavigation-rn.svg?style=flat-square)](https://www.npmjs.com/package/fluidbottomnavigation-rn)
[![NpmLicense](https://img.shields.io/npm/l/fluidbottomnavigation-rn.svg?style=flat-square)](https://www.npmjs.com/package/fluidbottomnavigation-rn)
[![Expo](https://img.shields.io/badge/expo-compatible-green.svg?style=flat-square)](https://expo.io/)

This is an enhanced version of [10clouds' fluid tab bar for React Native](https://github.com/10clouds/FluidBottomNavigation-rn).

Changes made by me, @VictorLi08, over the original:
- Added Expo compatibility by removing `react-native-view-overflow` and the need to link it.
- Added integrated vector icons via [@expo/vector-icons](https://github.com/expo/vector-icons) so you need not supply your own icons (this should work for normal React Native projects as well!).
- Tab bar now auto-selects first tab index on mount (this behavior is customizable).
- Tab bar background color is now fully customizable.
- Removed support for icons via image source (because good-looking 20x20 icons are hard to find and even the best 20x20 icon pales in comparison to FontAwesome).
- Removed example project in favor of expanded usage documentation.

![Sample](https://raw.githubusercontent.com/10clouds/FluidBottomNavigation-rn/master/static/sample.gif)

## Installation

### [npm](https://npmjs.com)
```
npm i enhanced-fluid-bottom-navigation-bar
```

### yarn
```
yarn add enhanced-fluid-bottom-navigation-bar
```

## Usage

### Rendering Component
This component requires just 2 props:
- `onPress` a function that should handle rendering tabs
- `values` an array of objects that contains the title and icon properties for each tab.

```JSX
<TabBar
  onPress={(tabIndex) => { this._handlePress(tabIndex) }}
  values={[
    {
      title: 'News',      // string, required
      icon: 'news',       // string, required
      iconSet: 'Entypo',  // string, required
      size: 32            // number, required (icon will be size x size)
    }
  ]}
/>
```

Look up valid icon names and their corresponding icon set at the [@expo/vector-icons directory](https://expo.github.io/vector-icons/).

### Integration with `react-navigation`
1. Define a custom component that renders `TabBar` with the `values` you want. React's tab navigator will pass `navigation` and `onTabPress` props to your component when hooked up; use these to implement the `onPress` callback to navigate to the appropriate route:

``` JSX
import TabBar from 'enhanced-fluid-bottom-navigation-bar';

class FluidTabBar extends Component {
  render() {
    return (
      <TabBar
        onPress={tabIndex => {
          let route = this.props.navigation.state.routes[tabIndex];
          this.props.onTabPress({route});
        }}
        values={[
          {
            title: 'Tab 1',
            icon: 'star',     
            iconSet: 'MaterialIcons',
            size: 32          
          }, {
            title: 'Tab 2',
            icon: 'check',     
            iconSet: 'AntDesign',
            size: 32          
          }
        ]}
      />
    );
  }
}
  ```
In this case, pressing a tab in `FluidTabBar` navigates to the route that shares the same array index.

2. Create a tab navigator and supply our custom component to `tabBarComponent`.
``` javascript
import {createBottomTabNavigator} from 'react-navigation-tabs';

const myTabNavigator = createBottomTabNavigator(
  {  // RouteConfigs
    Tab1: { screen: Tab1Screen },
    Tab2: { screen: Tab2Screen },
  },
  {
    initialRouteName: 'Tab1',
    tabBarComponent: FluidTabBar,
  }
);
```

3. Create an app container from your tab navigator and use it as your top-level component.
``` javascript
import {createAppContainer} from 'react-navigation';

const myAppContainer = createAppContainer(myTabNavigator)
```

## Customization

Prop | Type | Default | Description
--- | --- | --- | ---
tintColor | String | rgb(76, 83, 221) | Adjusts icon bubble background color and text color.
backgroundColor | String | rgb(76, 83, 221) | Adjusts tab bar background color and icon tint color when selected.
autoSelect | Number | 0 | Auto-selects the tab at this index on mount.

## Author

__Original Author:__ [Patryk Mierzejewski](https://github.com/pmierzejewski)

__Improvements By:__ [Victor Li](https://github.com/victorli08)

## License

Available under the MIT license. See the LICENSE file for more info.
