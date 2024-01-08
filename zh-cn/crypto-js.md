> 模板版本：v0.1.2

<p align="center">
  <h1 align="center"> <code>crypto-js</code> </h1>
</p>
<p align="center">
        <a href="https://github.com/brix/crypto-js/blob/4.2.0/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>


> [!tip] [Github 地址](https://github.com/brix/crypto-js/tree/4.2.0)

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **yarn**

```bash
yarn add crypto-js
yarn add @types/crypto-js
```

#### **npm**

```bash
npm install crypto-js
npm install @types/crypto-js
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

```typescript
import React, { useState } from 'react';
import { View, Button, Text } from 'react-native';
import CryptoJS from 'crypto-js';

function CryptoJSDemo() {
    const[result, setResult] = useState(' ');
    return(
        <View>
        	<Text>{result}</Text>
        	// 非对称加密
        	<Button title='testMD5' onPress={testMD5}></Button>
			<Button title='testHmacMD5' onPress={testHmacMD5}></Button>

			// 对称加密
			<Button title='testAESEncrypt' onPress={testAESEncrypt}></Button>
			<Button title='testAESDecrypt' onPress={testAESDecrypt}></Button>

			// 类型转换
			<Button title='testEncHexParse' onPress={testEncHexParse}></Button>
			<Button title='testEncHexStringify' onPress={testEncHexStringify}></Button>
			<Button title='testFormatHexParse' onPress={testFormatHexParse}></Button>
			<Button title='testFormatHexStringify' onPress={testFormatHexStringify}></Button>
        </View>
    );
    
    function testMD5(){
        let md5 = CryptoJS.MD5('123456');
        setResult(md5.toString());
    }
    
    function testHmacMD5(){
        let hmacMD5 = CryptoJS.HmacMD5('123456', '123456');
         setResult(hmacMD5.toString());
    }

	function testAESEncrypt(){
        let encrypted = CryptoJS.AES.encrypt(CryptoJS.enc.Hex.parse('48656c6c6f576f726c6421'), CryptoJS.enc.Hex.parse('000102030405060708090a0b0c0d0e0f'), { mode: CryptoJS.mode.ECB, padding: CryptoJS.pad.NoPadding });
        setResult(encrypted.toString());
    }

	function testAESDecrypt(){
        let encrypted = CryptoJS.AES.encrypt(CryptoJS.enc.Hex.parse('48656c6c6f576f726c6421'), CryptoJS.enc.Hex.parse('000102030405060708090a0b0c0d0e0f'), { mode: CryptoJS.mode.ECB, padding: CryptoJS.pad.NoPadding });
        let decrypted = CryptoJS.AES.decrypt(encrypted, CryptoJS.enc.Hex.parse('000102030405060708090a0b0c0d0e0f'), { mode: CryptoJS.mode.ECB, padding: CryptoJS.pad.NoPadding });
        setResult(decrypted.toString());
    }

	function testEncHexParse() {
        let wordArray = CryptoJS.enc.Hex.parse('48656c6c6f576f726c6421');
        setResult(wordArray.toString());
    }

	function testEncHexStringify() {
        let wordArray = CryptoJS.enc.Hex.parse('48656c6c6f576f726c6421');
        let hexStr = CryptoJS.enc.Hex.stringify(wordArray);
        setResult(hexStr);
    }

	function testFormatHexParse() {
        let hexStr = CryptoJS.format.Hex.parse('48656c6c6f576f726c6421').toString(CryptoJS.format.Hex);
        setResult(hexStr);
    }

	function testFormatHexStringify() {
        let ciphertext = CryptoJS.enc.Hex.parse('48656c6c6f576f726c6421');
        let cipSalt = {
            'ciphertext': ciphertext
        }
        let hexStr = CryptoJS.format.Hex.stringify(CryptoJS.lib.CipherParams.create(cipSalt));
        setResult(hexStr);
    }
}

export default CryptoJSDemo;
```

## 约束与限制

#### 兼容性

在下述版本验证通过：

1. IDE: 4.1.3.322; SDK: openharmony ( API 11) 4.1.0.52; 测试设备: Mate40 pro (NOH-AN00); Rom: 2.0.0.52(C00E52R1P17log); RNOH: 0.72.11。

## API列表

**以下`C` 均为crypto-js导出的对象。**

#### Base

**静态方法**

| 名称              | 说明                             | 类型     | 是否必填 | 鸿蒙支持 |
| ----------------- | -------------------------------- | -------- | -------- | -------- |
| C.lib.Base.extend | 创建一个新对象并继承自指定对象。 | function | no       | yes      |

**API**

| 名称   | 说明                           | 类型     | 是否必填 | 鸿蒙支持 |
| ------ | ------------------------------ | -------- | -------- | -------- |
| create | 创建对象的实例。               | function | no       | yes      |
| mixIn  | 向对象中添加属性键值对。       | function | no       | yes      |
| clone  | 创建一个对象的克隆版本的新对象 | function | no       | yes      |

#### WordArray

**属性**

| 名称     | 说明                     | 类型     | 是否必填 | 鸿蒙支持 |
| -------- | ------------------------ | -------- | -------- | -------- |
| words    | 32位的字节数组。         | number[] | no       | yes      |
| sigBytes | 此字数组中的有效字节数。 | number   | no       | yes      |

**静态方法**

| 名称                   | 说明                               | 类型     | 是否必填 | 鸿蒙支持                        |
| ---------------------- | ---------------------------------- | -------- | -------- | ------------------------------- |
| C.lib.WordArray.create | 初始化新创建的字节数组。           | function | no       | yes                             |
| C.lib.WordArray.random | 创建一个用随机字节填充的字节数组。 | function | no       | no (与android和ios一致均不支持) |

**API**

| 名称     | 说明                               | 类型     | 是否必填 | 鸿蒙支持 |
| -------- | ---------------------------------- | -------- | -------- | -------- |
| toString | 字节数组转换为字符串。             | function | no       | yes      |
| concat   | 将一个字节数组连接到这个字节数组。 | function | no       | yes      |
| clamp    | 移除无效字节。                     | function | no       | yes      |
| clone    | 复制数组，并创建新数组。           | function | no       | yes      |

#### CipherParams

**属性**

| 名称       | 说明                                                | 类型         | 是否必填 | 鸿蒙支持 |
| ---------- | --------------------------------------------------- | ------------ | -------- | -------- |
| ciphertext | 原始密文。                                          | WordArray    | no       | yes      |
| key        | 密文的Key。                                         | WordArray    | no       | yes      |
| iv         | 在加密操作中使用的IV。                              | WordArray    | no       | yes      |
| salt       | 与密钥推导函数一起使用的salt。                      | WordArray    | no       | yes      |
| algorithm  | 密码算法。                                          | CipherStatic | no       | yes      |
| mode       | 加密操作中使用的块模式。                            | Mode         | no       | yes      |
| padding    | 加密操作中使用的填充方案。                          | Padding      | no       | yes      |
| blockSize  | 密码的块大小。                                      | number       | no       | yes      |
| formatter  | 将此cipher params对象转换为字符串的默认格式化策略。 | Format       | no       | yes      |

**静态方法**

| 名称                      | 说明                              | 类型     | 是否必填 | 鸿蒙支持 |
| ------------------------- | --------------------------------- | -------- | -------- | -------- |
| C.lib.CipherParams.create | 初始化新创建的cipher params对象。 | function | no       | yes      |

**API**

| 名称     | 说明                                | 类型     | 是否必填 | 鸿蒙支持 |
| -------- | ----------------------------------- | -------- | -------- | -------- |
| toString | 将此cipher params对象转换为字符串。 | function | no       | yes      |

#### X64

**静态方法**

| 名称              | 说明                   | 类型     | 是否必填 | 鸿蒙支持 |
| ----------------- | ---------------------- | -------- | -------- | -------- |
| C.x64.Word.create | 初始化新创建的64位字。 | function | no       | yes      |

#### X64WordArray

**属性**

| 名称     | 说明                          | 类型     | 是否必填 | 鸿蒙支持 |
| -------- | ----------------------------- | -------- | -------- | -------- |
| words    | CryptoJS.x64.Word对象的数组。 | number[] | no       | yes      |
| sigBytes | 此字数组中的有效字节数。      | number   | no       | yes      |

**静态方法**

| 名称                   | 说明                     | 类型     | 是否必填 | 鸿蒙支持 |
| ---------------------- | ------------------------ | -------- | -------- | -------- |
| C.x64.WordArray.create | 初始化新创建的单词数组。 | function | no       | yes      |

**API**

| 名称  | 说明                             | 类型     | 是否必填 | 鸿蒙支持 |
| ----- | -------------------------------- | -------- | -------- | -------- |
| toX32 | 将此64位字数组转换为32位字数组。 | function | no       | yes      |
| clone | 创建此字节数组的副本。           | function | no       | yes      |

#### mode

**常量**

| 名称       | 说明             | 类型 | 是否必填 | 鸿蒙支持 |
| ---------- | ---------------- | ---- | -------- | -------- |
| C.mode.CBC | 密码块链模式。   | /    | no       | yes      |
| C.mode.CFB | 密码反馈块模式。 | /    | no       | yes      |
| C.mode.CTR | 计数器阻塞模式。 | /    | no       | yes      |
| C.mode.OFB | 输出反馈块模式。 | /    | no       | yes      |
| C.mode.ECB | 电子码本块模式。 | /    | no       | yes      |

#### pad.Pkcs7

**静态方法**

| 名称              | 说明                                           | 类型     | 是否必填 | 鸿蒙支持 |
| ----------------- | ---------------------------------------------- | -------- | -------- | -------- |
| C.pad.Pkcs7.pad   | 使用PKCS  #5/7中定义的算法填充数据。           | function | no       | yes      |
| C.pad.Pkcs7.unpad | 取消填充使用PKCS  #5/7中定义的算法填充的数据。 | function | no       | yes      |

#### pad.AnsiX923

**静态方法**

| 名称                 | 说明                                         | 类型     | 是否必填 | 鸿蒙支持 |
| -------------------- | -------------------------------------------- | -------- | -------- | -------- |
| C.pad.AnsiX923.pad   | 使用AnsiX923中定义的算法填充数据。           | function | no       | yes      |
| C.pad.AnsiX923.unpad | 取消填充使用AnsiX923中定义的算法填充的数据。 | function | no       | yes      |

#### pad.Iso10126

**静态方法**

| 名称                 | 说明                                         | 类型     | 是否必填 | 鸿蒙支持                        |
| -------------------- | -------------------------------------------- | -------- | -------- | ------------------------------- |
| C.pad.Iso10126.pad   | 使用Iso10126中定义的算法填充数据。           | function | no       | no (与android和ios一致均不支持) |
| C.pad.Iso10126.unpad | 取消填充使用Iso10126中定义的算法填充的数据。 | function | no       | yes                             |

#### pad.ZeroPadding

**静态方法**

| 名称                    | 说明                                            | 类型     | 是否必填 | 鸿蒙支持 |
| ----------------------- | ----------------------------------------------- | -------- | -------- | -------- |
| C.pad.ZeroPadding.pad   | 使用ZeroPadding中定义的算法填充数据。           | function | no       | yes      |
| C.pad.ZeroPadding.unpad | 取消填充使用ZeroPadding中定义的算法填充的数据。 | function | no       | yes      |

#### pad.NoPadding

**常量**

| 名称            | 说明             | 类型 | 是否必填 | 鸿蒙支持 |
| --------------- | ---------------- | ---- | -------- | -------- |
| C.pad.NoPadding | 不使用填充规则。 | /    | no       | yes      |

#### algo

**静态方法**

| 名称                    | 说明                                | 类型     | 是否必填 | 鸿蒙支持 |
| ----------------------- | ----------------------------------- | -------- | -------- | -------- |
| C.algo.MD5.create       | 初始化MD5加密新创建的工具类。       | function | no       | yes      |
| C.MD5                   | MD5加密。                           | function | no       | yes      |
| C.algo.SHA1.create      | 初始化SHA1加密新创建的工具类。      | function | no       | yes      |
| C.SHA1                  | SHA1加密。                          | function | no       | yes      |
| C.algo.SHA256.create    | 初始化SHA256加密新创建的工具类。    | function | no       | yes      |
| C.SHA256                | SHA256加密                          | function | no       | yes      |
| C.algo.SHA224.create    | 初始化SHA224加密新创建的工具类。    | function | no       | yes      |
| C.SHA224                | SHA224加密。                        | function | no       | yes      |
| C.algo.SHA512.create    | 初始化SHA512加密新创建的工具类。    | function | no       | yes      |
| C.SHA512                | SHA512加密。                        | function | no       | yes      |
| C.algo.SHA3.create      | 初始化SHA3加密新创建的工具类。      | function | no       | yes      |
| C.SHA3                  | SHA3加密。                          | function | no       | yes      |
| C.algo.SHA384.create    | 初始化SHA384加密新创建的工具类。    | function | no       | yes      |
| C.SHA384                | SHA384加密。                        | function | no       | yes      |
| C.algo.RIPEMD160.create | 初始化RIPEMD160加密新创建的工具类。 | function | no       | yes      |
| C.RIPEMD160             | RIPEMD160加密。                     | function | no       | yes      |

#### Hasher

**属性**

| 名称      | 说明                                                    | 类型   | 是否必填 | 鸿蒙支持 |
| --------- | ------------------------------------------------------- | ------ | -------- | -------- |
| blockSize | 哈希运算的32位字节块大小。缺省值：16（32*16=512bits）。 | number | no       | yes      |

**API**

| 名称     | 说明                   | 类型     | 是否必填 | 鸿蒙支持 |
| -------- | ---------------------- | -------- | -------- | -------- |
| reset    | 重置hasher为初始状态。 | function | no       | yes      |
| update   | 更新hasher的信息。     | function | no       | yes      |
| finalize | 结束hasher操作。       | function | no       | yes      |

#### HMAC

**静态方法**

| 名称               | 说明                 | 类型     | 是否必填 | 鸿蒙支持 |
| :----------------- | -------------------- | -------- | -------- | -------- |
| C.HmacMD5          | HmacMD5加密。        | function | no       | yes      |
| C.HmacSHA1         | HmacSHA1加密。       | function | no       | yes      |
| C.HmacSHA256       | HmacSHA256加密。     | function | no       | yes      |
| C.HmacSHA224       | HmacSHA224加密。     | function | no       | yes      |
| C.HmacSHA512       | HmacSHA512加密。     | function | no       | yes      |
| C.HmacSHA384       | HmacSHA384加密。     | function | no       | yes      |
| C.HmacSHA3         | HmacSHA3加密。       | function | no       | yes      |
| C.HmacRIPEMD160    | HmacRIPEMD160加密。  | function | no       | yes      |
| C.algo.HMAC.create | 初始化新创建的HMAC。 | function | no       | yes      |

**API**

| 名称     | 说明                                                         | 类型     | 是否必填 | 鸿蒙支持 |
| :------- | ------------------------------------------------------------ | -------- | -------- | -------- |
| reset    | 将此HMAC重置为其初始状态。                                   | function | no       | yes      |
| update   | 使用消息更新此HMAC。                                         | function | no       | yes      |
| finalize | 最终完成HMAC计算。     请注意，finally操作实际上是一个破坏性的、读一次的操作。 | function | no       | yes      |

#### AES

**静态方法**

| 名称                       | 说明                        | 类型     | 是否必填 | 鸿蒙支持 | 备注                                                         |
| :------------------------- | --------------------------- | -------- | -------- | -------- | ------------------------------------------------------------ |
| C.AES.encrypt              | AES算法加密。               | function | no       | yes      | 密码必须使用WordArray格式参数，不支持设置为string类型(与android/ios效果一致)。 |
| C.AES.decrypt              | AES算法解密。               | function | no       | yes      | 密码必须使用WordArray格式参数，不支持设置为string类型(与android/ios效果一致)。 |
| C.algo.AES.createEncryptor | 在AES加密模式下创建此密码。 | function | no       | yes      |                                                              |

#### DES

**静态方法**

| 名称                       | 说明                        | 类型     | 是否必填 | 鸿蒙支持 | 备注                                                         |
| :------------------------- | --------------------------- | -------- | -------- | -------- | ------------------------------------------------------------ |
| C.DES.encrypt              | DES算法加密。               | function | no       | yes      | 密码必须使用WordArray格式参数，不支持设置为string类型(与android/ios效果一致)。 |
| C.DES.decrypt              | DES算法解密。               | function | no       | yes      | 密码必须使用WordArray格式参数，不支持设置为string类型(与android/ios效果一致)。 |
| C.algo.DES.createEncryptor | 在DES加密模式下创建此密码。 | function | no       | yes      |                                                              |

#### TripleDES

**静态方法**

| 名称                             | 说明                              | 类型     | 是否必填 | 鸿蒙支持 | 备注                                                         |
| :------------------------------- | --------------------------------- | -------- | -------- | -------- | ------------------------------------------------------------ |
| C.TripleDES.encrypt              | TripleDES算法加密。               | function | no       | yes      | 密码必须使用WordArray格式参数，不支持设置为string类型(与android/ios效果一致)。 |
| C.TripleDES.decrypt              | TripleDES算法解密。               | function | no       | yes      | 密码必须使用WordArray格式参数，不支持设置为string类型(与android/ios效果一致)。 |
| C.algo.TripleDES.createEncryptor | 在TripleDES加密模式下创建此密码。 | function | no       | yes      |                                                              |

#### RC4

**静态方法**

| 名称                       | 说明                        | 类型     | 是否必填 | 鸿蒙支持 | 备注                                                         |
| :------------------------- | --------------------------- | -------- | -------- | -------- | ------------------------------------------------------------ |
| C.RC4.encrypt              | RC4算法加密。               | function | no       | yes      | 密码必须使用WordArray格式参数，不支持设置为string类型(与android/ios效果一致)。 |
| C.RC4.decrypt              | RC4算法解密。               | function | no       | yes      | 密码必须使用WordArray格式参数，不支持设置为string类型(与android/ios效果一致)。 |
| C.algo.RC4.createEncryptor | 在RC4加密模式下创建此密码。 | function | no       | yes      |                                                              |

#### RC4Drop

**静态方法**

| 名称                          | 说明                            | 类型     | 是否必填 | 鸿蒙支持 | 备注                                                         |
| :---------------------------- | ------------------------------- | -------- | -------- | -------- | ------------------------------------------------------------ |
| C.RC4Drop.encrypt             | RC4Drop算法加密。               | function | no       | yes      | 密码必须使用WordArray格式参数，不支持设置为string类型(与android/ios效果一致)。 |
| C.RC4Drop.decrypt             | RC4Drop算法解密。               | function | no       | yes      | 密码必须使用WordArray格式参数，不支持设置为string类型(与android/ios效果一致)。 |
| C.algo.RC4Drop.createEncrypto | 在RC4Drop加密模式下创建此密码。 | function | no       | yes      |                                                              |

#### Rabbit

**静态方法**

| 名称                          | 说明                           | 类型     | 是否必填 | 鸿蒙支持 | 备注                                                         |
| :---------------------------- | ------------------------------ | -------- | -------- | -------- | ------------------------------------------------------------ |
| C.Rabbit.encrypt              | Rabbit算法加密。               | function | no       | yes      | 密码必须使用WordArray格式参数，不支持设置为string类型(与android/ios效果一致)。 |
| C.Rabbit.decrypt              | Rabbit算法解密。               | function | no       | yes      | 密码必须使用WordArray格式参数，不支持设置为string类型(与android/ios效果一致)。 |
| C.algo.Rabbit.createEncryptor | 在Rabbit加密模式下创建此密码。 | function | no       | yes      |                                                              |

#### RabbitLegacy

**静态方法**

| 名称                                | 说明                                 | 类型     | 是否必填 | 鸿蒙支持 | 备注                                                         |
| :---------------------------------- | ------------------------------------ | -------- | -------- | -------- | ------------------------------------------------------------ |
| C.RabbitLegacy.encrypt              | RabbitLegacy算法加密。               | function | no       | yes      | 密码必须使用WordArray格式参数，不支持设置为string类型(与android/ios效果一致)。 |
| C.RabbitLegacy.decrypt              | RabbitLegacy算法解密。               | function | no       | yes      | 密码必须使用WordArray格式参数，不支持设置为string类型(与android/ios效果一致)。 |
| C.algo.RabbitLegacy.createEncryptor | 在RabbitLegacy加密模式下创建此密码。 | function | no       | yes      |                                                              |

#### Cipher

**属性**

| 名称    | 说明                                 | 类型   | 是否必填 | 鸿蒙支持 |
| :------ | ------------------------------------ | ------ | -------- | -------- |
| keySize | 此密码的密钥大小。缺省值：4（128位） | number | no       | yes      |
| ivSize  | 此密码的Iv大小。缺省值：4（128位）   | number | no       | yes      |

**API**

| 名称     | 说明                                                         | 类型     | 是否必填 | 鸿蒙支持 |
| :------- | ------------------------------------------------------------ | -------- | -------- | -------- |
| reset    | 将此密码重置为其初始状态。                                   | function | no       | yes      |
| process  | 添加需要加解密的数据。                                       | function | no       | yes      |
| finalize | 完成加密或解密过程。     请注意，finally操作实际上是一个破坏性的、一次读取的操作。 | function | no       | yes      |

#### Blowfish

**静态方法**

| 名称               | 说明           | 类型     | 是否必填 | 鸿蒙支持 |
| :----------------- | -------------- | -------- | -------- | -------- |
| C.Blowfish.encrypt | Blowfish加密。 | function | no       | yes      |
| C.Blowfish.decrypt | Blowfish解密。 | function | no       | yes      |

#### SerializableCipher

**静态方法**

| 名称                             | 说明                 | 类型     | 是否必填 | 鸿蒙支持 |
| :------------------------------- | -------------------- | -------- | -------- | -------- |
| C.lib.SerializableCipher.encrypt | 对信息进行加密。     | function | no       | yes      |
| C.lib.SerializableCipher.decrypt | 对加密信息进行解密。 | function | no       | yes      |

#### PasswordBasedCipher

**静态方法**

| 名称                              | 说明                 | 类型     | 是否必填 | 鸿蒙支持 | 备注                                                         |
| :-------------------------------- | -------------------- | -------- | -------- | -------- | ------------------------------------------------------------ |
| C.lib.PasswordBasedCipher.encrypt | 对信息进行加密。     | function | no       | yes      | 必须传入有效的salt参数，不传入salt参数时不支持(与android/ios效果一致)。 |
| C.lib.PasswordBasedCipher.decrypt | 对加密信息进行解密。 | function | no       | yes      | 必须传入有效的salt参数，不传入salt参数时不支持(与android/ios效果一致)。 |

#### kdf.OpenSSL

**静态方法**

| 名称                  | 说明                 | 类型     | 是否必填 | 鸿蒙支持 | 备注                                                         |
| :-------------------- | -------------------- | -------- | -------- | -------- | ------------------------------------------------------------ |
| C.kdf.OpenSSL.execute | 从密码派生密钥和IV。 | function | no       | yes      | 必须传入有效的salt参数，不传入salt参数时不支持(与android/ios效果一致)。 |

#### kdf.PBKDF2

**静态方法**

| 名称                 | 说明                               | 类型     | 是否必填 | 鸿蒙支持 |
| :------------------- | ---------------------------------- | -------- | -------- | -------- |
| C.algo.PBKDF2.create | 初始化PBKDF2新创建的密钥推导函数。 | function | no       | yes      |
| C.PBKDF2             | PBKDF2派生密钥。                   | function | no       | yes      |

**API**

| 名称    | 说明                               | 类型     | 是否必填 | 鸿蒙支持 |
| :------ | ---------------------------------- | -------- | -------- | -------- |
| compute | 计算基于PBKDF2密码的密钥派生函数。 | function | no       | yes      |

#### EvpKDF

**静态方法**

| 名称                 | 说明                               | 类型     | 是否必填 | 鸿蒙支持 |
| :------------------- | ---------------------------------- | -------- | -------- | -------- |
| C.algo.EvpKDF.create | 初始化EvpKDF新创建的密钥推导函数。 | function | no       | yes      |
| C.EvpKDF             | EvpKDF派生密钥。                   | function | no       | yes      |

**API**

| 名称    | 说明                               | 类型     | 是否必填 | 鸿蒙支持 |
| :------ | ---------------------------------- | -------- | -------- | -------- |
| compute | 计算基于EvpKDF密码的密钥派生函数。 | function | no       | yes      |

#### format

**静态方法**

| 名称                       | 说明                                        | 类型     | 是否必填 | 鸿蒙支持 |
| :------------------------- | ------------------------------------------- | -------- | -------- | -------- |
| C.format.OpenSSL.stringify | 将CipherParams对象转换为OpenSSL兼容字符串。 | function | no       | yes      |
| C.format.OpenSSL.parse     | 将OpenSSL兼容字符串转换为CipherParams对象。 | function | no       | yes      |
| C.format.Hex.stringify     | 将CipherParams对象转换为16进制字符串。      | function | no       | yes      |
| C.format.Hex.parse         | 将16进制字符串转换为CipherParams对象。      | function | no       | yes      |

#### enc/Encoder

**静态方法**

| 名称                      | 说明                                  | 类型     | 是否必填 | 鸿蒙支持 |
| :------------------------ | ------------------------------------- | -------- | -------- | -------- |
| C.enc.Hex.stringify       | 将字节数组转换为十六进制字符串。      | function | no       | yes      |
| C.enc.Hex.parse           | 将十六进制字符串转换为字节数组。      | function | no       | yes      |
| C.enc.Latin1.stringify    | 将字节数组转换为Latin1格式字符串。    | function | no       | yes      |
| C.enc.Latin1.parse        | 将Latin1格式字符串转换为字节数组。    | function | no       | yes      |
| C.enc.Utf8.stringify      | 将字节数组转换为UTF-8格式字符串。     | function | no       | yes      |
| C.enc.Utf8.parse          | 将UTF-8格式字符串转换为字节数组。     | function | no       | yes      |
| C.enc.Utf16.stringify     | 将字节数组转换为UTF-16格式字符串。    | function | no       | yes      |
| C.enc.Utf16.parse         | 将UTF-16格式字符串转换为字节数组。    | function | no       | yes      |
| C.enc.Utf16BE.stringify   | 将字节数组转换为UTF-16 BE格式字符串。 | function | no       | yes      |
| C.enc.Utf16BE.parse       | 将UTF-16 BE格式字符串转换为字节数组。 | function | no       | yes      |
| C.enc.Utf16LE.stringify   | 将字节数组转换为UTF-16 LE格式字符串。 | function | no       | yes      |
| C.enc.Utf16LE.parse       | 将UTF-16 LE格式字符串转换为字节数组。 | function | no       | yes      |
| C.enc.Base64.stringify    | 将字节数组转换为Base64格式字符串。    | function | no       | yes      |
| C.enc.Base64.parse        | 将Base64格式字符串转换为字节数组。    | function | no       | yes      |
| C.enc.Base64url.stringify | 将字节数组转换为Base64url格式字符串。 | function | no       | yes      |
| C.enc.Base64url.parse     | 将Base64url格式字符串转换为字节数组。 | function | no       | yes      |

## 遗留问题

## 其他

## 开源协议

本项目基于 [MIT License](https://github.com/brix/crypto-js/blob/4.2.0/LICENSE) ，请自由地享受和参与开源。
