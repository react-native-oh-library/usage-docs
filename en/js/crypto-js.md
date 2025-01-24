> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>crypto-js</code> </h1>
</p>
<p align="center">
        <a href="https://github.com/brix/crypto-js/blob/4.2.0/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github address](https://github.com/brix/crypto-js/tree/4.2.0)

## Installation and Usage

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
npm install crypto-js@^4.2.0
npm install @types/crypto-js@^4.2.1
```

#### **yarn**

```bash
yarn add crypto-js@^4.2.0
yarn add @types/crypto-js@^4.2.1
```

<!-- tabs:end -->

Quick use:

```typescript
import React, { useState } from 'react';
import { View, Button, Text } from 'react-native';
import CryptoJS from 'crypto-js';

function CryptoJSDemo() {
  const [result, setResult] = useState(' ');
  return (
    <View>
      <Text>{result}</Text>

      <Button title='testMD5' onPress={testMD5}></Button>
      <Button title='testHmacMD5' onPress={testHmacMD5}></Button>

      <Button title='testAESEncrypt' onPress={testAESEncrypt}></Button>
      <Button title='testAESDecrypt' onPress={testAESDecrypt}></Button>

      <Button title='testEncHexParse' onPress={testEncHexParse}></Button>
      <Button title='testEncHexStringify' onPress={testEncHexStringify}></Button>
      <Button title='testFormatHexParse' onPress={testFormatHexParse}></Button>
      <Button title='testFormatHexStringify' onPress={testFormatHexStringify}></Button>
    </View>
  );

  function testMD5() {
    let md5 = CryptoJS.MD5('123456');
    setResult('testMD5 result: ' + md5.toString());
  }

  function testHmacMD5() {
    let hmacMD5 = CryptoJS.HmacMD5('123456', '123456');
    setResult('testHmacMD5 result: ' + hmacMD5.toString());
  }

  function testAESEncrypt() {
    let encrypted = CryptoJS.AES.encrypt(CryptoJS.enc.Hex.parse('48656c6c6f576f726c6421'), CryptoJS.enc.Hex.parse('000102030405060708090a0b0c0d0e0f'), { mode: CryptoJS.mode.ECB, padding: CryptoJS.pad.PKcs7 });
    setResult('testAESEncrypt result: ' + encrypted.toString());
  }

  function testAESDecrypt() {
    let encrypted = CryptoJS.AES.encrypt(CryptoJS.enc.Hex.parse('48656c6c6f576f726c6421'), CryptoJS.enc.Hex.parse('000102030405060708090a0b0c0d0e0f'), { mode: CryptoJS.mode.ECB, padding: CryptoJS.pad.PKcs7 });
    let decrypted = CryptoJS.AES.decrypt(encrypted, CryptoJS.enc.Hex.parse('000102030405060708090a0b0c0d0e0f'), { mode: CryptoJS.mode.ECB, padding: CryptoJS.pad.PKcs7 });
    setResult('testAESDecrypt result: ' + decrypted.toString());
  }

  function testEncHexParse() {
    let wordArray = CryptoJS.enc.Hex.parse('48656c6c6f576f726c6421');
    setResult('testEncHexParse result: ' + wordArray.toString());
  }

  function testEncHexStringify() {
    let wordArray = CryptoJS.enc.Hex.parse('48656c6c6f576f726c6421');
    let hexStr = CryptoJS.enc.Hex.stringify(wordArray);
    setResult('testEncHexStringify result: ' + hexStr);
  }

  function testFormatHexParse() {
    let hexStr = CryptoJS.format.Hex.parse('48656c6c6f576f726c6421').toString(CryptoJS.format.Hex);
    setResult('testFormatHexParse result: ' + hexStr);
  }

  function testFormatHexStringify() {
    let ciphertext = CryptoJS.enc.Hex.parse('48656c6c6f576f726c6421');
    let cipSalt = {
      'ciphertext': ciphertext
    }
    let hexStr = CryptoJS.format.Hex.stringify(CryptoJS.lib.CipherParams.create(cipSalt));
    setResult('testFormatHexStringify result: ' + hexStr);
  }
}

