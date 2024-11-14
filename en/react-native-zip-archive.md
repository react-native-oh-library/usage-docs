> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-zip-archive</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/mockingbot/react-native-zip-archive">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/mockingbot/react-native-zip-archive/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>


> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-zip-archive)

## 安装与使用

Find the matching version information in the release address of a third-party library：[@react-native-oh-tpl/react-native-zip-archive Releases](https://github.com/react-native-oh-library/react-native-zip-archive/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

进入到工程目录并输入以下命令：


<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-zip-archive
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-zip-archive
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React, { useState, useEffect } from 'react';
import { View, Button, StyleSheet, TextInput, Alert, Text, ActivityIndicator } from 'react-native';
import { pathParameters, zip, unzip, zipWithPassword, unzipWithPassword, subscribe, creteFile, isPasswordProtected, unzipAssets, getUncompressedSize } from 'react-native-zip-archive';
import { ProgressBar } from 'react-native-paper';

export default function ZipArchiveDemo() {
    const [fileName, setFileName] = useState('');
    const [fileContent, setFileContent] = useState('');
    const [createdFilePath, setCreatedFilePath] = useState('');
    const [compressedFilePath, setCompressedFilePath] = useState('');

    const [newZipPath, setNewZipPath]: any = useState();
    const [newSourcePath, setNewSourcePath]: any = useState();
    const [newFolder, setNewFolder]: any = useState();
    const [password, setPassword] = useState('');
    const [showInput, setShowInput] = useState(false);
    const [zipPassword, setZipPassword] = useState('');
    const [progress, setProgress] = useState(0);
    const [isProgressPing, setIsProgressPing] = useState<boolean>(false);
    const [loading, setLoading] = useState(false);
    const [unzipStatus, setUnzipStatus] = useState('');
    const [uncompressSize, setUncompressSize] = useState('');
    let unzipPassword: string = '';
    let needPassword: boolean = false;

    // 存储设置的密码
    const setUnzipPassword = (value: string) => {
        console.log(`setUnzipPassword: ${value}`);
        unzipPassword = value;
    }

    useEffect(() => {
        let filesDir = pathParameters(); // 获取 HarmonyOS 应用文件路径
        let newZipPath: any = filesDir + '.zip';
        let newSourcePath: any = filesDir;
        let newFolder: any = filesDir + 'Out';//解压时新建个文件夹

        setNewZipPath(newZipPath);//存储压缩包
        setNewSourcePath(newSourcePath);//原文件路径
        setNewFolder(newFolder);//解压时新建个文件夹

        if (!showInput) {
            setPassword(''); // 隐藏输入框时清空密码
        }
    }, [showInput]);

    // 创建文件
    const createFile = () => {
        if (!fileName || !fileContent) {
            Alert.alert('文件名和内容不能为空');
            return;
        }
        const filePath = `${newSourcePath}/${fileName}.txt`;

        if (fileName && fileContent) {
            creteFile(filePath, fileContent)
                .then(() => {
                    setCreatedFilePath(filePath);
                    Alert.alert('文件创建成功')
                    setTimeout(() => {
                        setFileName('');
                        setFileContent('');
                    }, 100);
                })
                .catch((error) => {
                    console.log('文件创建失败:', error);
                });
        } else {
            Alert.alert('请输入文件名和内容');
        }
    };

    // 密码压缩
    const handleZipPress = () => {
        if (password === '') {
            Alert.alert('错误', '请输入密码');
            return;
        }
       
        if (createdFilePath) {
            handleProgress();//进度条
            zipWithPassword(newSourcePath, newZipPath, password)
                .then(() => {
                    console.log(`password--11:${password}`)
                    setZipPassword(password);
                    setCompressedFilePath(newZipPath)
                    Alert.alert('成功', '已使用密码创建压缩');
                })
                .catch(error => {
                    Alert.alert('错误', `创建压缩文件失败: ${error}`);
                });
        } else {
            Alert.alert('无文件可供压缩');
        }
    };

    // 解压时是否需要密码
    const isUnzipWithPassword = () => {
        if (unzipPassword) {
            if (zipPassword === '') {
                Alert.alert('错误', '请先进行压缩并设置密码');
                return;
            }

            if (unzipPassword === zipPassword) {
                handleGetUncompressedSize();
                handleProgress();//进度条
                unzipWithPassword(newZipPath,newFolder, unzipPassword)
                    .then(() => {
                        Alert.alert('成功', '已使用密码解压文件');
                    })
                    .catch(error => {
                        Alert.alert('错误', `解压文件失败: ${error}`);
                    });

            } else {
                Alert.alert('密码输入错误');
            }
        } else {
            Alert.alert('错误', '请先输入密码');
        }
    }

    // 密码解压&解压
    const handleUnzipPress = () => {
        if (this.needPassword) {
            isUnzipWithPassword();
            setShowInput(true);
            return;
        }
        isPasswordProtected(newZipPath)
            .then((res) => {
                if (res) {
                    this.needPassword = true;
                    setShowInput(true);
                } else {
                    if (compressedFilePath) {
                        if (needPassword === false) {
                            handleGetUncompressedSize();
                            handleProgress();//进度条
                            unzip(newZipPath, newFolder,'UTF-8')
                                .then(() => {
                                    console.log(`unzip success`)
                                    Alert.alert('成功', '已解压');
                                })
                                .catch(error => {
                                    Alert.alert('错误', '解压失败');
                                    console.log(`unzip error: ${error}`);
                                })
                        }
                    } else {
                        Alert.alert('无压缩文件可供解压');
                    }
                }
            })
            .catch(error => {
                console.error(`isPasswordProtected error: ${error}`)
            })
    }

    // 进度条
    const handleProgress = () => {
        setIsProgressPing(true);
        setProgress(0); //重置进度条
        interface data {
            progress: number,
            filePath: string
        }
        let currentProgress = 0;

        const interval = setInterval(() => {
            if (currentProgress < 100) {
                currentProgress += 20;
                setProgress(currentProgress);
                console.log(`current progress: ${currentProgress}%`);
            } else {
                clearInterval(interval); // 达到最大值后清除 interval
                setIsProgressPing(false);
            }
        }, 1000);

        subscribe((data: data) => {
            try {
                if (data.progress != null) {
                    currentProgress = data.progress;
                    setProgress(data.progress);
                    console.log(`subscribe success: ${data.progress}`);
                    setIsProgressPing(false);

                    if (data.progress === 100) {
                        clearInterval(interval);
                    }
                }
            } catch (error) {
                console.log(`subscribe error: ${error}`);
                clearInterval(interval);
            }
        })
    }

    // unzipAssets
    const handleUnzipAssets = async () => {
        setLoading(true);
        let filesDir = pathParameters();
        //解压files.zip文件到系统中的 destinationFolder 目录中
        let assetPath = filesDir + '.zip';
        let targetPath = filesDir + 'destinationFolder';
        if (compressedFilePath) {
            try {
                await unzipAssets(assetPath, targetPath);
                setUnzipStatus('解压完成');
                console.log(`unzipAssets success`);
            } catch (err) {
                setUnzipStatus(`解压失败：${err}`);
                console.log(`unzipAssets err: ${err}`);
            } finally {
                setLoading(false);
            }
        } else {
            Alert.alert('无压缩文件可供解压');
        }
    }

    // getUncompressedSize
    const handleGetUncompressedSize = () => {
        getUncompressedSize(newZipPath)
            .then((uncompressSize:any) => {
                setUncompressSize(uncompressSize);
                console.log(`uncompressSize success:${uncompressSize}`)
            })
            .catch((err) => {
                console.log(`getUncompressedSize err:${err}`)
            })
    }

    return (
        <View style={styles.content}>
            <View style={styles.buttonSix}>
                <View>
                    <Text>解压缩后的大小:{uncompressSize ? uncompressSize : '0'}字节</Text>
                    <View style={styles.progressBar}>
                        <View style={{ width: `${progress}%`, backgroundColor: '#00AEEF', height: '100%' }}></View>
                    </View>
                    <Text style={styles.percentageText}>{progress}%</Text>
                </View>
            </View>

            <View >
                <View >
                    <TextInput
                        placeholder="请输入文件名"
                        value={fileName}
                        onChangeText={setFileName}
                        style={{ borderWidth: 1, padding: 10, width: '70%' }}
                    />
                    <TextInput
                        style={{
                            height: 100,
                            borderColor: 'gray',
                            borderWidth: 1,
                            width: 200,
                            padding: 10,
                            marginBottom: 10,
                            marginTop: 10
                        }}
                        onChangeText={text => setFileContent(text)}
                        value={fileContent}
                        placeholder="文件内容"
                        multiline={true}
                    />
                    <Button title="创建文件" onPress={createFile} />
                </View>
            </View>

            <View style={styles.buttonSix}>
                <Button title='压缩' disabled={!createdFilePath} onPress={() => {
                    if (createdFilePath) {
                        handleProgress();//进度条
                        zip(newSourcePath, newZipPath)
                            .then(() => {
                                setCompressedFilePath(newZipPath)
                                Alert.alert('成功', '已压缩');
                            })
                            .catch(error => {
                                Alert.alert('错误', `压缩失败: ${error}`);
                            })
                    } else {
                        Alert.alert('无文件可供压缩');
                    }
                }} />
            </View>

            <View>
                <TextInput
                    style={styles.input}
                    placeholder="设置压缩密码"
                    onChangeText={text => setPassword(text)}
                    value={password}
                />
            </View>
            <View style={styles.buttonSix}>
                <Button title='密码压缩' disabled={!createdFilePath} onPress={handleZipPress} />
            </View>

            {showInput && (
                <View>
                    <TextInput
                        style={styles.input}
                        placeholder="输入解压密码"
                        onChangeText={text => setUnzipPassword(text)}
                    />
                </View>
            )}

            <View style={styles.buttonSix}>
                <Button title="解压" disabled={!createdFilePath} onPress={handleUnzipPress} />
            </View>
        </View>
    )
}

const styles = StyleSheet.create({
    content: {
        display: 'flex',
        justifyContent: 'center',
        alignItems: 'center',
        marginTop: 56
    },
    buttonSix: {
        width: '65%',
        marginBottom: 10,
        marginTop: 20
    },
    input: {
        borderWidth: 1,
        padding: 10,
        width: 300
    },
    container: {
        flex: 1,
        justifyContent: 'center',
        alignItems: 'center',
    },
    progressBar: {
        width: 250,
        height: 20,
        backgroundColor: '#E0E0E0',
        borderRadius: 10,
        overflow: 'hidden',
        marginTop: 10
    },
    percentageText: {
        marginTop: 5,
        fontSize: 16
    }
})
```

## 使用 Codegen

本库已经适配了 `Codegen` ，在使用前需要主动执行生成三方库桥接代码，详细请参考[ Codegen 使用文档](/zh-cn/codegen.md)。

## Link

目前 HarmonyOS 暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`

### 1.在工程根目录的 `oh-package.json5` 添加 overrides 字段

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "./react_native_openharmony"
  }
}
```

### 2.引入原生端代码

目前有两种方法：

1. 通过 har 包引入（在 IDE 完善相关功能后该方法会被遗弃，目前首选此方法）；
2. 直接链接源码。

方法一：通过 har 包引入（推荐）

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
+   "@react-native-oh-tpl/react-native-zip-archive": "file:../../node_modules/@react-native-oh-tpl/react-native-zip-archive/harmony/zipArchive_package.har"
  }
```

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

