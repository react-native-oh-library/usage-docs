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

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-contacts)

## Installation and Usage

Find the matching version information in the release address of a third-party library: [@react-native-oh-tpl/react-native-contacts Releases](https://github.com/react-native-oh-library/react-native-contacts/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:



<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-contacts
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-contacts
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

> [!TIP] For details, see [Directly Linking Source Code](/en/link-source-code.md).

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

[!TIP] The permission level of "ohos.permission.READ_CONTACTS" and "ohos.permission.WRITE_CONTACTS" is **system_basic**, and the authorization mode is **user_grant**. For details, see [Requesting ACL Permissions](https://developer.huawei.com/consumer/en/doc/harmonyos-guides-V2/signing-0000001587684945-V2#section157591551175916)

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

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                                                         | Description                                                  | Type     | Required | Platform    | HarmonyOS Support |
| ------------------------------------------------------------ | ------------------------------------------------------------ | -------- | -------- | ----------- | ----------------- |
| getAll: Promise<Contact[]>                                   | returns all contacts as an array of objects                  | function | no       | Android,iOS | yes               |
| getAllWithoutPhotos:Promise<Contact[]>                       | same as `getAll` on Android, but on iOS it will not return uris for contact photos (because there's a significant overhead in creating the images) | function | no       | Android,iOS | yes               |
| getContactById(contactId): Promise<Contact>                  | returns contact with defined contactId (or null if it doesn't exist) | function | no       | Android,iOS | yes               |
| getCount(): Promise<number>                                  | returns the number of contacts                               | function | no       | Android,iOS | yes               |
| getPhotoForId(contactId: string): Promise<string>            | Promise - returns a URI (or null) for a contacts photoURL    | function | no       | Android,iOS | yes               |
| addContact(contact: Partial<Contact>): Promise<Contact>      | adds a contact to the AddressBook                            | function | no       | Android,iOS | yes               |
| openContactForm(contact: Partial<Contact>): Promise<Contact \| null> | create a new contact and display in contactsUI               | function | no       | Android,iOS | partially         |
| openExistingContact(contact: Contact): Promise<Contact>      | open existing contact (edit mode), where contact is an object with a valid recordID | function | no       | Android,iOS | partially         |
| viewExistingContact(contact: { recordID: string })           | open existing contact (view mode), where contact is an object with a valid recordID | function | no       | Android,iOS | partially         |
| editExistingContact(contact: Contact): Promise<Contact>      | add numbers to the contact, where the contact is an object with a valid recordID and an array of phoneNumbers | function | no       | Android,iOS | no                |
| updateContact(contact: Partial<Contact> & {recordID: string}): Promise<void> | where contact is an object with a valid recordID             | function | no       | Android,iOS | yes               |
| deleteContact(contact: Contact): Promise<void>               | where contact is an object with a valid recordID             | function | no       | Android,iOS | yes               |
| getContactsMatchingString(str: string): Promise<Contact[]>   | where string is any string to match a name (first, middle, family) to | function | no       | Android,iOS | yes               |
| getContactsByPhoneNumber(phoneNumber: string): Promise<Contact[]> | where string is a phone number to match to.                  | function | no       | Android,iOS | yes               |
| getContactsByEmailAddress(emailAddress: string): Promise<Contact[]> | where string is an email address to match to.                | function | no       | Android,iOS | yes               |
| checkPermission(): Promise<'authorized' \| 'denied' \| 'undefined'>; | checks permission to access Contacts ios only                | function | no       | iOS         | yes               |
| requestPermission(): Promise<'authorized' \| 'denied' \| 'undefined'> | request permission to access Contacts ios only               | function | no       | iOS         | yes               |
| writePhotoToPath(contactId: string, file: string): Promise<boolean> | writes the contact photo to a given path android only        | function | no       | Android     | no                |

**Contacts**
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| recordID | Contact ID| string | no | Android,iOS | yes |
| backTitle | Back button title| string | no | Android,iOS | no |
| company | Company| string|no | Android,iOS | yes |
| emailAddresses | Email addresses.| EmailAddress[] | no | Android,iOS | yes |
| displayName | Display name| string | no | Android,iOS | yes |
| familyName | Family name| string | no | Android,iOS | yes |
| givenName | Given name| string | no | Android,iOS | yes |
| middleName | Middle name| string | no | Android,iOS | yes |
| jobTitle | Job title| string | no | Android,iOS | yes |
| phoneNumbers | Phone numbers.| PhoneNumber[] | no | Android,iOS | yes |
| hasThumbnail | Whether a contact has a thumbnail.| boolean | no | Android,iOS | no |
| thumbnailPath | Thumbnail path| string | no | Android,iOS | no |
| isStarred | Whether a contact is starred.| boolean | no | Android,iOS | yes |
| postalAddresses | Postal addresses.| PostalAddress[] | no | Android,iOS | yes |
| prefix | Prefix| string | no | Android,iOS | yes |
| suffix | Suffix| string | no | Android,iOS | yes |
| department | Department| string | no | Android,iOS | yes |
| birthday | Birthday| Birthday | no | Android,iOS | yes |
| imAddresses | Instant message addresses.| InstantMessageAddress[] | no | Android,iOS | yes |
| urlAddresses | Image addresses.| UrlAddress[] | no | Android,iOS | no |
| note | Note| string | no | Android,iOS | yes |

**EmailAddress**
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| label | Title| string | no | Android,iOS | yes |
| email | Address| string | no | Android,iOS | yes |

**PhoneNumber**
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| label | Title| string | no | Android,iOS | yes |
| number | Number| string | no | Android,iOS | yes |

**PostalAddress**
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| label | Title| string | no | Android,iOS | yes |
| formattedAddress | Formatted address| string | no | Android,iOS | yes |
| street | Street| string | no | Android,iOS | yes |
| pobox | Postal box| string | no | Android,iOS | yes |
| neighborhood | Neighborhood| string | no | Android,iOS | yes |
| city | City| string | no | Android,iOS | yes |
| region | Region| string | no | Android,iOS | yes |
| state | State| string | no | Android,iOS | yes |
| postCode | Postal code| string | no | Android,iOS | yes |
| country | Country/Region| string | no | Android,iOS | yes |

**InstantMessageAddress**
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| username | User name| string | no | Android,iOS | no |
| service | Service address| string | no | Android,iOS | no |

**Birthday**
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| day | Day| number | no | Android,iOS | yes |
| month | Month| number | no | Android,iOS | yes |
| year | Year| number | no | Android,iOS | yes |

**UrlAddress**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| url | Path| string | no | Android,iOS | yes |
| label | Title| string | no | Android,iOS | yes |

## Known Issues

- [ ] **openContactForm**: Currently, only the name and phone number parameters can be passed to the system contact page, and the contact information cannot be returned after a contact is created. The system contact application must support all properties.[issue#1](https://github.com/react-native-oh-library/react-native-contacts/issues/1)
- [ ] **openExistingContact**: Currently, the same page is used for adding and editing contacts, and only the name and phone number can be passed. After the contact is edited, the contact information cannot be obtained. [issue#1](https://github.com/react-native-oh-library/react-native-contacts/issues/1)
- [ ] **viewExistingContact**: Only the name and phone number are displayed on the viewing page. The contact application needs to support all properties. [issue#1](https://github.com/react-native-oh-library/react-native-contacts/issues/1)
- [ ] **editExistingContact**: There is no independent page for editing only phone numbers. [issue#1](https://github.com/react-native-oh-library/react-native-contacts/issues/1)
- [ ] **writePhotoToPath**: The system contact application does not support this API. [issue#1](https://github.com/react-native-oh-library/react-native-contacts/issues/1)

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/morenoh149/react-native-contacts/blob/master/LICENSE).
