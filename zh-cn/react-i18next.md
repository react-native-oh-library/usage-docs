> 模板版本：v0.1.3

<p align="center">
  <h1 align="center"> <code>react-i18next</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/i18next/react-i18next/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

>[!tip] [Github 地址](https://github.com/i18next/react-i18next)


## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash

npm install i18next@^23.2.3
npm install react-i18next@^14.0.0

```

#### **yarn**

```bash

yarn add i18next@^23.2.3
yarn add react-i18next@^14.0.0

```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

```js
import React from "react";
import { createRoot } from 'react-dom/client';
import i18n from "i18next";
import { useTranslation, initReactI18next } from "react-i18next";

i18n
  .use(initReactI18next) // passes i18n down to react-i18next
  .init({
    // the translations
    // (tip move them in a JSON file and import them,
    // or even better, manage them via a UI: https://react.i18next.com/guides/multiple-translation-files#manage-your-translations-with-a-management-gui)
    resources: {
      en: {
        translation: {
          "Welcome to React": "Welcome to React and react-i18next"
        }
      }
    },
    lng: "en", // if you're using a language detector, do not define the lng option
    fallbackLng: "en",

    interpolation: {
      escapeValue: false // react already safes from xss => https://www.i18next.com/translation-function/interpolation#unescape
    }
  });

function App() {
  const { t } = useTranslation();

  return <h2>{t('Welcome to React')}</h2>;
}

// append app to dom
const root = createRoot(document.getElementById('root'));
root.render(
  <App />
);
```

## 约束与限制

### 兼容性

 在下述版本验证通过：

1. RNOH：0.72.11; SDK：OpenHarmony(api11) 4.1.0.53; IDE：DevEco Studio 4.1.3.412; ROM：2.0.0.52;
2. RNOH：0.72.13; SDK：HarmonyOS NEXT Developer Preview1; IDE：DevEco Studio 4.1.3.500; ROM：2.0.0.58;

## API

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

详情见 [react-i18next源库地址](https://github.com/i18next/react-i18next)

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ---- | ---- | -------- | -------- | -------- |
| initReactI18next | we pass the i18n instance to react-i18next which will make it available for all the components. | function | no | / | yes |
| useTranslation | It gets the t function and i18n instance inside your functional component. | function | no | / | yes |
| withTranslation | The withTranslation is a classic HOC (higher order component) and gets the t function and i18n instance inside your component via props. | function | no | / | yes |
| Translation | The Translation is a render prop and gets the t function and i18n instance to your component. | function | no | / | yes |
| Trans | The Trans component is the best way to translate a JSX tree in one translation. This enables you to eg. easily translate text containing a link component or formatting | function | no | / | yes |
| I18nextProvider | The I18nextProvider does take an i18next instance via prop i18n and passes that down using the context API. | function | no | / | yes |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/i18next/react-i18next/blob/master/LICENSE) ，请自由地享受和参与开源。