方法二：直接链接源码

> [!TIP] 如需使用直接链接源码，请参考[直接链接源码说明](/zh-cn/link-source-code.md)

### 3.配置 CMakeLists 和引入zipArchive

打开 `entry/src/main/cpp/CMakeLists.txt`，添加：

```diff
project(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(CMAKE_SKIP_BUILD_RPATH TRUE)
set(RNOH_APP_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
set(NODE_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../node_modules")
+ set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
set(RNOH_CPP_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../../react-native-harmony/harmony/cpp")
set(LOG_VERBOSITY_LEVEL 1)
set(CMAKE_ASM_FLAGS "-Wno-error=unused-command-line-argument -Qunused-arguments")
set(CMAKE_CXX_FLAGS "-fstack-protector-strong -Wl,-z,relro,-z,now,-z,noexecstack -s -fPIE -pie")
set(WITH_HITRACE_SYSTRACE 1) # for other CMakeLists.txt files to use
add_compile_definitions(WITH_HITRACE_SYSTRACE)

add_subdirectory("${RNOH_CPP_DIR}" ./rn)

# RNOH_BEGIN: manual_package_linking_1
add_subdirectory("../../../../sample_package/src/main/cpp" ./sample-package)
+ add_subdirectory("${OH_MODULES}/@react-native-oh-tpl/react-native-zip-archive/src/main/cpp" ./zipArchive-package)
# RNOH_END: manual_package_linking_1

file(GLOB GENERATED_CPP_FILES "./generated/*.cpp")

add_library(rnoh_app SHARED
    ${GENERATED_CPP_FILES}
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)
target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: manual_package_linking_2
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC nativi_minizip)
# RNOH_END: manual_package_linking_2
```

