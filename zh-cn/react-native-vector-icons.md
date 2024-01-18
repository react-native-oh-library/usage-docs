<p align="center">
  <h1 align="center"><code><a href="https://github.com/oblador/react-native-vector-icons">react-native-vector-icons</a></code> </h1>
</p>
<p align="center">
    <a href="https://github.com/oblador/react-native-vector-icons">
        <img src="https://cloud.githubusercontent.com/assets/378279/12009887/33f4ae1c-ac8d-11e5-8666-7a87458753ee.png" alt="Supported platforms" />
    </a>
    <a href="https://github.com/oblador/react-native-vector-icons/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

## 安装与使用

#### 进入到工程目录并输入以下命令：

#### **yarn**

```bash
yarn add react-native-vector-icons@10.0.3
```

#### **npm**

```bash
npm install --save react-native-vector-icons@10.0.3
```

### 基本使用

#### 自带字体图标对照网页

[Explore all icons](https://oblador.github.io/react-native-vector-icons/).

- [`AntDesign`](https://ant.design/) from AntFinance (*298* icons)
- [`Entypo`](http://entypo.com) by Daniel Bruce (v1.0.1 with *411* icons)
- [`EvilIcons`](http://evil-icons.io) designed by Alexander Madyankin & Roman Shamin (v1.10.1 with *70* icons)
- [`Feather`](http://feathericons.com) created by Cole Bemis & Contributors (v4.28.0 featuring *286* icons)
- [`FontAwesome`](http://fortawesome.github.io/Font-Awesome/icons/) by Dave Gandy (v4.7.0 containing *675* icons)
- [`FontAwesome 5`](https://fontawesome.com/v5/icons/) from Fonticons, Inc. (v5.15.3 offering *1598* free and *7848* pro icons)
- [`FontAwesome 6`](https://fontawesome.com) designed by Fonticons, Inc. (v6.1.2 featuring *2016* free and *16150* pro icons)
- [`Fontisto`](https://github.com/kenangundogan/fontisto) created by Kenan Gündoğan (v3.0.4 featuring *615* icons)
- [`Foundation`](http://zurb.com/playground/foundation-icon-fonts-3) by ZURB, Inc. (v3.0 with *283* icons)
- [`Ionicons`](https://ionicons.com/) crafted by Ionic (v7.1.0 containing *1338* icons)
- [`MaterialIcons`](https://fonts.google.com/icons/) by Google, Inc. (v4.0.0 featuring *2189* icons)
- [`MaterialCommunityIcons`](https://materialdesignicons.com/) from MaterialDesignIcons.com (v6.5.95 including *6596* icons)
- [`Octicons`](http://octicons.github.com) designed by Github, Inc. (v16.3.1 with *250* icons)
- [`Zocial`](http://zocial.smcllns.com/) by Sam Collins (v1.4.0 with *100* icons)
- [`SimpleLineIcons`](https://simplelineicons.github.io/) crafted by Sabbir & Contributors (v2.5.5 with *189* icons)

#### 自带字体的使用

```js
import FontAwesome from 'react-native-vector-icons/FontAwesome';

<FontAwesome.Button 
    name="fontName">
</FontAwesome.Button>
```

### 自定义字体使用

```js
import { createIconSet } from 'react-native-vector-icons';

const CustomFont = createIconSet(
    require('../assets/fonts/customfont.json'),
    'custom-fontFamily',
    '../assets/fonts/customfont.ttf',
  );

<CustomFont.Button
    name="fontName"
    >
</CustomFont.Button>
```

### [fontello](http://fontello.com)字体使用
从[fontello](http://fontello.com)网站选择合适的字体之后下载对应的字体文件和配置文件导入使用

```js
import { createIconSetFromFontello } from 'react-native-vector-icons';
import fontelloConfig from '../assets/fonts/config.json';

const CustomFontello = createIconSetFromFontello(
    fontelloConfig,
    'fontello',
    '../assets/fonts/fontello.ttf',
  );

<CustomFontello.Button
    name="fontName"
    >
</CustomFontello.Button>
```

### [IcoMoon](https://icomoon.io/app)字体使用
从[IcoMoon](https://icomoon.io/app)网站选择合适的字体之后下载对应的字体文件和配置文件导入使用

```js
import { createIconSetFromIcoMoon } from 'react-native-vector-icons';
import icoMoonConfig from '../assets/fonts/selection.json';

const CustomFontIcoMoon = createIconSetFromIcoMoon(
    icoMoonConfig,
    'icomoon',
    '../assets/fonts/icomoon.ttf',
  );

<CustomFontIcoMoon.Button
    name="fontName"
    >
</CustomFontIcoMoon.Button>
```

## Link

目前鸿蒙暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的鸿蒙工程 `harmony`

### 在 ArkTs 侧引入和注册字体文件

步骤一：
    复制 `react-native-vector-icons/Fonts` 目录下的字体文件到  `entry/src/main/ets/assets/fonts` 目录下

步骤二：
    打开 `entry/src/main/ets/pages/Index.ets`，添加以下代码

```ts
    import font from '@ohos.font';
    //...

    //定义字体文件的 familyName 和 familySrc
    //注意: familyName 要和 react-native-vector-icons 目录下 [字体名.js] 中的 familyName 对应，当前库版本10.0.3，版本不同名字可能不同，请到对应文件中查看
    //特别注意：FontAwesome 系列中字体的 familyName 需要通过代码逻辑自行理解
    const fonts: font.FontOptions[] = [
        {
            familyName: 'AntDesign',
            familySrc: '/assets/fonts/AntDesign.ttf'
        },
        {
            familyName: 'Entypo',
            familySrc: '/assets/fonts/Entypo.ttf'
        },
        {
            familyName: 'EvilIcons',
            familySrc: '/assets/fonts/EvilIcons.ttf'
        },
        {
            familyName: 'Feather',
            familySrc: '/assets/fonts/Feather.ttf'
        },
        {
            familyName: 'FontAwesome',
            familySrc: '/assets/fonts/FontAwesome.ttf'
        },
        {
            familyName: 'FontAwesome5Brands-Regular',
            familySrc: '/assets/fonts/FontAwesome5_Brands.ttf'
        },
        {
            familyName: 'FontAwesome5Free-Regular',
            familySrc: '/assets/fonts/FontAwesome5_Regular.ttf'
        },
        {
            familyName: 'FontAwesome5Free-Solid',
            familySrc: '/assets/fonts/FontAwesome5_Solid.ttf'
        },

        {
            familyName: 'FontAwesome6Brands-Regular',
            familySrc: '/assets/fonts/FontAwesome6_Brands.ttf'
        },
        {
            familyName: 'FontAwesome6Free-Regular',
            familySrc: '/assets/fonts/FontAwesome6_Regular.ttf'
        },
        {
            familyName: 'FontAwesome6Free-Solid',
            familySrc: '/assets/fonts/FontAwesome6_Solid.ttf'
        },

        {
            familyName: 'Fontisto',
            familySrc: '/assets/fonts/Fontisto.ttf'
        },
        {
            familyName: 'fontcustom',
            familySrc: '/assets/fonts/Foundation.ttf'
        },
        {
            familyName: 'Ionicons',
            familySrc: '/assets/fonts/Ionicons.ttf'
        },
        {
            familyName: 'Material Design Icons',
            familySrc: '/assets/fonts/MaterialCommunityIcons.ttf'
        },
        {
            familyName: 'Material Icons',
            familySrc: '/assets/fonts/MaterialIcons.ttf'
        },
        {
            familyName: 'Octicons',
            familySrc: '/assets/fonts/Octicons.ttf'
        },
        {
            familyName: 'simple-line-icons',
            familySrc: '/assets/fonts/SimpleLineIcons.ttf'
        },
        {
            familyName: 'zocial',
            familySrc: '/assets/fonts/Zocial.ttf'
        }
    ]

    @Entry
    @Component
    struct Index {
        //...
        aboutToAppear() {
            //...

            //注册字体文件
            for (const customFont of fonts) {
                font.registerFont(customFont)
            }
        }
        //...
    }
```
#### 提醒：自定义字体也需要用同样的方法在此注册

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请使用 Api 11 及以上版本，低版本会导致font注册不成功，图标显示不出来。


## 遗留问题

- [ ] getImageSource和getImageSourceSync原生方法可以将字体文件绘制成Bitmap位图供 `Image` 组件使用，Harmony OS侧暂时不支持

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/oblador/react-native-vector-icons/blob/master/LICENSE) ，请自由地享受和参与开源。
