> Template version: v0.2.2

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


> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-zip-archive)

## Installation and Usage

Find the matching version information in the release address of a third-party library：[@react-native-oh-tpl/react-native-zip-archive Releases](https://github.com/react-native-oh-library/react-native-zip-archive/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:


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

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

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

    const setUnzipPassword = (value: string) => {
        console.log(`setUnzipPassword: ${value}`);
        unzipPassword = value;
    }

    useEffect(() => {
        let filesDir = pathParameters(); 
        let newZipPath: any = filesDir + '.zip';
        let newSourcePath: any = filesDir;
        let newFolder: any = filesDir + 'Out';

        setNewZipPath(newZipPath);
        setNewSourcePath(newSourcePath);
        setNewFolder(newFolder);

        if (!showInput) {
            setPassword(''); 
        }
    }, [showInput]);

    const createFile = () => {
        if (!fileName || !fileContent) {
            Alert.alert('The file name and content cannot be empty.');
            return;
        }
        const filePath = `${newSourcePath}/${fileName}.txt`;

        if (fileName && fileContent) {
            creteFile(filePath, fileContent)
                .then(() => {
                    setCreatedFilePath(filePath);
                    Alert.alert('File created successfully')
                    setTimeout(() => {
                        setFileName('');
                        setFileContent('');
                    }, 100);
                })
                .catch((error) => {
                    console.log('File creation failed:', error);
                });
        } else {
            Alert.alert('Please enter the file name and content');
        }
    };

    const handleZipPress = () => {
        if (password === '') {
            Alert.alert('error', 'Please input a password');
            return;
        }
       
        if (createdFilePath) {
            handleProgress();
            zipWithPassword(newSourcePath, newZipPath, password)
                .then(() => {
                    console.log(`password--11:${password}`)
                    setZipPassword(password);
                    setCompressedFilePath(newZipPath)
                    Alert.alert('successful', 'Created compression using password');
                })
                .catch(error => {
                    Alert.alert('error', `Failed to create compressed file: ${error}`);
                });
        } else {
            Alert.alert('No files available for compression');
        }
    };

    const isUnzipWithPassword = () => {
        if (unzipPassword) {
            if (zipPassword === '') {
                Alert.alert('error', 'Please compress and set a password first');
                return;
            }

            if (unzipPassword === zipPassword) {
                handleGetUncompressedSize();
                handleProgress();
                unzipWithPassword(newZipPath,newFolder, unzipPassword)
                    .then(() => {
                        Alert.alert('success', 'The password has been used to decompress the file');
                    })
                    .catch(error => {
                        Alert.alert('error', `Failed to decompress file: ${error}`);
                    });

            } else {
                Alert.alert('Password input error');
            }
        } else {
            Alert.alert('error', 'Please enter your password first');
        }
    }

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
                            handleProgress();
                            unzip(newZipPath, newFolder,'UTF-8')
                                .then(() => {
                                    console.log(`unzip success`)
                                    Alert.alert('success', 'Decompressed');
                                })
                                .catch(error => {
                                    Alert.alert('error', 'Decompression failed');
                                    console.log(`unzip error: ${error}`);
                                })
                        }
                    } else {
                        Alert.alert('No compressed files available for decompression');
                    }
                }
            })
            .catch(error => {
                console.error(`isPasswordProtected error: ${error}`)
            })
    }

    const handleProgress = () => {
        setIsProgressPing(true);
        setProgress(0); 
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
                clearInterval(interval);
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

    const handleUnzipAssets = async () => {
        setLoading(true);
        let filesDir = pathParameters();
        let assetPath = filesDir + '.zip';
        let targetPath = filesDir + 'destinationFolder';
        if (compressedFilePath) {
            try {
                await unzipAssets(assetPath, targetPath);
                setUnzipStatus('Decompression completed');
                console.log(`unzipAssets success`);
            } catch (err) {
                setUnzipStatus(`Decompression failed：${err}`);
                console.log(`unzipAssets err: ${err}`);
            } finally {
                setLoading(false);
            }
        } else {
            Alert.alert('No compressed files available for decompression');
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
                    <Text>Size after decompression:{uncompressSize ? uncompressSize : '0'}byte</Text>
                    <View style={styles.progressBar}>
                        <View style={{ width: `${progress}%`, backgroundColor: '#00AEEF', height: '100%' }}></View>
                    </View>
                    <Text style={styles.percentageText}>{progress}%</Text>
                </View>
            </View>

            <View >
                <View >
                    <TextInput
                        placeholder="Please enter a file name"
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
                        placeholder="file content"
                        multiline={true}
                    />
                    <Button title="create a file" onPress={createFile} />
                </View>
            </View>

            <View style={styles.buttonSix}>
                <Button title='compress' disabled={!createdFilePath} onPress={() => {
                    if (createdFilePath) {
                        handleProgress();
                        zip(newSourcePath, newZipPath)
                            .then(() => {
                                setCompressedFilePath(newZipPath)
                                Alert.alert('success', 'compressed');
                            })
                            .catch(error => {
                                Alert.alert('error', `compressed failed: ${error}`);
                            })
                    } else {
                        Alert.alert('No files available for compression');
                    }
                }} />
            </View>

            <View>
                <TextInput
                    style={styles.input}
                    placeholder="Set compression password"
                    onChangeText={text => setPassword(text)}
                    value={password}
                />
            </View>
            <View style={styles.buttonSix}>
                <Button title='password compression' disabled={!createdFilePath} onPress={handleZipPress} />
            </View>

            {showInput && (
                <View>
                    <TextInput
                        style={styles.input}
                        placeholder="Enter decompression password"
                        onChangeText={text => setUnzipPassword(text)}
                    />
                </View>
            )}

            <View style={styles.buttonSix}>
                <Button title="extract" disabled={!createdFilePath} onPress={handleUnzipPress} />
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

## Use Codegen

If this repository has been adapted to `Codegen`, generate the bridge code of the third-party library by using the `Codegen`. For details, see [Codegen Usage Guide](/en/codegen.md).

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
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
+   "@react-native-oh-tpl/react-native-zip-archive": "file:../../node_modules/@react-native-oh-tpl/react-native-zip-archive/harmony/zipArchive_package.har"
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

### 3. CMakeLists and Introducing zipArchive Package

Open `entry/src/main/cpp/CMakeLists.txt` and add the following code:

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

### 4. Introducing ZipArchivePackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
+ import {ZipArchivePackage} from '@react-native-oh-tpl/react-native-zip-archive/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new ZipArchivePackage(ctx)
  ];
}
```

### 5. Running

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

Check the release version information in the release address of the third-party library: [@react-native-oh-library/react-native-zip-archive Releases](https://github.com/react-native-oh-library/react-native-zip-archive/releases)

## API

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

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

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/mockingbot/react-native-zip-archive/blob/master/LICENSE).
