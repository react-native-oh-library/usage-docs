> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"><code><a href="https://github.com/oblador/react-native-vector-icons">react-native-vector-icons</a></code> </h1>
</p>
<p align="center">
    <a href="https://github.com/oblador/react-native-vector-icons">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/oblador/react-native-vector-icons/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/oblador/react-native-vector-icons)

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-vector-icons@10.0.3
```

#### **yarn**

```bash
yarn add react-native-vector-icons@10.0.3
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

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

### 本库自带字体的使用

```js
import FontAwesome from 'react-native-vector-icons/FontAwesome';

<FontAwesome.Button 
    name="glass"
    backgroundColor="#3b5998"
    size={20}
    >
</FontAwesome.Button>
```

### 外部字体使用
> [!ATTENTION] 使用外部字体时，请确保entry/src/main/ets/assets/fonts和entry/src/main/resource/rawfile/assets/assets/fonts下同时拥有要使用的ttf文件
使用外部字体时，不管是用户自己制作的字体文件还是从网站下载的字体文件，都需要有 *.ttf 和 *.json 文件(文件目录不固定，能引用到就可以了)

#### 用户自制字体文件
用户自己制作的字体文件导入使用，以下字体文件名和字体家族名仅供参考，以用户实际输出字体文件信息为准

```js
import { createIconSet } from 'react-native-vector-icons';

const CustomTest = createIconSet(
    require('../assets/fonts/test.json'), // 引入本地assets下的字体资源
    'poppy-icon',
    '../assets/fonts/test.ttf',  // 引入本地assets下的字体资源
  );

<CustomFont.Button
    name="to-do"
    backgroundColor="#3b5998"
    size={20}
    >
</CustomFont.Button>
```

