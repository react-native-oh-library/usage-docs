> 模板版本：v0.2.2

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

> [!TIP] [Github 地址](https://github.com/tradle/react-native-crypto)


## 安装与使用

[!TIP]本库依赖[@react-native-oh-tpl/react-native-randombytes](./react-native-randombytes.md)

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

#### 安装适配 Node.js 核心模块的模拟库

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
import './shim.js'
import crypto from 'react-native-crypto'
// ...the rest of your code
```

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

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
            title="提交"
            onPress={handleButtonPress}
        />
        <TextInput
            style={{ height: 40, borderColor: 'gray', borderWidth: 1, marginBottom: 10, padding: 5, marginTop: 5 }}
            placeholder="输入数字"
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

本库 HarmonyOS 侧实现依赖@react-native-oh-tpl/react-native-randombytes 的原生端代码，如已在 HarmonyOS 工程中引入过该库，则无需再次引入，可跳过本章节步骤，直接使用。

如未引入请参照[@react-native-oh-tpl/react-native-randombytes 文档](/zh-cn/react-native-randombytes.md)进行引入

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH: 0.72.27; SDK：HarmonyOS NEXT Developer Beta1 5.0.0.25; IDE：DevEco Studio 5.0.3.400SP7; ROM：3.0.0.25;

## API

> [!Tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!Tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。
> 

| Name                            | Description              | Type      | Required | Platform | HarmonyOS Support |
| ----                            | -----------              | ----      | -------- | -------- | ----------------- |
| createHash                      | 创建哈希对象                                                          | function  | yes      | iOS/Android      | yes               |
| createHmac                      | 创建 HMAC（Hash-based Message Authentication Code）对象                | function  | yes      | iOS/Android      | yes               |
| pbkdf2                          |是一种用于密码加密的密钥派生函数（PBKDF2)                                      | function  | yes      | iOS/Android      | yes               |
| pbkdf2Sync                      |是一种用于密码加密的密钥派生函数（PBKDF2），但它是同步执行的                      | function  | yes      | iOS/Android      | yes               |
| randomBytes                     | 生成指定大小的随机字节序列                                               | function  | yes      | iOS/Android      | yes               |
| getHashes                       | 提供支持的特定哈希算法列表                                               | function  | no       | iOS/Android      | yes               |
| createCipher                    | 创建加密算法的加密对象                                                  | function  | yes      | iOS/Android      | yes               |
| Cipher                    | 创建加密算法的加密对象                                                  | function  | yes      | iOS/Android      | yes               |
| createDecipher                  | 创建解密算法的解密对象                                                  | function  | yes      | iOS/Android      | yes               |
| Decipher                  | 创建解密算法的解密对象                                                  | function  | yes      | iOS/Android      | yes               |
| createCipheriv                  | 创建加密算法的加密对象，并指定初始化向量（IV）来增强加密的安全性            | function  | yes      | iOS/Android      | yes               |
| Cipheriv                  | 创建加密算法的加密对象，并指定初始化向量（IV）来增强加密的安全性            | function  | yes      | iOS/Android      | yes               |
| createDecipheriv                | 创建解密算法的解密对象，并指定与加密时使用相同的初始化向量（IV）来正确解密数据 | function  | yes      | iOS/Android      | yes               |
| Decipheriv                | 创建解密算法的解密对象，并指定与加密时使用相同的初始化向量（IV）来正确解密数据 | function  | yes      | iOS/Android      | yes               |
| getCiphers                      | 获取当前支持的加密算法列表                                               | function  | no       | iOS/Android      | yes               |
| listCiphers                      | 获取当前支持的加密算法列表                                               | function  | no       | iOS/Android      | yes               |
| DiffieHellmanGroup              | 实现 Diffie-Hellman 密钥交换协议的模块                                     | function  | yes      | iOS/Android      | yes               |
| createDiffieHellmanGroup        | 创建一个 Diffie-Hellman 密钥协商算法中的“群”，即 Diffie-Hellman 的参数         | function  | yes      | iOS/Android      | yes               |
| getDiffieHellman                | 获取 Diffie-Hellman 密钥交换算法的实现                                     | function  | yes      | iOS/Android      | yes               |
| createDiffieHellman             | 创建 Diffie-Hellman 实例                                                | function  | yes      | iOS/Android      | yes               |
| DiffieHellman                   | 是一个用于实现 Diffie-Hellman 密钥交换协议的类或方法集合，主要用于安全通信中的密钥生成和共享密钥计算。 | function  | yes      | iOS/Android      | yes               |
| createSign                      | 创建一个用于生成签名的对象实例                                            | function  | yes      | iOS/Android      | yes               |
| Sign                            | 创建一个用于生成签名的对象实例                                                          | function  | yes      | iOS/Android      | yes               |
| createVerify                    | 创建一个用于验证签名的对象实例                                            | function  | yes      | iOS/Android      | yes               |
| Verify                          | 创建一个用于验证签名的对象实例                                                        | function  | yes      | iOS/Android      | yes               |
| createECDH                      | 创建椭圆曲线 Diffie-Hellman 密钥交换对象的方法                              | function  | yes      | iOS/Android      | yes               |
| publicEncrypt                   | 使用公钥对 buffer 的内容进行加密，并返回一个包含加密内容的新 Buffer                                                                    | function  | yes      | iOS/Android      | yes               |
| privateEncrypt                  | 使用私钥对 buffer 的内容进行加密，并返回一个包含加密内容的新 Buffer                                                                    | function  | yes      | iOS/Android      | yes               |
| publicDecrypt                   | 使用公钥对加密的 buffer 进行解密，并返回一个包含解密内容的新 Buffer                                                                    | function  | yes      | iOS/Android      | yes                |
| privateDecrypt                  |  使用私钥对加密的 buffer 进行解密，并返回一个包含解密内容的新 Buffer                                                                    | function  | yes      | iOS/Android      | yes                |
| randomFill                      | 使用加密安全的伪随机数据填充一个给定的 Buffer，异步操作                                                                    | function  | yes      | iOS/Android      | yes               |
| randomFillSync                  | 使用加密安全的伪随机数据同步填充一个给定的 Buffer                                                                    | function  | yes      | iOS/Android      | yes               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/tradle/react-native-crypto/blob/master/LICENSE) ，请自由地享受和参与开源。