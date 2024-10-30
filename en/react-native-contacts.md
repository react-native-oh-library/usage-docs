> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-contacts</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/morenoh149/react-native-contacts">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
        <a href="https://github.com/morenoh149/react-native-contacts/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!tip] [GitHub address](https://github.com/react-native-oh-library/react-native-contacts)

## Installation and Usage

Find the matching version information in the release address of a third-party library and download an applicable .tgz package: [@react-native-oh-tpl/react-native-contacts Releases](https://github.com/react-native-oh-library/react-native-contacts/releases).

Go to the project directory and execute the following instruction:

> [!TIP] Replace the content with the path of the .tgz package at the comment sign (#).

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-contacts@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-contacts@file:#
```

<!-- tabs:end -->

Quick use:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React, { useState } from "react";
import { ScrollView, Button, Alert } from "react-native";
import Contacts from "react-native-contacts";

export const ContactsDemo = () => {
  let emailAddress: Contacts.EmailAddress = {
    label: "emailAddress",
    email: "test@163.com",
  };
  let phoneNumber: Contacts.PhoneNumber = {
    label: "phoneNumber",
    number: "13142536789",
  };

  let postalAddress: Contacts.PostalAddress = {
    label: "label",
    formattedAddress: "formattedAddress",
    street: "street",
    pobox: "pobox",
    neighborhood: "neighborhood",
    city: "city",
    region: "region",
    state: "state",
    postCode: "postCode",
    country: "country",
  };

  let birthday: Contacts.Birthday = {
    day: 1,
    month: 5,
    year: 2024,
  };

  let instantMessageAddress: Contacts.InstantMessageAddress = {
    username: "username",
    service: "service",
  };

  let urlAddress: Contacts.UrlAddress = {
    url: "url",
    label: "label",
  };
  let contact: Contacts.Contact = {
    company: "addcompany",
    emailAddresses: [emailAddress],
    displayName: "adddisplayName",
    familyName: "addfamilyName",
    givenName: "addgivenName",
    middleName: "addmiddleName",
    jobTitle: "addjobTitle",
    phoneNumbers: [phoneNumber],
    hasThumbnail: false,
    thumbnailPath: "addthumbnailPath",
    isStarred: false,
    postalAddresses: [postalAddress],
    prefix: "addprefix",
    suffix: "addsuffix",
    department: "adddepartment",
    birthday: birthday,
    imAddresses: [instantMessageAddress],
    urlAddresses: [urlAddress],
    note: "addnote",
  };

  return (
    <ScrollView>
      <Button
        title="requestPermission"
        onPress={() => {
          Contacts.requestPermission().then((data) => {
            console.log(`requestPermission:${JSON.stringify(data)}`);
            Alert.alert(`requestPermission:${JSON.stringify(data)}`);
          });
        }}
      />
      <Button
        title="checkPermission"
        onPress={() => {
          Contacts.checkPermission().then((data) => {
            console.log(`checkPermission:${JSON.stringify(data)}`);
            Alert.alert(`checkPermission:${JSON.stringify(data)}`);
          });
        }}
      />
      <Button
        title="getAll"
        onPress={() => {
          Contacts.getAll().then((contacts: Contacts.Contact[]) => {
            console.log(`getAll:${JSON.stringify(contacts)}`);
          });
        }}
      />
      <Button
        title="getAllWithoutPhotos"
        onPress={() => {
          Contacts.getAllWithoutPhotos().then(
            (contacts: Contacts.Contact[]) => {
              console.log(`getAllWithoutPhotos:${JSON.stringify(contacts)}`);
            }
          );
        }}
      />
      <Button
        title="getContactById"
        onPress={() => {
          Contacts.getContactById("1").then(
            (contact: Contacts.Contact | null) => {
              console.log(`getContactById:${JSON.stringify(contact)}`);
            }
          );
        }}
      />
      <Button
        title="getCount"
        onPress={() => {
          Contacts.getCount().then((count: number) => {
            console.log(`getCount:${count}`);
          });
        }}
      />
      <Button
        title="getPhotoForId"
        onPress={() => {
          Contacts.getPhotoForId("1").then((photoUrl: string) => {
            console.log(`getPhotoForId:${photoUrl}`);
          });
        }}
      />
      <Button
        title="addContact"
        onPress={() => {
          Contacts.addContact(contact).then((contact: Contacts.Contact) => {
            console.log(`addContact:${JSON.stringify(contact)}`);
          });
        }}
      />

      <Button
        title="openContactForm"
        onPress={() => {
          Contacts.openContactForm(contact).then(
            (contact: Contacts.Contact) => {
              console.log(`openContactForm:${JSON.stringify(contact)}`);
              Alert.alert(`openContactForm success`);
            }
          );
        }}
      />
      <Button
        title="openExistingContact"
        onPress={() => {
          Contacts.openExistingContact({
            recordID: "1",
            phoneNumbers: [
              {
                label: "phoneNumber2",
                number: "13521456721",
              },
            ],
          }).then((contact: Contacts.Contact) => {
            console.log(`openExistingContact:${JSON.stringify(contact)}`);
            Alert.alert(`openExistingContact success`);
          });
        }}
      />
      <Button
        title="viewExistingContact"
        onPress={() => {
          Contacts.viewExistingContact({
            recordID: "1",
            phoneNumbers: [
              {
                label: "phoneNumber2",
                number: "13521456721",
              },
            ],
          }).then((contact: Contacts.Contact) => {
            console.log(`viewExistingContact:${JSON.stringify(contact)}`);
            Alert.alert(`viewExistingContact success`);
          });
        }}
      />
      <Button
        title="editExistingContact"
        onPress={() => {
          Contacts.editExistingContact({
            recordID: "1",
            phoneNumbers: [
              {
                label: "phoneNumber2",
                number: "13521456721",
              },
            ],
          }).then((contact: Contacts.Contact) => {
            console.log(`editExistingContact:${JSON.stringify(contact)}`);
            Alert.alert(`editExistingContact success`);
          });
        }}
      />
      <Button
        title="updateContact"
        onPress={() => {
          Contacts.updateContact({
            recordID: "1",
            familyName: "updateContact",
            givenName: "updateContact",
            phoneNumbers: [
              {
                label: "phoneNumber2",
                number: "13521456721",
              },
              {
                label: "phoneNumber3",
                number: "13521456222",
              },
            ],
          }).then(() => {
            Alert.alert(`updateContact success`);
          });
        }}
      />
      <Button
        title="deleteContact"
        onPress={() => {
          Contacts.deleteContact({
            recordID: "3",
          }).then(() => {
            Alert.alert(`deleteContact success`);
          });
        }}
      />
      <Button
        title="getContactsMatchingString"
        onPress={() => {
          Contacts.getContactsMatchingString("addfamilyName").then(
            (contacts: Contacts.Contact[]) => {
              console.log(
                `getContactsMatchingString:${JSON.stringify(contacts)}`
              );
            }
          );
        }}
      />
      <Button
        title="getContactsByPhoneNumber"
        onPress={() => {
          Contacts.getContactsByPhoneNumber("789").then(
            (contacts: Contacts.Contact[]) => {
              console.log(
                `getContactsByPhoneNumber:${JSON.stringify(contacts)}`
              );
            }
          );
        }}
      />
      <Button
        title="getContactsByEmailAddress"
        onPress={() => {
          Contacts.getContactsByEmailAddress("test@163.com").then(
            (contacts: Contacts.Contact[]) => {
              console.log(
                `getContactsByEmailAddress:${JSON.stringify(contacts)}`
              );
            }
          );
        }}
      />
      <Button
        title="writePhotoToPath"
        onPress={() => {
          Contacts.writePhotoToPath("1", "file").then((data) => {
            console.log(`writePhotoToPath:${JSON.stringify(data)}`);
          });
        }}
      />
      <Button
        title="iosEnableNotesUsage"
        onPress={() => {
          Contacts.iosEnableNotesUsage(true);
          console.log(`iosEnableNotesUsage:true`);
        }}
      />
    </ScrollView>
  );
};
```

## Use Codegen

If this repository has been adapted to `Codegen`, generate the bridge code of the third-party library by using the `Codegen`. For details, see [Codegen Usage Guide](/zh-cn/codegen.md).

## Link

Currently, HarmonyOS does not support AutoLink. Therefore, you need to manually configure the linking.

Open the `harmony` directory of the HarmonyOS project in DevEco Studio.

### 1. Adding the overrides Field to oh-package.json5 File in the Root Directory of the Project

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "./react_native_openharmony"
  }
}
```

### 2. Introducing Native Code

Currently, two methods are available:

Method 1 (recommended): Use the HAR file.

> [!TIP] The HAR file is stored in the `harmony` directory in the installation path of the third-party library.

Open `entry/oh-package.json5` file and add the following dependencies:

```json
"dependencies": {
    "@rnoh/react-native-openharmony" : "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-contacts": "file:../../node_modules/@react-native-oh-tpl/react-native-contacts/harmony/contacts.har"
  }