#### [fontello](http://fontello.com)网站中的字体使用
从[fontello](http://fontello.com)网站选择合适的字体之后下载对应的字体文件和配置文件导入使用

```js
import { createIconSetFromFontello } from 'react-native-vector-icons';
import fontelloConfig from '../assets/fonts/config.json';

const CustomFontello = createIconSetFromFontello(
    fontelloConfig,
    'fontello',
    '../assets/fonts/fontello.ttf', // 引入本地assets下的字体资源
  );

<CustomFontello.Button
    name="emo-happy"
    backgroundColor="#3b5998"
    size={20}
    >
</CustomFontello.Button>
```

#### [IcoMoon](https://icomoon.io/app)网站中的字体使用
从[IcoMoon](https://icomoon.io/app)网站选择合适的字体之后下载对应的字体文件和配置文件导入使用

```js
import { createIconSetFromIcoMoon } from 'react-native-vector-icons';
import icoMoonConfig from '../assets/fonts/selection.json'; // 引入本地assets下的字体资源

const CustomFontIcoMoon = createIconSetFromIcoMoon(
    icoMoonConfig,
    'icomoon',
    '../assets/fonts/icomoon.ttf', // 引入本地assets下的字体资源
  );

<CustomFontIcoMoon.Button
    name="home2"
    backgroundColor="#3b5998"
    size={20}
    >
</CustomFontIcoMoon.Button>
```

### 以下展示了本库的基本用法

```js
import React from 'react';
import {ScrollView} from 'react-native';

//导入原库自带字体
import FontAwesome5 from 'react-native-vector-icons/FontAwesome5';
import FontAwesome6 from 'react-native-vector-icons/FontAwesome6';
import Fontisto from 'react-native-vector-icons/Fontisto';
import Foundation from 'react-native-vector-icons/Foundation';
import Ionicons from 'react-native-vector-icons/Ionicons';
import MaterialCommunityIcons from 'react-native-vector-icons/MaterialCommunityIcons';
import MaterialIcons from 'react-native-vector-icons/MaterialIcons';
import SimpleLineIcons from 'react-native-vector-icons/SimpleLineIcons';
import Octicons from 'react-native-vector-icons/Octicons';
import Zocial from 'react-native-vector-icons/Zocial';
import AntDesign from 'react-native-vector-icons/AntDesign';
import Entypo from 'react-native-vector-icons/Entypo';
import EvilIcons from 'react-native-vector-icons/EvilIcons';
import Feather from 'react-native-vector-icons/Feather';
import FontAwesome from 'react-native-vector-icons/FontAwesome';


import { createIconSetFromIcoMoon, createIconSetFromFontello, createIconSet } from 'react-native-vector-icons';
import icoMoonConfig from '../assets/fonts/icomoon-selection.json';
import fontelloConfig from '../assets/fonts/fontello-config.json';

export function VectorIconsDemo() {

  //引入用户自制字体
  const CustomTest = createIconSet(
    require('../assets/fonts/test.json'), // 引入本地assets下的字体资源
    'poppy-icon',
    '../assets/fonts/test.ttf', // 引入本地assets下的字体资源
  );

  //引入 IcoMoon 自定义字体
  const CustomIconMoon = createIconSetFromIcoMoon(
    icoMoonConfig,
    'icomoon',
    '../assets/fonts/icomoon.ttf' // 引入本地assets下的字体资源
  );

  //引入 fontello 自定义字体
  const CustomFontello = createIconSetFromFontello(
    fontelloConfig,
    'fontello',
    '../assets/fonts/fontello.ttf' // 引入本地assets下的字体资源
  );

  return (
    <ScrollView style={{ padding:20 }}>

      <CustomTest.Button
          name="application-record"
          backgroundColor="#3b5998"
          size={20}
       >
        CustomTest application-record
       </CustomTest.Button>

       <CustomTest.Button
          name="to-do"
          backgroundColor="#3b5998"
          size={20}
       >
        CustomTest to-do
       </CustomTest.Button>

      <CustomIconMoon.Button
          name="home2"
          backgroundColor="#3b5998"
       >
        CustomIconMoon home2
       </CustomIconMoon.Button>

       <CustomFontello.Button
          name="emo-happy"
          backgroundColor="#3b5998"
       >
        CustomFontello emo-happy
       </CustomFontello.Button>

        <AntDesign.Button
            name="forward"
            backgroundColor="#3b5998"
            size={20}
          >
        AntDesign forward
        </AntDesign.Button>

        <Entypo.Button
            name="app-store"
            backgroundColor="#3b5998"
            size={20}
          >
        Entypo app-store
        </Entypo.Button>

        <EvilIcons.Button
            name="bell"
            backgroundColor="#3b5998"
            size={20}
          >
        EvilIcons bell
        </EvilIcons.Button>

        <Feather.Button
            name="sunrise"
            backgroundColor="#3b5998"
            size={20}
          >
        Feather sunrise
        </Feather.Button>
        <FontAwesome.Button
            name="glass"
            backgroundColor="#3b5998"
            size={20}
          >
          FontAwesome glass
        </FontAwesome.Button>
        

        <FontAwesome5.Button
            name="angry"
            backgroundColor="#3b5998"
            size={20}
          >
          FontAwesome5_regular angry
        </FontAwesome5.Button>
        <FontAwesome5.Button
            name="adn"
            backgroundColor="#3b5998"
            size={20}
          >
          FontAwesome5_brands adn
        </FontAwesome5.Button>
        <FontAwesome5.Button
            name="ad"
            backgroundColor="#3b5998"
            size={20} 
            
          >
          FontAwesome5_solid ad
        </FontAwesome5.Button>

        <FontAwesome6.Button
            name="adn"
            backgroundColor="#3b5998"
            size={20} 
          >
          FontAwesome6_brands adn
        </FontAwesome6.Button>
        <FontAwesome6.Button
            name="bookmark"
            backgroundColor="#3b5998"
            size={20} 
            solid
          >
          FontAwesome6_regular bookmark
        </FontAwesome6.Button>
        <FontAwesome6.Button
            name="apple-whole"
            backgroundColor="#3b5998"
            size={20}
          >
          FontAwesome6_solid apple-whole
        </FontAwesome6.Button>
        <Fontisto.Button
            name="aws"
            backgroundColor="#3b5998"
            size={20}
          >
          Fontisto aws
        </Fontisto.Button>
        <Foundation.Button
            name="archive"
            backgroundColor="#3b5998"
            size={20}
          >
          Foundation archive
        </Foundation.Button>
        <Ionicons.Button
            name="aperture"
            backgroundColor="#3b5998"
            size={20}
          >
          Ionicons aperture
        </Ionicons.Button>
        <MaterialCommunityIcons.Button
              name="zip-box"
              backgroundColor="#3b5998"
              size={20}
            >
          MaterialCommunityIcons zip-box
        </MaterialCommunityIcons.Button>
        <MaterialIcons.Button
              name="airplay"
              backgroundColor="#3b5998"
              size={20}
            >
          MaterialIcons airplay
        </MaterialIcons.Button>
        <Octicons.Button
            name="share"
            backgroundColor="#3b5998"
            size={20}
          >
          Octicons share
        </Octicons.Button>
        <SimpleLineIcons.Button
            name="mouse"
            backgroundColor="#3b5998"
            size={20}
          >
          SimpleLineIcons mouse
        </SimpleLineIcons.Button>
        <Zocial.Button
            name="rss"
            backgroundColor="#3b5998"
            size={20}
          >
          Zocial rss
        </Zocial.Button>
    </ScrollView>
  );
}
```

## Link

目前 HarmonyOS 暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`

### 在 ArkTs 侧引入和注册字体文件

步骤一：
    复制 `node_modules/react-native-vector-icons/Fonts` 目录下的字体文件到  `entry/src/main/ets/assets/fonts` 目录下(如使用了外部字体文件，需要将*.ttf文件复制过来)

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
            familyName: 'anticon',
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
        },
        //以下三种为外部字体，这里是举例说明，以用户实际为准
        {
            familyName: 'icomoon',
            familySrc: '/assets/fonts/icomoon.ttf'
        },
        {
            familyName: 'fontello',
            familySrc: '/assets/fonts/fontello.ttf'
        },
        {
            familyName: 'poppy-icon',
            familySrc: '/assets/fonts/test.ttf'
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