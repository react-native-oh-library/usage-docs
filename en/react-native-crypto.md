> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-crypto</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/tradle/react-native-crypto">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/tradle/react-native-crypto/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/tradle/react-native-crypto)

## Installation and Usage

[!TIP]This repository depends on [@react-native-oh-tpl/react-native-randombytes](./react-native-randombytes.md)

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-crypto@2.2.0
```

#### **yarn**

```bash
yarn add react-native-crypto@2.2.0
```

<!-- tabs:end -->

#### Install a mock library that adapts to Node.js core modules.

1. Install

```bash
# install latest rn-nodeify
npm i --save-dev rn-nodeify
# install node core shims and recursively hack package.json files
# in ./node_modules to add/update the "browser"/"react-native" field with relevant mappings
./node_modules/.bin/rn-nodeify --hack --install
```

2. `rn-nodeify` will create a `shim.js` in the project root directory

```js
// make sure you use `import` and not require!
import "./shim.js";
import crypto from "react-native-crypto";
// ...the rest of your code
```

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import './shim.js'
import React, { useState } from 'react';
import crypto from 'react-native-crypto';

const [randomBytesResult, setRandomBytesResult] = useState('');
const [inputValue, setInputValue] = useState('');
const [intValue, setIntValue] = useState(0);

const TestCrypto = () => {
  function handleRandom(data: number) {
      if (!data) throw new Error('The input is can not be null!')
      crypto.randomBytes(data, (err: Error | null, bytes: Buffer) => {
          if (err) throw err;
          setRandomBytesResult(bytes.toJSON().data.join('-'));
      });
  }

  function handleInputChange(text: any) {
      const intValue = parseInt(text);
      if (!isNaN(text)) {
          setInputValue(text);
          setIntValue(intValue);
      } else {
          setInputValue('');
          setIntValue(0);
      }
  };

  function handleButtonPress() {
      handleRandom(intValue);
  };

  return (
    <View style={styles.buttonContainer}>
        <Button
            title="submit"
            onPress={handleButtonPress}
        />
        <TextInput
            style={{ height: 40, borderColor: 'gray', borderWidth: 1, marginBottom: 10, padding: 5, marginTop: 5 }}
            placeholder="input number"
            onChangeText={handleInputChange}
            value={inputValue}
            keyboardType="numeric"
        />
    </View>
    <Text style={styles.result}>{randomBytesResult}</Text>
  );
}

const styles = StyleSheet.create({
    buttonContainer: {
        marginVertical: 5,
    },
    result: {
        fontSize: 16,
        marginTop: 5,
        marginLeft: 6,
        marginBottom: 12
    }
})

export default TestCrypto;
```

## Link

The HarmonyOS implementation of this library depends on the native code from @react-native-oh-tpl/react-native-randombytes. If this library is included into your HarmonyOS application, there is no need to include it again; you can skip the steps in this section and use it directly.

If it is not included, follow the guide provided in @react-native-oh-tpl/react-native-randombytes to add it to your project.

## Constraints

### Compatibility

This document is verified based on the following versions:

1. RNOH: 0.72.27; SDK：HarmonyOS NEXT Developer Beta1 5.0.0.25; IDE：DevEco Studio 5.0.3.400SP7; ROM：3.0.0.25;

## API

