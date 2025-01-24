<p align="center">
  <h1 align="center"> <code>@react-native-ohos-community/auto-fill</code> </h1>
</p>
<p align="center">
    <img src="https://img.shields.io/badge/platforms-%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    <a href="https://github.com/react-native-oh-library/auto-fill/blob/sig/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

Based on the HarmonyOS [autoFillManager](https://developer.huawei.com/consumer/en/doc/harmonyos-references-V5/js-apis-app-ability-autofillmanager-V5) module, auto-fill provides the feature of saving the form input data to the recent forms for automatic filling. This feature is supported only in OpenHarmony OS.

<video controls src="https://github.com/user-attachments/assets/19be83fb-2afb-4a31-9e7f-cba3848a5892" title="auto-fill-demo" width="180"></video>

## Prerequisites

1. Apply for the SmartFill service. Currently, SmartFill is in the beta phase. You can send an email to apply for access. For details about the email template, see [Application Email Template](https://developer.huawei.com/consumer/en/doc/harmonyos-guides-V5/scenario-fusion-introduction-to-smart-fill-V5#section107231967593).
2. Enable SmartFill by choosing **Settings** > **Privacy & security** > **SmartFill**.
3. Connect the device to the Internet.
4. Log in to a HUAWEI ID on the device.
5. Pass the [textContentType](https://reactnative.cn/docs/textinput#textcontenttype) attribute to the **TextInput** component on the service side.

## How to Install

Find the matching version information in the release address of the third-party library: [@react-native-ohos-community/auto-fill Releases](https://github.com/react-native-oh-library/auto-fill/releases). For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instructions:


- **npm**

  ```bash
  npm install @react-native-ohos-community/auto-fill
  ```

- **yarn**

  ```bash
  yarn add @react-native-ohos-community/auto-fill
  ```

## Description

### How to Use

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

When **AutoFill.autoSave** is called for the first time, the saving sheet that asks the user whether to save the input to recent forms is displayed.

- If the user touches the **Save** button, SmartFill is enabled and the input data is saved to the recent forms.
- If the user touches the **Ignore** button, the same device will not ask the user again within 24 hours. After the user touches the **Ignore** button for five times, the user will be prompted to choose whether they don't want to be asked again.

### When to Use

- Contact information filling: applicable to forms related to contact data such as ticket purchase information and delivery information.
- Account and password filling: applicable to forms related to the login page.
- Automatic form filling during page redirection.
- For details about the sample code, see [ContactsComponent.tsx](https://github.com/react-native-oh-library/auto-fill/blob/sig/tester/App.tsx).

> For details about the password saving and filling rules, see [Password Autofill Service](https://developer.huawei.com/consumer/en/doc/harmonyos-guides-V5/passwordvault-V5).

### The Mapping of ContentType

The following lists the mapping between [textContentType](https://reactnative.cn/docs/textinput#textcontenttype) received by the **TextInput** component in React Native and [ContentType](https://developer.huawei.com/consumer/en/doc/harmonyos-references-V5/ts-basic-components-textinput-V5#contenttype12) in HarmonyOS.

```js
// The key is the value of textContentType in React Native,
// The value is the value of ContentType in HarmonyOS.
{
    "addressCity": CITY_ADDRESS, // City
    "addressState": PROVINCE_ADDRESS, // Province
    "countryName": COUNTRY_ADDRESS, // Country
    "creditCardNumber": BANK_CARD_NUMBER, // Bank card number
    "fullStreetAddress": FULL_STREET_ADDRESS, // Detailed address
    "sublocality": DISTRICT_ADDRESS, // District/County
    "telephoneNumber": PHONE_NUMBER, // Phone number
    "username": USER_NAME, // Username
    "password": PASSWORD, // Password
    "newPassword": NEW_PASSWORD, // New password
    "houseNumber": HOUSE_NUMBER, // House number
    "districtAddress": DISTRICT_ADDRESS, // District/County
    "cityAddress": CITY_ADDRESS, // City
    "provinceAddress": PROVINCE_ADDRESS, // Province
    "countryAddress": COUNTRY_ADDRESS, // Country
    "personFullName": PERSON_FULL_NAME, // Full name
    "personLastName": PERSON_LAST_NAME, // Last name
    "personFirstName": PERSON_FIRST_NAME, // First name
    "phoneNumber": PHONE_NUMBER, // Phone number
    "phoneCountryCode": PHONE_COUNTRY_CODE, // Country code
    "fullPhoneNumber": FULL_PHONE_NUMBER, // Full phone number
    "emailAddress": EMAIL_ADDRESS, // Email address
    "bankCardNumber": BANK_CARD_NUMBER, // Bank card number
    "idCardNumber": ID_CARD_NUMBER, // ID card number
    "nickName": NICKNAME, // Nickname
    "name": PERSON_FULL_NAME, // Full name
    "familyName": PERSON_LAST_NAME, // Last name
    "givenName": PERSON_FIRST_NAME, // First name
    "detailInfoWithoutStreet": DETAIL_INFO_WITHOUT_STREET,// Detailed address without street information
    "formatAddress": FORMAT_ADDRESS, // Format address
}
```

### Link

Currently, HarmonyOS does not support AutoLink. Therefore, you need to manually configure AutoLink.

Open the **harmony** directory of the HarmonyOS project in DevEco Studio.

#### 1. 1. Adding the **overrides** Field to the **oh-package.json5** File in the Root Directory of the Project

```json
{
  "overrides": {
    "@rnoh/react-native-openharmony": "./react_native_openharmony"
  }
}
```

#### 2. 2. Introducing Native Code

Currently, two methods are available:

(1) Use the HAR file (this method will be deprecated once DevEco Studio supports the relevant functionality; currently, this is the preferred method).

(2) Directly link to the source code.

Method 1 (recommended): Use the HAR file.

> [!TIP] The HAR file is stored in the **harmony** directory in the installation path of the third-party library.

Open **entry/oh-package.json5** and add the following dependencies:

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-ohos-community/auto-fill": "file:../../node_modules/@react-native-ohos-community/auto-fill/harmony/auto_fill.har"
  }
```

Click the **sync** button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Method 2: Directly link to the source code.

For details, see [Direct Linking of Source Code](https://gitee.com/react-native-oh-library/usage-docs/blob/master/en/link-source-code.md).

#### 3. Configuring CMakeLists and Introducing AutoFillPackage

Open **entry/src/main/cpp/CMakeLists.txt** and add the following code:

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

Open **entry/src/main/cpp/PackageProvider.cpp** and add the following code:

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

#### 4. Introducing AutoFillPackage to ArkTs

Open **entry/src/main/ets/RNPackagesFactory.ts** and add the following code:

```diff
  ...
+ import { AutoFillPackage } from '@react-native-ohos-community/auto-fill/ts'

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
+   new AutoFillPackage(ctx),
  ];
}
```

## Constraints

### Compatibility

To use this library, you need to use the correct React Native and RNOH versions. In addition, use the matching DevEco Studio and the ROM on your phone.

Find the matching version information in the release address of the third-party library: [@react-native-ohos-community/auto-fill Releases](https://github.com/react-native-oh-library/auto-fill/releases)


## API Description

auto-fill exposes only the **autoSave** API, which is used to save the current form information.

| API                              | Description                         |                    Parameter                     | Return Value |
| :------------------------------- | ----------------------------------- | :----------------------------------------------: | :----------: |
| autoSave(onSuccess?, onFailure?) | Saves the current form information. | (onSuccess?: () => void, onFailure?: () => void) |     void     |

> The **autoSave** API can be invoked only once within 2 seconds on the native side. If the API is invoked multiple times, the **onFailure** callback is triggered and the message "autoSave called too frequently, please wait for 2 seconds" is displayed.


## License

This project is licensed under [Apache License 2.0](https://github.com/react-native-oh-library/auto-fill/blob/sig/LICENSE).