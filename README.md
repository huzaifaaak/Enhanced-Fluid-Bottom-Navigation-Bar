# FluidBottomNavigation for React Native

[![NpmVersion](https://img.shields.io/npm/v/fluidbottomnavigation-rn.svg?style=flat-square)](https://www.npmjs.com/package/fluidbottomnavigation-rn)
[![NpmLicense](https://img.shields.io/npm/l/fluidbottomnavigation-rn.svg?style=flat-square)](https://www.npmjs.com/package/fluidbottomnavigation-rn)
[![Expo](https://img.shields.io/badge/expo-compatible-green.svg?style=flat-square)](https://expo.io/)

The Animated Tab Bar for React Native

Improvements made by me, @VictorLi08, over the original:
- Added Expo compatibility by removing `react-native-view-overflow`.
- Added integrated vector icons via [@expo/vector-icons](https://github.com/expo/vector-icons) (should work for normal React Native projects as well!)
- Tab bar now auto-selects first tab index.
- Removed support for icons via image source (because only 20x20 icons fit, and most 20x20 icons are ugly).

![Sample](https://raw.githubusercontent.com/10clouds/FluidBottomNavigation-rn/master/static/sample.gif)

## Example

To run the example project, clone the repo, and run `npm install` from the Example directory first.

## Installation

It is available through [npm](https://npmjs.com). To install just run

```
npm i fluidbottomnavigation-rn
```

in your project directory. And then link it's native dependency with

```
react-native link react-native-view-overflow
```

and you're done!

## Usage

This component requires just 2 props. `onPress` function, that should handle rendering tabs and an array of `values` objects that contains title and icons for given tabs.

```JSX
<TabBar
  onPress={(tabIndex) => { this._handlePress(tabIndex) }}
  values={[
    {
      title: "News",      // required
      icon: 'news',       // required
      iconSet: 'Entypo',  // required
      size: 32            // required
    }
  ]}
/>
```

Look up valid icon names and their corresponding icon set at the [@expo/vector-icons directory](https://expo.github.io/vector-icons/).

## Customization

Prop | Type | Default | Description
--- | --- | --- | ---
tintColor | String | rgb(76, 83, 221) | Adjusts icon background color and text color to suit your app.
autoSelect | Number | 0 | Auto-selects the tab at this index on mount.

## Author

[Patryk Mierzejewski](https://github.com/pmierzejewski)

## License

FluidBottomNavigation Component is available under the MIT license. See the LICENSE file for more info.