> [!Tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!Tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                     | Description                                                                                                                                                                                                                                                                                                         | Type     | Required | Platform    | HarmonyOS Support |
| ------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | ----------- | ----------------- |
| createHash               | Create a hash object                                                                                                                                                                                                                                                                                                | function | yes      | iOS/Android | yes               |
| createHmac               | Create an HMAC (Hash-based Message Authentication Code) object                                                                                                                                                                                                                                                      | function | yes      | iOS/Android | yes               |
| pbkdf2                   | It is a key derivation function (PBKDF2) used for password encryption                                                                                                                                                                                                                                               | function | yes      | iOS/Android | yes               |
| pbkdf2Sync               | It is a key derivation function (PBKDF2) used for password encryption,But it is executed synchronously                                                                                                                                                                                                              | function | yes      | iOS/Android | yes               |
| randomBytes              | Generate a random byte sequence of a specified size                                                                                                                                                                                                                                                                 | function | yes      | iOS/Android | yes               |
| getHashes                | Provide a list of supported specific hash algorithms                                                                                                                                                                                                                                                                | function | no       | iOS/Android | yes               |
| createCipher             | Create an encryption object for an encryption algorithm                                                                                                                                                                                                                                                             | function | yes      | iOS/Android | yes               |
| Cipher                   | Create an encryption object for an encryption algorithm                                                                                                                                                                                                                                                             | function | yes      | iOS/Android | yes               |
| createDecipher           | Create a decryption object for a decryption algorithm                                                                                                                                                                                                                                                               | function | yes      | iOS/Android | yes               |
| Decipher                 | Create a decryption object for a decryption algorithm                                                                                                                                                                                                                                                               | function | yes      | iOS/Android | yes               |
| createCipheriv           | Create an encryption object for an encryption algorithm and specify an initialization vector (IV) to enhance encryption security                                                                                                                                                                                    | function | yes      | iOS/Android | yes               |
| Cipheriv                 | Create an encryption object for an encryption algorithm and specify an initialization vector (IV) to enhance encryption security                                                                                                                                                                                    | function | yes      | iOS/Android | yes               |
| createDecipheriv         | Create a decryption object for a decryption algorithm and specify the same initialization vector (IV) used during encryption to correctly decrypt the data                                                                                                                                                          | function | yes      | iOS/Android | yes               |
| Decipheriv               | Create a decryption object for a decryption algorithm and specify the same initialization vector (IV) used during encryption to correctly decrypt the data                                                                                                                                                          | function | yes      | iOS/Android | yes               |
| getCiphers               | Get a list of currently supported encryption algorithms                                                                                                                                                                                                                                                             | function | no       | iOS/Android | yes               |
| listCiphers              | Get a list of currently supported encryption algorithms                                                                                                                                                                                                                                                             | function | no       | iOS/Android | yes               |
| DiffieHellmanGroup       | Module that implements the Diffie-Hellman key exchange protocol                                                                                                                                                                                                                                                     | function | yes      | iOS/Android | yes               |
| createDiffieHellmanGroup | Create a "group" in the Diffie-Hellman key negotiation algorithm, i.e., Diffie-Hellman parameters                                                                                                                                                                                                                   | function | yes      | iOS/Android | yes               |
| getDiffieHellman         | Get an implementation of the Diffie-Hellman key exchange algorithm                                                                                                                                                                                                                                                  | function | yes      | iOS/Android | yes               |
| createDiffieHellman      | Create a Diffie-Hellman instance                                                                                                                                                                                                                                                                                    | function | yes      | iOS/Android | yes               |
| DiffieHellman            | It is a class or set of methods for implementing the Diffie-Hellman key exchange protocol, mainly used for key generation and shared key calculation in secure communications.                                                                                                                                      | function | yes      | iOS/Android | yes               |
| createSign               | Create an object instance for generating signatures                                                                                                                                                                                                                                                                 | function | yes      | iOS/Android | yes               |
| Sign                     | Create an object instance for generating signatures                                                                                                                                                                                                                                                                 | function | yes      | iOS/Android | yes               |
| createVerify             | Create an object instance for verifying signatures                                                                                                                                                                                                                                                                  | function | yes      | iOS/Android | yes               |
| Verify                   | Create an object instance for verifying signatures                                                                                                                                                                                                                                                                  | function | yes      | iOS/Android | yes               |
| createECDH               | Method to create an elliptic curve Diffie-Hellman key exchange object                                                                                                                                                                                                                                               | function | yes      | iOS/Android | yes               |
| publicEncrypt            | Method to create an elliptic curve Diffie-Hellman key exchange object                                                                                                                                                                                                                                               | function | yes      | iOS/Android | yes               |
| privateEncrypt           | Encrypt the content of a buffer using a private key and return a new Buffer containing the encrypted content (Note: Typically, private keys are used for decryption and public keys for encryption in asymmetric encryption, but this could refer to a specific use case or library behavior.)                      | function | yes      | iOS/Android | yes               |
| publicDecrypt            | Decrypt the encrypted content of a buffer using a public key and return a new Buffer containing the decrypted content (Note: This is incorrect in the context of standard asymmetric encryption; public keys are used for encryption, not decryption. This may refer to a specific scenario or a misunderstanding.) | function | yes      | iOS/Android | yes               |
| privateDecrypt           | Decrypt the encrypted content of a buffer using a private key and return a new Buffer containing the decrypted content                                                                                                                                                                                              | function | yes      | iOS/Android | yes               |
| randomFill               | Fill a given Buffer with cryptographically secure pseudorandom data asynchronously                                                                                                                                                                                                                                  | function | yes      | iOS/Android | yes               |
| randomFillSync           | Fill a given Buffer with cryptographically secure pseudorandom data synchronously                                                                                                                                                                                                                                   | function | yes      | iOS/Android | yes               |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/tradle/react-native-crypto/blob/master/LICENSE).