```

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Method 2: Directly link to the source code.

> [!TIP] For details, see [Directly Linking Source Code](/zh-cn/link-source-code.md).

### 3. Introducing ContactsPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+ import {ContactsPackage} from '@react-native-oh-tpl/react-native-contacts/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [new SamplePackage(ctx),
+   new ContactsPackage(ctx)];
}
```

### 4. Running

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Then build and run the code.

## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-contacts Releases](https://github.com/react-native-oh-library/react-native-contacts/releases)

### Permission Requirements

[!tip] "ohos.permission.READ_CONTACTS"，"ohos.permission.WRITE_CONTACTS"权限等级为<B>system_basic</B>，授权方式为<B>user_grant</B>，[使用 ACL 签名的配置指导](https://developer.harmonyos.com/cn/docs/documentation/doc-guides-V3/signing-0000001587684945-V3#section157591551175916)

Open the `entry/src/main/module.json5` file and add the following code:

```json
"requestPermissions": [
     ...
     {
        "name": "ohos.permission.READ_CONTACTS",
        "reason": "$string:read_contacts_reason",
        "usedScene": {
          "abilities": [
            "EntryAbility"
          ],
          "when": "always"
        }
      },
      {
        "name": "ohos.permission.WRITE_CONTACTS",
        "reason": "$string:write_contacts_reason",
        "usedScene": {
          "abilities": [
            "EntryAbility"
          ],
          "when": "always"
        }
      }
]
```

## API

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                                                                         | Description                                                                                                                                        | Type     | Required | Platform    | HarmonyOS Support |
| ---------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | ----------- | ----------------- |
| getAll: Promise<Contact[]>                                                   | returns all contacts as an array of objects                                                                                                        | function | no       | android,ios | yes               |
| getAllWithoutPhotos:Promise<Contact[]>                                       | same as `getAll` on Android, but on iOS it will not return uris for contact photos (because there's a significant overhead in creating the images) | function | no       | android,ios | yes               |
| getContactById(contactId): Promise<Contact>                                  | returns contact with defined contactId (or null if it doesn't exist)人                                                                             | function | no       | android,ios | yes               |
| getCount(): Promise<number>                                                  | returns the number of contacts                                                                                                                     | function | no       | android,ios | yes               |
| getPhotoForId(contactId: string): Promise<string>                            | Promise - returns a URI (or null) for a contacts photoURL                                                                                          | function | no       | android,ios | yes               |
| addContact(contact: Partial<Contact>): Promise<Contact>                      | adds a contact to the AddressBook                                                                                                                  | function | no       | android,ios | yes               |
| openContactForm(contact: Partial<Contact>): Promise<Contact \| null>         | create a new contact and display in contactsUI 面                                                                                                  | function | no       | android,ios | partially         |
| openExistingContact(contact: Contact): Promise<Contact>                      | open existing contact (edit mode), where contact is an object with a valid recordID                                                                | function | no       | android,ios | partially         |
| viewExistingContact(contact: { recordID: string })                           | open existing contact (view mode), where contact is an object with a valid recordID 面                                                             | function | no       | android,ios | partially         |
| editExistingContact(contact: Contact): Promise<Contact>                      | add numbers to the contact, where the contact is an object with a valid recordID and an array of phoneNumbers 面                                   | function | no       | android,ios | no                |
| updateContact(contact: Partial<Contact> & {recordID: string}): Promise<void> | where contact is an object with a valid recordID                                                                                                   | function | no       | android,ios | yes               |
| deleteContact(contact: Contact): Promise<void>                               | where contact is an object with a valid recordID                                                                                                   | function | no       | android,ios | yes               |
| getContactsMatchingString(str: string): Promise<Contact[]>                   | where string is any string to match a name (first, middle, family) to                                                                              | function | no       | android,ios | yes               |
| getContactsByPhoneNumber(phoneNumber: string): Promise<Contact[]>            | where string is a phone number to match to.                                                                                                        | function | no       | android,ios | yes               |
| getContactsByEmailAddress(emailAddress: string): Promise<Contact[]>          | where string is an email address to match to.                                                                                                      | function | no       | android,ios | yes               |
| checkPermission(): Promise<'authorized' \| 'denied' \| 'undefined'>;         | checks permission to access Contacts ios only                                                                                                      | function | no       | ios         | yes               |
| requestPermission(): Promise<'authorized' \| 'denied' \| 'undefined'>        | request permission to access Contacts ios only                                                                                                     | function | no       | ios         | yes               |
| writePhotoToPath(contactId: string, file: string): Promise<boolean>          | writes the contact photo to a given path android only                                                                                              | function | no       | android     | no                |

**Contacts**
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| recordID | 联系人 id | string | no | android,ios | yes |
| backTitle | 返回键标题 | string | no | android,ios | no |
| company | 公司 | string|null | no | android,ios | yes |
| emailAddresses | 电子邮箱地址 | EmailAddress[] | no | android,ios | yes |
| displayName | 展示名 | string | no | android,ios | yes |
| familyName | 姓氏 | string | no | android,ios | yes |
| givenName | 名字 | string | no | android,ios | yes |
| middleName | 中间名 | string | no | android,ios | yes |
| jobTitle | 职位名称 | string | no | android,ios | yes |
| phoneNumbers | 电话号码 | PhoneNumber[] | no | android,ios | yes |
| hasThumbnail | 有头像 | boolean | no | android,ios | np |
| thumbnailPath | 头像地址 | string | no | android,ios | no |
| isStarred | 是否标记 | boolean | no | android,ios | yes |
| postalAddresses | 邮件地址 | PostalAddress[] | no | android,ios | yes |
| prefix | 前缀 | string | no | android,ios | yes |
| suffix | 后缀 | string | no | android,ios | yes |
| department | 部门 | string | no | android,ios | yes |
| birthday | 生日 | Birthday | no | android,ios | yes |
| imAddresses | 即时消息地址 | InstantMessageAddress[] | no | android,ios | yes |
| urlAddresses | 图片地址 | UrlAddress[] | no | android,ios | no |
| note | 备注 | string | no | android,ios | yes |

**EmailAddress**
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| label | 标题 | string | no | android,ios | yes |
| email | 地址 | string | no | android,ios | yes |

**PhoneNumber**
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| label | 标题 | string | no | android,ios | yes |
| number | 号码 | string | no | android,ios | yes |

**PostalAddress**
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| label | 标题 | string | no | android,ios | yes |
| formattedAddress | 格式化地址 | string | no | android,ios | yes |
| street | 街道 | string | no | android,ios | yes |
| pobox | 信箱 | string | no | android,ios | yes |
| neighborhood | 邻域 | string | no | android,ios | yes |
| city | 城市 | string | no | android,ios | yes |
| region | 区域 | string | no | android,ios | yes |
| state | 州 | string | no | android,ios | yes |
| postCode | 邮政编码 | string | no | android,ios | yes |
| country | 国家/地区 | string | no | android,ios | yes |

**InstantMessageAddress**
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| username | 用户名 | string | no | android,ios | no |
| service | 服务地址 | string | no | android,ios | no |

**Birthday**
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| day | 年 | number | no | android,ios | yes |
| month | 月 | number | no | android,ios | yes |
| year | 日 | number | no | android,ios | yes |

**UrlAddress**
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| url | 路径 | string | no | android,ios | yes |
| label | 标题 | string | no | android,ios | yes |

## Known Issues

- [ ] openContactForm: 跳转到系统联系人界面只支持姓名和电话参数传递，需要系统联系人应用支持所有属性，另外创建成功之后无法返回联系人信息，联系人应用目前不支持。[issue#1](https://github.com/react-native-oh-library/react-native-contacts/issues/1)
- [ ] openExistingContact: 联系人应用新增和编辑是同一个界面，目前参数只支持姓名和电话传递，编辑成功之后也无法拿到联系人信息[issue#1](https://github.com/react-native-oh-library/react-native-contacts/issues/1)
- [ ] viewExistingContact: 查看界面只有姓名和电话信息，需要联系人应用补齐所有属性[issue#1](https://github.com/react-native-oh-library/react-native-contacts/issues/1)
- [ ] editExistingContact: 没有单独的只支持编辑电话号码的页面，目前同编辑页面[issue#1](https://github.com/react-native-oh-library/react-native-contacts/issues/1)
- [ ] writePhotoToPath: 系统联系人应用不支持[issue#1](https://github.com/react-native-oh-library/react-native-contacts/issues/1)

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/morenoh149/react-native-contacts/blob/master/LICENSE).
