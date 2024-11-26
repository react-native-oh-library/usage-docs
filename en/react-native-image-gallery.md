> Template version: v0.2.0

<p align="center">
  <h1 align="center"> <code>react-native-image-gallery</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-native-oh-library/react-native-image-gallery">
        <img src="https://img.shields.io/badge/platforms-android%20%7C%20ios%20%7C%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="">
        <img src="https://img.shields.io/badge/license-ISC-green.svg" alt="License" />
    </a>
</p>

>   [!tip]  
>
> [GitHub address](https://github.com/react-native-oh-library/react-native-image-gallery/tree/sig)

## Installation and Usage

Find the matching version information in the release address of a third-party library：[@react-native-oh-tpl/react-native-image-gallery Releases](https://github.com/react-native-oh-library/react-native-image-gallery/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

>  [!TIP] Replace the content with the path of the .tgz package at the comment sign (#).

#### **npm**

```bash
npm i @react-native-oh-tpl/react-native-image-gallery
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-image-gallery
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import Gallery from 'react-native-image-gallery';

  render() {
    return (
      <Gallery
        style={{ flex: 1, backgroundColor: 'black' }}
        images={[
          { source: require('yourApp/image.png'), dimensions: { width: 150, height: 150 } },
          { source: { uri: 'http://i.imgur.com/XP2BE7q.jpg' } },
          { source: { uri: 'http://i.imgur.com/5nltiUd.jpg' } },
          { source: { uri: 'http://i.imgur.com/6vOahbP.jpg' } },
          { source: { uri: 'http://i.imgur.com/kj5VXtG.jpg' } }
        ]}
      />
    );
  }
```

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-image-gallery Releases](https://github.com/react-native-oh-library/react-native-image-gallery/releases)

#### Properties

| Prop   | Description | Type  | Default | Platform | HarmonyOS Support |
| --------------------- | --------------------- | -------- | -------- |----------|-------------------|
`images` | Your array of images | `array` | Required | all      | yes               |
`initialPage` | Image displayed first | `number` | `0`|    all      | yes               |
`imageComponent` | Custom function to render your images, 1st param is the image props, 2nd is its dimensions | `function` | `<Image>` component|    all      | yes               |
`errorComponent` | Custom function to render the page of an image that couldn't be displayed | `function` | A `<View>` with a stylized error|    all      | yes               |
`flatListProps` | Props to be passed to the underlying `FlatList` | `object` | `{windowSize: 3}`|     all     | yes               |
`pageMargin` | Blank space to show between images | `number` | `0`|     all     | yes               |
`onPageSelected` | Fired with the index of page that has been selected | `function`|          |    all      | yes               |
`onPageScrollStateChanged` | Called when page scrolling state has changed, see [scroll state and events](#scroll-state-and-events) | `function`|     |  all        | yes               |
`onPageScroll` | Scroll event, see [scroll state and events](#scroll-state-and-events) | `function`|      |    all      | yes               |
`scrollViewStyle` | Custom style for the `FlatList` component | `object` | `{}`|     all     | yes               |
`onSingleTapConfirmed` | Fired after a single tap | `function`|   |      all    | yes               |
`onLongPress` | Fired after a long press | `function`|     |      all    | yes               |

## Known Issues

## Others

## License

This project is licensed under [The ISC License (ISC)](https://choosealicense.com/licenses/isc).
