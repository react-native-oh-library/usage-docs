<p align="center">
  <h1 align="center"> <code>@react-native-ohos-community/auto-fill</code> </h1>
</p>
<p align="center">
    <img src="https://img.shields.io/badge/platforms-%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    <a href="https://github.com/react-native-oh-library/auto-fill/blob/sig/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

auto-fill 基于 HarmonyOS [autoFillManager](https://developer.huawei.com/consumer/cn/doc/harmonyos-references-V5/js-apis-app-ability-autofillmanager-V5) 模块，提供将表单输入数据保存到历史表单输入中，以供下次自动填充的功能，仅支持 ohos 平台。

<video controls src="https://github.com/user-attachments/assets/19be83fb-2afb-4a31-9e7f-cba3848a5892" title="auto-fill-demo" width="180"></video>

## 前提条件

1. **申请接入智能填充服务** 。当前智能填充处于 Beta 阶段，您可通过发送邮件的方式进行申请接入。邮件模板可参考 [智能填充概述-申请接入智能填充服务](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides-V5/scenario-fusion-introduction-to-smart-fill-V5#section1167564853816)
2. 设备智能填充开关必须处于打开状态，请前往“设置 > 隐私和安全 > 智能填充”打开。  
3. 设备已连接互联网。
4. 设备需要登录华为账号。
5. 业务侧需要给 `TextInput` 组件传入 [`textContentType`](https://reactnative.cn/docs/textinput#textcontenttype) 属性。

## 安装

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-ohos-community/auto-fill Releases](https://github.com/react-native-oh-library/auto-fill/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

- **npm**
  ```bash
  npm install @react-native-ohos-community/auto-fill@file:#
  ```
- **yarn**
  ```bash
  yarn add @react-native-ohos-community/auto-fill@file:#
  ```

## 使用说明

### 基本用法

```tsx
import React, { useState } from 'react';
import { View, TextInput, Button, StyleSheet } from 'react-native';
import AutoFill from '@react-native-ohos-community/auto-fill';

const MyFormComponent = () => {
  const [fullName, setFullName] = useState('');
  const [phoneNumber, setPhoneNumber] = useState('');

  const handleSubmit = () => {
    AutoFill.autoSave(
      () => {
        console.log('AutoFillTurboModule success in js is been called');
      },
      () => {
        console.log('AutoFillTurboModule failed in js is been called');
      }
    );
  };

  return (
    <View style={styles.container}>
      <TextInput
        style={styles.input}
        placeholder="Full Name"
        value={fullName}
        onChangeText={setFullName}
        autoCapitalize="words"
        textContentType="name"
      />
      <TextInput
        style={styles.input}
        placeholder="Phone Number"
        value={phoneNumber}
        onChangeText={setPhoneNumber}
        keyboardType="phone-pad"
        textContentType="telephoneNumber"
      />

      <Button title="Submit" onPress={handleSubmit} />
    </View>
  );
};

export default MyFormComponent;
```

初次调用 `AutoFill.autoSave` 将弹出“保存至历史表单输入”半模态窗。

- 点击 “保存信息” 按钮之后，智能填充开关会打开并将表单输入数据保存到历史表单输入中。
- 点击 “忽略” 按钮后，该设备 24 小时之内不会再次询问。该设备累计忽略 5 次后，半模态中将显示“忽略后不再询问”勾选框，勾选之后点击“忽略”按钮，后续将不再询问。

### 常见使用场景

- 联系人信息填充: 适用于如购票信息、收货信息等联系人数据相关表单
- 账号密码填充：适用于如登录界面相关表单
- 页面跳转时表单自动填充
- 示例代码可查看 [ContactsComponent.tsx](https://github.com/react-native-oh-library/auto-fill/blob/sig/tester/App.tsx)

> 具体密码保存与填充规则请参考：[密码自动填充服务](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides-V5/passwordvault-V5)

### ContentType 对应关系

React-Native 侧 TextInput 组件接收的 [textContentType](https://reactnative.cn/docs/textinput#textcontenttype) 类型与 HarmonyOS 中 [ContentType](https://developer.huawei.com/consumer/cn/doc/harmonyos-references-V5/ts-basic-components-textinput-V5#contenttype12%E6%9E%9A%E4%B8%BE%E8%AF%B4%E6%98%8E) 类型映射关系如下，可供参考。

```js
// key 值为 RN 侧 textContentType 值,
// value 值为 HarmonyOS 侧 ContentType 值
{
    "addressCity": CITY_ADDRESS,  // 市
    "addressState": PROVINCE_ADDRESS, // 省
    "countryName": COUNTRY_ADDRESS, // 国家
    "creditCardNumber": BANK_CARD_NUMBER, // 银行卡号
    "fullStreetAddress": FULL_STREET_ADDRESS, // 详细地址
    "sublocality": DISTRICT_ADDRESS, // 区/县
    "telephoneNumber": PHONE_NUMBER, // 手机号码
    "username": USER_NAME, // 用户名
    "password": PASSWORD, // 密码
    "newPassword": NEW_PASSWORD, // 新密码
    "houseNumber": HOUSE_NUMBER, // 门牌号
    "districtAddress": DISTRICT_ADDRESS, // 区/县
    "cityAddress": CITY_ADDRESS,    // 市
    "provinceAddress": PROVINCE_ADDRESS,   // 省
    "countryAddress": COUNTRY_ADDRESS, // 国家
    "personFullName": PERSON_FULL_NAME, // 姓名
    "personLastName": PERSON_LAST_NAME, // 姓氏
    "personFirstName": PERSON_FIRST_NAME, // 名字
    "phoneNumber": PHONE_NUMBER, // 手机号码
    "phoneCountryCode": PHONE_COUNTRY_CODE, // 国家代码
    "fullPhoneNumber": FULL_PHONE_NUMBER, // 包含国家代码的手机号码
    "emailAddress": EMAIL_ADDRESS, // 邮箱地址
    "bankCardNumber": BANK_CARD_NUMBER, // 银行卡号
    "idCardNumber": ID_CARD_NUMBER, // 身份证号
    "nickName": NICKNAME, // 昵称
    "name": PERSON_FULL_NAME, // 姓名
    "familyName": PERSON_LAST_NAME, // 姓氏
    "givenName": PERSON_FIRST_NAME, // 名字
    "detailInfoWithoutStreet": DETAIL_INFO_WITHOUT_STREET,// 无街道地址
    "formatAddress": FORMAT_ADDRESS, // 标准地址
}
```

### Link

目前 HarmonyOS 暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`

#### 1. 在 harmony 工程根目录的 `oh-package.json5` 添加 overrides 字段

```json
{
  "overrides": {
    "@rnoh/react-native-openharmony": "./react_native_openharmony"
  }
}
```

#### 2. 引入原生端代码

目前有两种方法：

（1）通过 har 包引入（在 IDE 完善相关功能后该方法会被遗弃，目前首选此方法）；

（2）直接链接源码。

方法 一：通过 har 包引入（推荐）

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-ohos-community/auto-fill": "file:../../node_modules/@react-native-ohos-community/auto-fill/harmony/auto_fill.har"
  }
```

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

方法 二：直接链接源码

如需使用直接链接源码，请参考[直接链接源码](https://gitee.com/react-native-oh-library/usage-docs/blob/master/zh-cn/link-source-code.md)说明

#### 3. 配置 CMakeLists 和引入 AutoFillPackage

打开 `entry/src/main/cpp/CMakeLists.txt`，添加：

```diff
project(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(CMAKE_SKIP_BUILD_RPATH TRUE)
...
+ set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
set(RNOH_CPP_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../../react-native-harmony/harmony/cpp")
set(LOG_VERBOSITY_LEVEL 1)

# RNOH_BEGIN: manual_package_linking_1
+ add_subdirectory("${OH_MODULES}/@react-native-ohos-community/auto-fill/src/main/cpp" ./auto-fill)
# RNOH_END: manual_package_linking_1

add_library(rnoh_app SHARED
    ${GENERATED_CPP_FILES}
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)

# RNOH_BEGIN: manual_package_linking_2
+ target_link_libraries(rnoh_app PUBLIC auto_fill)
# RNOH_END: manual_package_linking_2
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
+ #include "AutoFillPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(
    Package::Context ctx) {
  return {
+       std::make_shared<AutoFillPackage>(ctx),
  };
}
```

#### 4. 在 ArkTs 侧引入 AutoFillPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import { AutoFillPackage } from '@react-native-ohos-community/auto-fill/ts'

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
+   new AutoFillPackage(ctx),
  ];
}
```

## 约束与限制
### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-ohos-community/auto-fill Releases](https://github.com/react-native-oh-library/auto-fill/releases)


## API 接口说明

auto-fill 仅暴露一个 autoSave 接口，用于保存当前表单信息

| API                              | 说明             |                       入参                       | 返回值 |
| :------------------------------- | ---------------- | :----------------------------------------------: | :----: |
| autoSave(onSuccess?, onFailure?) | 保存当前表单信息 | (onSuccess?: () => void, onFailure?: () => void) |  void  |

> autoSave 方法在 native 侧限制 2s 内只能调用一次，多次调用将触发 onFailure 回调，并输出 `autoSave called too frequently, please wait for 2 seconds.`


## 开源协议

本项目基于 [Apache License 2.0](https://github.com/react-native-oh-library/auto-fill/blob/sig/LICENSE) ，请自由地享受和参与开源。
