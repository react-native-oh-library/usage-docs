> 模板版本：v0.1.3

<p align="center">
  <h1 align="center"> <code>i18next</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/i18next/i18next/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

>[!tip] [Github 地址](https://github.com/i18next/i18next)


## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install i18next@^23.7.16 --save
```

#### **yarn**

```bash
yarn add i18next@^23.7.16
```

<!-- tabs:end -->

快速使用：

```js
import i18next from 'i18next'

i18next.init({
  fallbackLng: 'en',
  ns: ['file1', 'file2'],
  defaultNS: 'file1',
  debug: true
}, (err, t) => {
  if (err) return console.log('something went wrong loading', err);
  t('key'); // -> same as i18next.t
});

// with only callback
i18next.init((err, t) => {
  if (err) return console.log('something went wrong loading', err);
  t('key'); // -> same as i18next.t
});

// using Promises
i18next
  .init({ /* options */ })
  .then(function(t) { t('key'); });
```

## 约束与限制

### 兼容性

 在下述版本验证通过：

1. RNOH：0.72.11; SDK：OpenHarmony(api11) 4.1.0.53; IDE：DevEco Studio 4.1.3.412; ROM：2.0.0.52;
2. RNOH：0.72.13; SDK：HarmonyOS NEXT Developer Preview1; IDE：DevEco Studio 4.1.3.500; ROM：2.0.0.58;

## API

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

详情见 [i18next源库地址](https://github.com/i18next/i18next)

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ---- | ---- | -------- | -------- | -------- |
| init | The default export of the i18next module is an i18next instance ready to be initialized by calling init. | function | no | / | yes |
| use  | The use function is there to load additional plugins to i18next. | function | no | / | yes |
| t    | You can specify either one key as a String or multiple keys as an Array of String. The first one that resolves will be returned. | function | no | / | yes |
| exists  | Uses the same resolve functionality as the t function and returns true if a key exists. | function | no | / | yes |
| getFixedT  | Returns a t function that defaults to given language or namespace. | function | no | / | yes |
| changeLanguage  | Changes the language. The callback will be called as soon translations were loaded or an error occurs while loading. | function | no | / | yes |
| language | Is set to the current detected or set language. | function | no | / | yes |
| languages | Is set to an array of language codes that will be used to look up the translation value. | function | no | / | yes |
| resolvedLanguage | Is set to the current resolved language. | function | no | / | yes |
| loadNamespaces | Loads additional namespaces not defined in init options. | function | no | / | yes |
| loadLanguages | Loads additional languages not defined in init options (preload). | function | no | / | yes |
| reloadResources | Reloads resources on given state. Optionally you can pass an array of languages and namespaces as params if you don't want to reload all. | function | no | / | yes |
| setDefaultNamespace | Changes the default namespace. | function | no | / | yes |
| dir | Returns rtl or ltr depending on languages read direction. | function | no | / | yes |
| format | Exposes interpolation.formatt function added on init. | function | no | / | yes |
| createInstance | Will return a new i18next instance. | function | no | / | yes |
| cloneInstance | Creates a clone of the current instance. Shares store, plugins and initial configuration. Can be used to create an instance sharing storage but being independent on set language or default namespaces. | function | no | / | yes |
| onLanguageChanged | i18next.on('languageChanged', function(lng) {}) Gets fired when changeLanguage got called. | function | no | / | yes |
| onMissingKey | i18next.on('missingKey', function(lngs, namespace, key, res) {}) Gets fired on accessing a key not existing. Needs saveMissing set to true. | function | no | / | yes |
| onAdded | i18next.store.on('added', function(lng, ns) {}) Gets fired when resources got added. | function | no | / | yes |
| onRemoved | i18next.store.on('removed', function(lng, ns) {}) Gets fired when resources got removed. | function | no | / | yes |
| getResource | Gets one value by given key. | function | no | / | yes |
| addResource | Adds one key/value. | function | no | / | yes |
| addResources | Adds multiple key/values. | function | no | / | yes |
| addResourceBundle | Adds a complete bundle.Setting deep (default false) param to true will extend existing translations in that file. Setting deep and overwrite (default false) to true it will overwrite existing translations in that file.So omitting deep and overwrite will overwrite all existing translations with the one provided in resources. Using deep you can choose to keep existing nested translation and to overwrite those with the new ones. | function | no | / | yes |
| hasResourceBundle | Checks if a resource bundle exists. | function | no | / | yes |
| getDataByLanguage | Returns a resource data by language. | function | no | / | yes |
| getResourceBundle | Returns a resource bundle. | function | no | / | yes |
| removeResourceBundle | Removes an existing bundle. | function | no | / | yes |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/i18next/i18next/blob/master/LICENSE) ，请自由地享受和参与开源。