export default CryptoJSDemo;
```

## Constraints

#### Compatibility

This document is verified based on the following versions:

1. RNOH：0.72.11; SDK：OpenHarmony(api11) 4.1.0.53; IDE：DevEco Studio 4.1.3.412; ROM：2.0.0.52;
2. RNOH：0.72.13; SDK：HarmonyOS NEXT Developer Preview1; IDE：DevEco Studio 4.1.3.500; ROM：2.0.0.58;

## API List

**The following `C` is an object exported by crypto-js:**

```typescript
import C from "crypto-js";
```

#### Base

**Static Methods**

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name              | Description                                                  | Type     | Required | HarmonyOS Support |
| ----------------- | ------------------------------------------------------------ | -------- | -------- | ----------------- |
| C.lib.Base.extend | Creates an object and inherits it from the specified object. | function | no       | yes               |

**API**

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name   | Description                           | Type     | Required | HarmonyOS Support |
| ------ | ------------------------------------- | -------- | -------- | ----------------- |
| create | Creates an object instance.           | function | no       | yes               |
| mixIn  | Adds a property KV pair to an object. | function | no       | yes               |
| clone  | Creates a clone version of an object. | function | no       | yes               |

#### WordArray

**Properties**

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name     | Description                          | Type     | Required | HarmonyOS Support |
| -------- | ------------------------------------ | -------- | -------- | ----------------- |
| words    | A 32-bit byte array.                 | number[] | no       | yes               |
| sigBytes | Number of valid bytes in this array. | number   | no       | yes               |

**Static Methods**

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                   | Description                                    | Type     | Required | HarmonyOS Support            |
| ---------------------- | ---------------------------------------------- | -------- | -------- | ---------------------------- |
| C.lib.WordArray.create | Initializes a newly created byte array.        | function | no       | yes                          |
| C.lib.WordArray.random | Creates a byte array filled with random bytes. | function | no       | no (same as Android and iOS) |

**API**

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name     | Description                                   | Type     | Required | HarmonyOS Support |
| -------- | --------------------------------------------- | -------- | -------- | ----------------- |
| toString | Converts a byte array into a string.          | function | no       | yes               |
| concat   | Concatenates a byte array to this byte array. | function | no       | yes               |
| clamp    | Removes invalid bytes.                        | function | no       | yes               |
| clone    | Clones and creates an array.                  | function | no       | yes               |

#### CipherParams

**Properties**

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name       | Description                                                  | Type         | Required | HarmonyOS Support |
| ---------- | ------------------------------------------------------------ | ------------ | -------- | ----------------- |
| ciphertext | Original ciphertext.                                         | WordArray    | no       | yes               |
| key        | Key of the ciphertext.                                       | WordArray    | no       | yes               |
| iv         | Initialization Vector (IV) used in the encryption.           | WordArray    | no       | yes               |
| salt       | Salt used with the key derivation function.                  | WordArray    | no       | yes               |
| algorithm  | Password algorithm.                                          | CipherStatic | no       | yes               |
| mode       | Block mode used in the encryption.                           | Mode         | no       | yes               |
| padding    | Padding used in the encryption.                              | Padding      | no       | yes               |
| blockSize  | Block size of the password.                                  | number       | no       | yes               |
| formatter  | Default formatting policy for converting the **cipher params** object to a string. | Format       | no       | yes               |

**Static Methods**

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                      | Description                                             | Type     | Required | HarmonyOS Support |
| ------------------------- | ------------------------------------------------------- | -------- | -------- | ----------------- |
| C.lib.CipherParams.create | Initializes the newly created **cipher params** object. | function | no       | yes               |

**API**

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name     | Description                                        | Type     | Required | HarmonyOS Support |
| -------- | -------------------------------------------------- | -------- | -------- | ----------------- |
| toString | Converts the **cipher params** object to a string. | function | no       | yes               |

#### X64

**Static Methods**

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name              | Description                              | Type     | Required | HarmonyOS Support |
| ----------------- | ---------------------------------------- | -------- | -------- | ----------------- |
| C.x64.Word.create | Initializes a newly created 64-bit word. | function | no       | yes               |

#### X64WordArray

**Properties**

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name     | Description                                | Type     | Required | HarmonyOS Support |
| -------- | ------------------------------------------ | -------- | -------- | ----------------- |
| words    | Array of the **CryptoJS.x64.Word** object. | number[] | no       | yes               |
| sigBytes | Number of valid bytes in this array.       | number   | no       | yes               |

**Static Methods**

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                   | Description                             | Type     | Required | HarmonyOS Support |
| ---------------------- | --------------------------------------- | -------- | -------- | ----------------- |
| C.x64.WordArray.create | Initializes a newly created word array. | function | no       | yes               |

**API**

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name  | Description                                          | Type     | Required | HarmonyOS Support |
| ----- | ---------------------------------------------------- | -------- | -------- | ----------------- |
| toX32 | Converts a 64-bit word array to a 32-bit word array. | function | no       | yes               |
| clone | Creates a copy of this byte array.                   | function | no       | yes               |

#### mode

**Properties**

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name       | Description            | Type | Required | HarmonyOS Support |
| ---------- | ---------------------- | ---- | -------- | ----------------- |
| C.mode.CBC | Cipher block chaining. | /    | no       | yes               |
| C.mode.CFB | Cipher feedback block. | /    | no       | yes               |
| C.mode.CTR | Counter mode.          | /    | no       | yes               |
| C.mode.OFB | Output feedback block. | /    | no       | yes               |
| C.mode.ECB | Electronic code book.  | /    | no       | yes               |

#### pad.Pkcs7

**Static Methods**

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name              | Description                                                  | Type     | Required | HarmonyOS Support |
| ----------------- | ------------------------------------------------------------ | -------- | -------- | ----------------- |
| C.pad.Pkcs7.pad   | Pads the data using the algorithm defined in PKCS #5 or PKCS #7. | function | no       | yes               |
| C.pad.Pkcs7.unpad | Unpads the data using the algorithm defined in PKCS #5 or PKCS #7. | function | no       | yes               |

#### pad.AnsiX923

**Static Methods**

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                 | Description                                              | Type     | Required | HarmonyOS Support |
| -------------------- | -------------------------------------------------------- | -------- | -------- | ----------------- |
| C.pad.AnsiX923.pad   | Pads the data using the algorithm defined in AnsiX923.   | function | no       | yes               |
| C.pad.AnsiX923.unpad | Unpads the data using the algorithm defined in AnsiX923. | function | no       | yes               |

#### pad.Iso10126

**Static Methods**

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                 | Description                                              | Type     | Required | HarmonyOS Support            |
| -------------------- | -------------------------------------------------------- | -------- | -------- | ---------------------------- |
| C.pad.Iso10126.pad   | Pads the data using the algorithm defined in ISO10126.   | function | no       | no (same as Android and iOS) |
| C.pad.Iso10126.unpad | Unpads the data using the algorithm defined in ISO10126. | function | no       | yes                          |

#### pad.ZeroPadding

**Static Methods**

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                    | Description                                                 | Type     | Required | HarmonyOS Support |
| ----------------------- | ----------------------------------------------------------- | -------- | -------- | ----------------- |
| C.pad.ZeroPadding.pad   | Pads the data using the algorithm defined in ZeroPadding.   | function | no       | yes               |
| C.pad.ZeroPadding.unpad | Unpads the data using the algorithm defined in ZeroPadding. | function | no       | yes               |

#### pad.NoPadding

**Properties**

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name            | Description               | Type | Required | HarmonyOS Support |
| --------------- | ------------------------- | ---- | -------- | ----------------- |
| C.pad.NoPadding | No padding rules is used. | /    | no       | yes               |

#### algo

**Static Methods**

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                    | Description                                                  | Type     | Required | HarmonyOS Support |
| ----------------------- | ------------------------------------------------------------ | -------- | -------- | ----------------- |
| C.algo.MD5.create       | Initializes the utility class created by MD5 encryption.     | function | no       | yes               |
| C.MD5                   | Indicates the MD5 encryption.                                | function | no       | yes               |
| C.algo.SHA1.create      | Initializes the utility class created by SHA1 encryption.    | function | no       | yes               |
| C.SHA1                  | Indicates the SHA1 encryption.                               | function | no       | yes               |
| C.algo.SHA256.create    | Initializes the utility class created by SHA256 encryption.  | function | no       | yes               |
| C.SHA256                | Indicates the SHA256 encryption.                             | function | no       | yes               |
| C.algo.SHA224.create    | Initializes the utility class created by SHA224 encryption.  | function | no       | yes               |
| C.SHA224                | Indicates the SHA224 encryption.                             | function | no       | yes               |
| C.algo.SHA512.create    | Initializes the utility class created by SHA512 encryption.  | function | no       | yes               |
| C.SHA512                | Indicates the SHA512 encryption.                             | function | no       | yes               |
| C.algo.SHA3.create      | Initializes the utility class created by SHA3 encryption.    | function | no       | yes               |
| C.SHA3                  | Indicates the SHA3 encryption.                               | function | no       | yes               |
| C.algo.SHA384.create    | Initializes the utility class created by SHA384 encryption.  | function | no       | yes               |
| C.SHA384                | Indicates the SHA384 encryption.                             | function | no       | yes               |
| C.algo.RIPEMD160.create | Initializes the utility class created by RIPEMD160 encryption. | function | no       | yes               |
| C.RIPEMD160             | Indicates the RIPEMD160 encryption.                          | function | no       | yes               |

#### Hasher

**Properties**

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name      | Description                                                  | Type   | Required | HarmonyOS Support |
| --------- | ------------------------------------------------------------ | ------ | -------- | ----------------- |
| blockSize | Size of the 32-bit block for hashing. Default value: **16(32\*16=512 bits)**. | number | no       | yes               |

**API**

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name     | Description                         | Type     | Required | HarmonyOS Support |
| -------- | ----------------------------------- | -------- | -------- | ----------------- |
| reset    | Resets Hasher to the initial state. | function | no       | yes               |
| update   | Updates the Hasher information.     | function | no       | yes               |
| finalize | Ends the Hasher operation.          | function | no       | yes               |

#### HMAC

**Static Methods**

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name               | Description                             | Type     | Required | HarmonyOS Support |
| :----------------- | --------------------------------------- | -------- | -------- | ----------------- |
| C.HmacMD5          | Indicates the HMAC-MD5 encryption.      | function | no       | yes               |
| C.HmacSHA1         | Indicates the HMAC-SHA1 encryption.     | function | no       | yes               |
| C.HmacSHA256       | Indicates the HMAC-SHA256 encryption.   | function | no       | yes               |
| C.HmacSHA224       | Indicates the HMAC-SHA224 encryption.   | function | no       | yes               |
| C.HmacSHA512       | Indicates the HMAC-SHA512 encryption.   | function | no       | yes               |
| C.HmacSHA384       | Indicates the HMAC-SHA384 encryption.   | function | no       | yes               |
| C.HmacSHA3         | Indicates the HMAC-SHA3 encryption.     | function | no       | yes               |
| C.HmacRIPEMD160    | Indicates the HMACRIPEMD160 encryption. | function | no       | yes               |
| C.algo.HMAC.create | Initializes newly created HMAC.         | function | no       | yes               |

**API**

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name     | Description                                                  | Type     | Required | HarmonyOS Support |
| :------- | ------------------------------------------------------------ | -------- | -------- | ----------------- |
| reset    | Resets this HMAC to its initial state.                       | function | no       | yes               |
| update   | Updates this HMAC using a message.                           | function | no       | yes               |
| finalize | Finalizes the HMAC calculation. Note that this is a destructive and read-once operation. | function | no       | yes               |

#### AES

**Static Methods**

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                       | Description                                | Type     | Required | HarmonyOS Support | Notes                                                        |
| :------------------------- | ------------------------------------------ | -------- | -------- | ----------------- | ------------------------------------------------------------ |
| C.AES.encrypt              | Encrypts using the AES algorithm.          | function | no       | partially         | The password must be in the **WordArray** format and cannot be set to the string type (same as Android and iOS). |
| C.AES.decrypt              | Decrypts using the AES algorithm.          | function | no       | partially         | The password must be in the **WordArray** format and cannot be set to the string type (same as Android and iOS). |
| C.algo.AES.createEncryptor | Creates a password in AES encryption mode. | function | no       | yes               |                                                              |

#### DES

**Static Methods**

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                       | Description                                | Type     | Required | HarmonyOS Support | Notes                                                        |
| :------------------------- | ------------------------------------------ | -------- | -------- | ----------------- | ------------------------------------------------------------ |
| C.DES.encrypt              | Encrypts using the DES algorithm.          | function | no       | partially         | The password must be in the **WordArray** format and cannot be set to the string type (same as Android and iOS). |
| C.DES.decrypt              | Decrypts using the DES algorithm.          | function | no       | partially         | The password must be in the **WordArray** format and cannot be set to the string type (same as Android and iOS). |
| C.algo.DES.createEncryptor | Creates a password in DES encryption mode. | function | no       | yes               |                                                              |

#### TripleDES

**Static Methods**

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                             | Description                                      | Type     | Required | HarmonyOS Support | Notes                                                        |
| :------------------------------- | ------------------------------------------------ | -------- | -------- | ----------------- | ------------------------------------------------------------ |
| C.TripleDES.encrypt              | Encrypts using the TripleDES algorithm.          | function | no       | partially         | The password must be in the **WordArray** format and cannot be set to the string type (same as Android and iOS). |
| C.TripleDES.decrypt              | Decrypts using the TripleDES algorithm.          | function | no       | partially         | The password must be in the **WordArray** format and cannot be set to the string type (same as Android and iOS). |
| C.algo.TripleDES.createEncryptor | Creates a password in TripleDES encryption mode. | function | no       | yes               |                                                              |

#### RC4

**Static Methods**

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                       | Description                                | Type     | Required | HarmonyOS Support | Notes                                                        |
| :------------------------- | ------------------------------------------ | -------- | -------- | ----------------- | ------------------------------------------------------------ |
| C.RC4.encrypt              | Encrypts using the RC4 algorithm.          | function | no       | partially         | The password must be in the **WordArray** format and cannot be set to the string type (same as Android and iOS). |
| C.RC4.decrypt              | Decrypts using the RC4 algorithm.          | function | no       | partially         | The password must be in the **WordArray** format and cannot be set to the string type (same as Android and iOS). |
| C.algo.RC4.createEncryptor | Creates a password in RC4 encryption mode. | function | no       | yes               |                                                              |

#### RC4Drop

**Static Methods**

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                          | Description                                    | Type     | Required | HarmonyOS Support | Notes                                                        |
| :---------------------------- | ---------------------------------------------- | -------- | -------- | ----------------- | ------------------------------------------------------------ |
| C.RC4Drop.encrypt             | Encrypts using the RC4Drop algorithm.          | function | no       | partially         | The password must be in the **WordArray** format and cannot be set to the string type (same as Android and iOS). |
| C.RC4Drop.decrypt             | Decrypts using the RC4Drop algorithm.          | function | no       | partially         | The password must be in the **WordArray** format and cannot be set to the string type (same as Android and iOS). |
| C.algo.RC4Drop.createEncrypto | Creates a password in RC4Drop encryption mode. | function | no       | yes               |                                                              |

#### Rabbit

**Static Methods**

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                          | Description                                   | Type     | Required | HarmonyOS Support | Notes                                                        |
| :---------------------------- | --------------------------------------------- | -------- | -------- | ----------------- | ------------------------------------------------------------ |
| C.Rabbit.encrypt              | Encrypts using the Rabbit algorithm.          | function | no       | partially         | The password must be in the **WordArray** format and cannot be set to the string type (same as Android and iOS). |
| C.Rabbit.decrypt              | Decrypts using the Rabbit algorithm.          | function | no       | partially         | The password must be in the **WordArray** format and cannot be set to the string type (same as Android and iOS). |
| C.algo.Rabbit.createEncryptor | Creates a password in Rabbit encryption mode. | function | no       | yes               |                                                              |

#### RabbitLegacy

**Static Methods**

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                                | Description                                         | Type     | Required | HarmonyOS Support | Notes                                                        |
| :---------------------------------- | --------------------------------------------------- | -------- | -------- | ----------------- | ------------------------------------------------------------ |
| C.RabbitLegacy.encrypt              | Encrypts using the RabbitLegacy algorithm.          | function | no       | partially         | The password must be in the **WordArray** format and cannot be set to the string type (same as Android and iOS). |
| C.RabbitLegacy.decrypt              | Decrypts using the RabbitLegacy algorithm.          | function | no       | partially         | The password must be in the **WordArray** format and cannot be set to the string type (same as Android and iOS). |
| C.algo.RabbitLegacy.createEncryptor | Creates a password in RabbitLegacy encryption mode. | function | no       | yes               |                                                              |

#### Cipher

**Properties**

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name    | Description                                               | Type   | Required | HarmonyOS Support |
| :------ | --------------------------------------------------------- | ------ | -------- | ----------------- |
| keySize | Key size of the password. Default value: **4 (128 bits)** | number | no       | yes               |
| ivSize  | IV size of the password. Default value: **4 (128 bits)**  | number | no       | yes               |

**API**

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name     | Description                                                  | Type     | Required | HarmonyOS Support |
| :------- | ------------------------------------------------------------ | -------- | -------- | ----------------- |
| reset    | Resets the password to the initial state.                    | function | no       | yes               |
| process  | Adds data to be encrypted or decrypted.                      | function | no       | yes               |
| finalize | Finalizes encryption or decryption. Note that this is a destructive and read-once operation. | function | no       | yes               |

#### Blowfish

**Static Methods**

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name               | Description                            | Type     | Required | HarmonyOS Support |
| :----------------- | -------------------------------------- | -------- | -------- | ----------------- |
| C.Blowfish.encrypt | Encrypts using the Blowfish algorithm. | function | no       | yes               |
| C.Blowfish.decrypt | Decrypts using the Blowfish algorithm. | function | no       | yes               |

#### SerializableCipher

**Static Methods**

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                             | Description                         | Type     | Required | HarmonyOS Support |
| :------------------------------- | ----------------------------------- | -------- | -------- | ----------------- |
| C.lib.SerializableCipher.encrypt | Encrypts information.               | function | no       | yes               |
| C.lib.SerializableCipher.decrypt | Decrypts the encrypted information. | function | no       | yes               |

#### PasswordBasedCipher

**Static Methods**

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                              | Description                         | Type     | Required | HarmonyOS Support | Notes                                                        |
| :-------------------------------- | ----------------------------------- | -------- | -------- | ----------------- | ------------------------------------------------------------ |
| C.lib.PasswordBasedCipher.encrypt | Encrypts information.               | function | no       | partially         | A valid **salt** parameter must be passed in. Otherwise, the HarmonyOS platform does not support (same as Android and iOS). |
| C.lib.PasswordBasedCipher.decrypt | Decrypts the encrypted information. | function | no       | partially         | A valid **salt** parameter must be passed in. Otherwise, the HarmonyOS platform does not support (same as Android and iOS). |

#### kdf.OpenSSL

**Static Methods**

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                  | Description                               | Type     | Required | HarmonyOS Support | Notes                                                        |
| :-------------------- | ----------------------------------------- | -------- | -------- | ----------------- | ------------------------------------------------------------ |
| C.kdf.OpenSSL.execute | Derives the key and IV from the password. | function | no       | partially         | A valid **salt** parameter must be passed in. Otherwise, the HarmonyOS platform does not support (same as Android and iOS). |

#### kdf.PBKDF2

**Static Methods**

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                 | Description                                                | Type     | Required | HarmonyOS Support |
| :------------------- | ---------------------------------------------------------- | -------- | -------- | ----------------- |
| C.algo.PBKDF2.create | Initializes the key derivation function created by PBKDF2. | function | no       | yes               |
| C.PBKDF2             | Derives key by PBKDF2.                                     | function | no       | yes               |

**API**

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name    | Description                                                  | Type     | Required | HarmonyOS Support |
| :------ | ------------------------------------------------------------ | -------- | -------- | ----------------- |
| compute | Computes the key derivation function based on the PBKDF2 password. | function | no       | yes               |

#### EvpKDF

**Static Methods**

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                 | Description                                                | Type     | Required | HarmonyOS Support |
| :------------------- | ---------------------------------------------------------- | -------- | -------- | ----------------- |
| C.algo.EvpKDF.create | Initializes the key derivation function created by EvpKDF. | function | no       | yes               |
| C.EvpKDF             | Derives key by EvpKDF.                                     | function | no       | yes               |

**API**


> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name    | Description                                                  | Type     | Required | HarmonyOS Support |
| :------ | ------------------------------------------------------------ | -------- | -------- | ----------------- |
| compute | Computes the key derivation function based on the EvpKDF password. | function | no       | yes               |

#### format

**Static Methods**

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                       | Description                                                  | Type     | Required | HarmonyOS Support |
| :------------------------- | ------------------------------------------------------------ | -------- | -------- | ----------------- |
| C.format.OpenSSL.stringify | Converts the **CipherParams** object to an OpenSSL-compatible string. | function | no       | yes               |
| C.format.OpenSSL.parse     | Converts an OpenSSL-compatible string to the **CipherParams** object. | function | no       | yes               |
| C.format.Hex.stringify     | Converts the **CipherParams** object into a hexadecimal string. | function | no       | yes               |
| C.format.Hex.parse         | Converts a hexadecimal string into the **CipherParams** object. | function | no       | yes               |

#### enc/Encoder

**Static Methods**

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                      | Description                                                | Type     | Required | HarmonyOS Support |
| :------------------------ | ---------------------------------------------------------- | -------- | -------- | ----------------- |
| C.enc.Hex.stringify       | Converts a byte array into a hexadecimal string.           | function | no       | yes               |
| C.enc.Hex.parse           | Converts a hexadecimal string into a byte array.           | function | no       | yes               |
| C.enc.Latin1.stringify    | Converts a byte array into an ISO-8859-1-encoded C string. | function | no       | yes               |
| C.enc.Latin1.parse        | Converts an ISO-8859-1-encoded C string into a byte array. | function | no       | yes               |
| C.enc.Utf8.stringify      | Converts a byte array into a UTF-8-encoded string.         | function | no       | yes               |
| C.enc.Utf8.parse          | Converts a UTF-8-encoded string into a byte array.         | function | no       | yes               |
| C.enc.Utf16.stringify     | Converts a byte array into a UTF-16-encoded string.        | function | no       | yes               |
| C.enc.Utf16.parse         | Converts a UTF-16-encoded string into a byte array.        | function | no       | yes               |
| C.enc.Utf16BE.stringify   | Converts a byte array into a UTF-16BE-encoded string.      | function | no       | yes               |
| C.enc.Utf16BE.parse       | Converts a UTF-16BE-encoded string into a byte array.      | function | no       | yes               |
| C.enc.Utf16LE.stringify   | Converts a byte array into a UTF-16LE-encoded string.      | function | no       | yes               |
| C.enc.Utf16LE.parse       | Converts a UTF-16LE-encoded string into a byte array.      | function | no       | yes               |
| C.enc.Base64.stringify    | Converts a byte array into a Base64-encoded string.        | function | no       | yes               |
| C.enc.Base64.parse        | Converts a Base64-encoded string into a byte array.        | function | no       | yes               |
| C.enc.Base64url.stringify | Converts a byte array into a Base64URL-encoded string.     | function | no       | yes               |
| C.enc.Base64url.parse     | Converts a Base64URL-encoded string into a byte array.     | function | no       | yes               |

## Known Issues

## Others

## License

This project is licensed under [MIT License](https://github.com/brix/crypto-js/blob/4.2.0/LICENSE).
