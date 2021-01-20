# Enhanced Fluid Bottom Navigation Bar

[![NpmVersion](https://img.shields.io/npm/v/enhanced-fluid-bottom-navigation-bar.svg?style=flat-square)](https://www.npmjs.com/package/enhanced-fluid-bottom-navigation-bar)
[![NpmLicense](https://img.shields.io/npm/l/enhanced-fluid-bottom-navigation-bar.svg?style=flat-square)](https://www.npmjs.com/package/enhanced-fluid-bottom-navigation-bar)
[![Expo](https://img.shields.io/badge/expo-compatible-green.svg?style=flat-square)](https://expo.io/)

This project improves the customization of [10clouds' fluid tab bar for React Native](https://github.com/10clouds/FluidBottomNavigation-rn).

What's New in 0.2.2/0.2.3:
- Fixed and issue where `Zocial` icons were not being rendered properly.
- Formatting and linting.
- Optimized dependencies.

Changelog:
- Added Expo compatibility by removing `react-native-view-overflow` and the need to link it.
- Tab bar now auto-selects first tab index on mount (this behavior is customizable).
- Tab bar background color is now fully customizable.
- Icon highlight color on select is now fully customizable.
- Icon font size and font family is now fully customizable.
- Deprecated the ability to provide image sources for icon images.
- Removed example project in favor of expanded usage documentation.
- Fixed an issue where font scales poorly for long tab names when font size is not specified.

![Sample](https://raw.githubusercontent.com/VictorLi08/Enhanced-Fluid-Bottom-Navigation-Bar/master/static/sample.gif)

## Installation

### yarn (recommended)
```
yarn add https://github.com/huzaifaaak/Enhanced-Fluid-Bottom-Navigation-Bar.git
```

### npm
```
npm i https://github.com/huzaifaaak/Enhanced-Fluid-Bottom-Navigation-Bar.git
```

## Usage

### Rendering Component
This component requires just 2 props:
- `onPress`: a function that should handle rendering tabs.
- `values`: an array of objects that contains the title and icon properties for each tab.

```JSX
<TabBar
  onPress={tabIndex => { this._handlePress(tabIndex) }}
  values={[
    {
      title: 'News',      // required
      icon: news,       // required
      size: 32            // required (icon will be size x size)
    }
  ]}
/>
```

### Integration with `react-navigation`
1. Define a custom component that renders `TabBar` with the `values` you want. React's tab navigator will pass `navigation` and `onTabPress` props to your component when hooked up; use these to implement the `onPress` callback to navigate to the appropriate route:

``` JSX
import TabBar from 'enhanced-fluid-bottom-navigation-bar';

import Icon1 from '/images/icon1.png';
import Icon2 from './images/icon2.png';

function MyTabs() {
  return (
    <Tab.Navigator
      tabBar={props =>
        <TabBar {...props}
          onPress={(tabIndex) => {
            const { state, navigation } = props;
            const route = props.state.routes[tabIndex];
            const isFocused = state.index === tabIndex;
            const event = navigation.emit({
              type: 'tabPress',
              target: route.key,
              canPreventDefault: true,
            });

            if (!isFocused && !event.defaultPrevented) {
              navigation.navigate(route.name);
            }
          }}
          values={[
            {
              title: 'Tab1',
              icon: Icon1
            }, {
              title: 'Tab2',
              icon: Icon2
            },
            {
              title: 'Tab 3',
              icon: Icon1
            }, {
              title: 'Tab 4',
              icon: Icon2
            }
          ]}
        />}
    >
      <Tab.Screen name="Tab1" component={Tab1} />
      <Tab.Screen name="Tab2" component={Tab2} />
      <Tab.Screen name="Tab3" component={Tab3} />
      <Tab.Screen name="Tab4" component={Tab4} />
    </Tab.Navigator>
  );
}

```
In this case, pressing a tab in `FluidTabBar` navigates to the route that shares the same array index.

2. Pass MyTabs in the stack navigator

``` javascript
<Stack.Navigator
  initialRouteName="Tabs"
  headerMode="none">
    <Stack.Screen name="Tabs" component={MyTabs} />
</Stack.Navigator>
```

## Customization

Prop | Type | Default | Description
--- | --- | --- | ---
tintColor | String | rgb(76, 83, 221) | Icon bubble background color and text color.
selectColor | String | rgb(255, 255, 255) | Icon tint or highlight color when selected.
backgroundColor | String | rgb(255, 255, 255) | Tab bar background color.
autoSelect | Number | 0 | Auto-selects the tab at this index on mount.
fontSize | Number | undefined | Font size for tab captions.
fontFamily | String | undefined | Font family for tab captions.

NOTE: fontSize and fontFamily default to React Native's standard font size and font face.

## Author

__Original Author:__ [Patryk Mierzejewski](https://github.com/pmierzejewski)

__Modifications By:__ [Victor Li](https://github.com/victorli08)

__Modifications By:__ [Huzaifa K](https://github.com/huzaifaaak)

## License

Available under the MIT license. See the LICENSE file for more info.