### 4.在 ArkTs 侧引入 ZipArchivePackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
+ import {ZipArchivePackage} from '@react-native-oh-tpl/react-native-zip-archive/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new ZipArchivePackage(ctx)
  ];
}
```

### 5.运行

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

然后编译、运行即可。

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-library/react-native-zip-archive Releases](https://github.com/react-native-oh-library/react-native-zip-archive/releases)

## API

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                | Description                                                  | Type    | Required | Platform | HarmonyOS Support |
| ------------------- | ------------------------------------------------------------ | ------- | -------- | -------- | ----------------- |
| zip                 | File or folder compression                                   | string  | no       | All      | yes               |
| unzip               | Decompression of files or folders                            | string  | no       | All      | yes               |
| zipWithPassword     | Compress files or folders with a password                    | string  | no       | All      | yes               |
| unzipWithPassword   | Extract files or folders with a password                     | string  | no       | All      | yes               |
| isPasswordProtected | Check if the password exists during password decompression   | boolean | no       | All      | yes               |
| unzipAssets         | Pass in the specified directory during decompression         | string  | no       | All      | yes               |
| getUncompressedSize | File size after decompression                                | number  | no       | All      | yes               |
| subscribe           | Display progress bar during compression and password decompression | void    | no       | All      | yes               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/mockingbot/react-native-zip-archive/blob/master/LICENSE) ，请自由地享受和参与开源。
