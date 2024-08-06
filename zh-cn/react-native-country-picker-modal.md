> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-country-picker-modal</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-native-oh-library/react-native-country-picker-modal">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-native-oh-library/react-native-country-picker-modal/blob/master/LICENSE.md">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-country-picker-modal)

## 安装与使用

进入到工程目录并输入以下命令：

[!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-country-picker-modal@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-country-picker-modal@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```tsx
import React, {useState} from 'react';
import {
  Text,
  StyleSheet,
  PixelRatio,
  Switch,
  Button,
  ScrollView,
  View,
  ViewProps,
} from 'react-native';
import CountryPicker, {
  CountryModalProvider,
  CountryCode,
  Country,
  DARK_THEME,
} from 'react-native-country-picker-modal';

const styles = StyleSheet.create({
  container: {
    paddingVertical: 10,
    justifyContent: 'center',
    alignItems: 'center',
  },
  welcome: {
    fontSize: 17,
    textAlign: 'center',
    margin: 5,
  },
  instructions: {
    fontSize: 10,
    textAlign: 'center',
    color: '#888',
    marginBottom: 0,
  },
  data: {
    maxWidth: 250,
    padding: 10,
    marginTop: 7,
    backgroundColor: '#ddd',
    borderColor: '#888',
    borderWidth: 1 / PixelRatio.get(),
    color: '#777',
  },
  row: {
    flexDirection: 'row',
    alignItems: 'center',
  },
});

const Row = (
  props: ViewProps & {children?: React.ReactNode; fullWidth?: boolean},
) => (
  <View
    {...props}
    style={[
      styles.row,
      props.style,
      props.fullWidth && {
        width: '100%',
        justifyContent: 'space-between',
        padding: 10,
        paddingHorizontal: 50,
      },
    ]}
  />
);
interface OptionProps {
  title: string;
  value: boolean;
  onValueChange(value: boolean): void;
}
const Option = ({value, onValueChange, title}: OptionProps) => (
  <Row fullWidth>
    <Text style={styles.instructions}>{title}</Text>
    <Switch {...{value, onValueChange}} />
  </Row>
);

export function CountryPickerTest() {
  const [countryCode, setCountryCode] = useState<CountryCode>('AF');
  const [country, setCountry] = useState<Country>();
  const [withCountryNameButton, setWithCountryNameButton] =
    useState<boolean>(false);
  const [withCurrencyButton, setWithCurrencyButton] = useState<boolean>(false);
  const [withFlagButton, setWithFlagButton] = useState<boolean>(true);
  const [withCallingCodeButton, setWithCallingCodeButton] =
    useState<boolean>(false);
  const [withFlag, setWithFlag] = useState<boolean>(true);
  const [withEmoji, setWithEmoji] = useState<boolean>(true);
  const [withFilter, setWithFilter] = useState<boolean>(true);
  const [withAlphaFilter, setWithAlphaFilter] = useState<boolean>(false);
  const [withCallingCode, setWithCallingCode] = useState<boolean>(false);
  const [withCurrency, setWithCurrency] = useState<boolean>(false);
  const [withModal, setWithModal] = useState<boolean>(true);
  const [visible, setVisible] = useState<boolean>(false);
  const [dark, setDark] = useState<boolean>(false);
  const [disableNativeModal, setDisableNativeModal] = useState<boolean>(false);
  const onSelect = (country: Country) => {
    setCountryCode(country.cca2);
    setCountry(country);
  };
  const switchVisible = () => setVisible(!visible);
  return (
    <CountryModalProvider>
      <ScrollView contentContainerStyle={styles.container}>
        <Text style={styles.welcome}>Welcome to Country Picker !</Text>
        <Option
          title="With country name on button"
          value={withCountryNameButton}
          onValueChange={setWithCountryNameButton}
        />
        <Option
          title="With currency on button"
          value={withCurrencyButton}
          onValueChange={setWithCurrencyButton}
        />
        <Option
          title="With calling code on button"
          value={withCallingCodeButton}
          onValueChange={setWithCallingCodeButton}
        />
        <Option
          title="With flag"
          value={withFlag}
          onValueChange={setWithFlag}
        />
        <Option
          title="With emoji"
          value={withEmoji}
          onValueChange={setWithEmoji}
        />
        <Option
          title="With filter"
          value={withFilter}
          onValueChange={setWithFilter}
        />
        <Option
          title="With calling code"
          value={withCallingCode}
          onValueChange={setWithCallingCode}
        />
        <Option
          title="With currency"
          value={withCurrency}
          onValueChange={setWithCurrency}
        />
        <Option
          title="With alpha filter code"
          value={withAlphaFilter}
          onValueChange={setWithAlphaFilter}
        />
        <Option
          title="Without native modal"
          value={disableNativeModal}
          onValueChange={setDisableNativeModal}
        />
        <Option
          title="With modal"
          value={withModal}
          onValueChange={setWithModal}
        />
        <Option title="With dark theme" value={dark} onValueChange={setDark} />
        <Option
          title="With flag button"
          value={withFlagButton}
          onValueChange={setWithFlagButton}
        />
        <CountryPicker
          theme={dark ? DARK_THEME : {}}
          {...{
            countryCode,
            withFilter,
            excludeCountries: ['FR'],
            withFlag,
            withCurrencyButton,
            withCallingCodeButton,
            withCountryNameButton,
            withAlphaFilter,
            withCallingCode,
            withCurrency,
            withEmoji,
            withModal,
            withFlagButton,
            onSelect,
            disableNativeModal,
            preferredCountries: ['US', 'GB'],
            modalProps: {
              visible,
            },
            onClose: () => setVisible(false),
            onOpen: () => setVisible(true),
          }}
        />
        <Text style={styles.instructions}>Press on the flag to open modal</Text>
        <Button
          title={'Open modal from outside using visible props'}
          onPress={switchVisible}
        />
        {country !== null && (
          <Text style={styles.data}>{JSON.stringify(country, null, 0)}</Text>
        )}
      </ScrollView>
    </CountryModalProvider>
  );
}


```

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH: 0.72.27; SDK: HarmonyOS-Next-DB1 5.0.0.29(SP1); IDE: DevEco Studio 5.0.3.403; ROM: 3.0.0.25;


## 属性
详细请查看 [react-native-country-picker-modal的文档介绍](https://github.com/xcarpentier/react-native-country-picker-modal)

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name          | Description                           | Type                                      | Required | Platform                                | HarmonyOS Support                                        |
| ------------------ | ----------------------------------------------- | --------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| countryCode    | Country or area code. | [CountryCode](https://github.com/xcarpentier/react-native-country-picker-modal/blob/master/src/types.ts#L252)       | Yes     | All | Yes |
| region         | region code                                                  | [Region](https://github.com/xcarpentier/react-native-country-picker-modal/blob/master/src/types.ts#L272)                                           | No       | All                                         | Yes                                            |
| subregion         | subregion code | [Subregion](https://github.com/xcarpentier/react-native-country-picker-modal/blob/master/src/types.ts#L282) | No     | All                          | Yes                             |
| countryCodes         | Country Code | [CountryCode](https://github.com/xcarpentier/react-native-country-picker-modal/blob/master/src/types.ts#L252) | No     | All | Yes |
| theme        | theme | [Theme](https://github.com/xcarpentier/react-native-country-picker-modal/blob/7611d34fa35744dbec3fbcdd9b4401494b1ba8c4/src/CountryTheme.ts#L5) | No       | All | Yes |
| translation           | Translation Language Code                                    | [TranslationLanguageCode](https://github.com/xcarpentier/react-native-country-picker-modal/blob/master/src/types.ts#L309) | No     | All | Yes |
| modalProps       | ModalProps | [ModalProps](https://facebook.github.io/react-native/docs/modal#props) | No       | All | Yes |
| filterProps              | CountryFilterProps | [CountryFilterProps](https://facebook.github.io/react-native/docs/textinput#props) | No        | All | Yes |
| flatListProps        | extends flatListProps | [FlatListProps<Country>](https://facebook.github.io/react-native/docs/flatlist#props) | No        | All | Yes |
| withAlphaFilter   | Use AlphaFilter                        | boolean                                       | No        | All | Yes |
| withCallingCode  | Using the CallingCode                  | boolean                                       | No        | All | Yes |
| withCurrency  | Use Currency                                          | boolean                                                      | No        | All | Yes |
| withEmoji              | Use Emoji                       | boolean                                | No        | All | Yes |
| withCountryNameButton     | Use the button with the country name                  | boolean                                                      | No        | All | Yes |
| withCurrencyButton          | Using the With Currency Button     | boolean                                   | No        | All | Yes |
| withCallingCodeButton          | Using the With Call Code Button    | boolean                                   | No        | All | Yes |
| withFlagButton         | Using Flagged Buttons              | boolean                                   | No        | All | Yes |
| withCloseButton          | Using the Close Button         | boolean                               | No        | All | Yes |
| withFilter          | withFilter                         | boolean                                   | No        | All | Yes |
| withFlag | withFlag                     | boolean                                | No        | All | Yes |
| withModal      | withModal                              | boolean                                | No        | All | Yes |
| visible        | visible                                               | boolean                                                      | No        | All | Yes |
| containerButtonStyle             | containerButtonStyle | StyleProp<ViewStyle>                     | No        | All | Yes |
| renderFlagButton        | renderFlagButton | (props: (FlagButton['props'])): ReactNode ([FlagButton props](https://github.com/xcarpentier/react-native-country-picker-modal/blob/master/src/FlagButton.tsx#L73)) | No        | All | Yes |
| renderCountryFilter   | renderCountryFilter | (props: CountryFilter['props']): ReactNode ([CountryFilter props is TextInputProps](https://facebook.github.io/react-native/docs/textinput#props)) | No        | All | Yes |
| onSelect  | onSelect | (country: Country): void ([Country](https://github.com/xcarpentier/react-native-country-picker-modal/blob/master/src/types.ts#L263)) | Yes     | All | Yes |
| onOpen  | onOpen | (): void | Yes  | All | Yes |
| onClose            | onClose                          | (): void                                 | Yes     | All | Yes |
| closeButtonImage   | Source of the close button | [ImageSourcePropType](https://facebook.github.io/react-native/docs/image#props) | No        | All | Yes |
| closeButtonStyle         | closeButtonStyle    | StyleProp<ViewStyle>                    | No        | All | Yes |
| closeButtonImageStyle | closeButtonImageStyle | StyleProp<ViewStyle>          | No        | All | Yes |
| disableNativeModal     | you have to wrap your all app with CountryModalProvider | boolean | No        | All | Yes |
| preferredCountries    | preferredCountries | [CountryCode](https://github.com/xcarpentier/react-native-country-picker-modal/blob/master/src/types.ts#L254) preferred countries they appear first (`withAlphaFilter` must be false) | No        | All | Yes |


## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/xcarpentier/react-native-country-picker-modal/blob/master/LICENSE.md) ，请自由地享受和参与开源。
