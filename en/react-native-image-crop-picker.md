> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-image-crop-picker</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/ivpusic/react-native-image-crop-picker">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
        <a href="https://github.com/ivpusic/react-native-image-crop-picker/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-image-crop-picker)

## Installation and Usage

Find the matching version information in the release address of a third-party library：[@react-native-oh-tpl/react-native-image-crop-picker Releases ](https://github.com/react-native-oh-library/react-native-image-crop-picker/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:


#### **npm**

```
npm install @react-native-oh-tpl/react-native-image-crop-picker
```

#### **yarn**

```
yarn add @react-native-oh-tpl/react-native-image-crop-picker
```

The following code shows the basic use scenario of the repository:

> [!TIP] The name of the imported repository remains unchanged.

```
import ImagePicker from 'react-native-image-crop-picker';
import { openPicker } from 'react-native-image-crop-picker';
import React from 'react';
import { Text, StyleSheet, TextInput, View, Button, ScrollView, Switch } from 'react-native';

const ImageCropPickDemo = () => {
    const TAG: string = 'ImageCropPickerTurboModule';
    const [maxFiles, setMaxFiles] = React.useState('');
    const [imageQuality, setImageQuality] = React.useState('');
    const [imagePath, setImagePath] = React.useState('');
    const [clearImagePath, setClearImagePath] = React.useState('');
    const [cropperTitle, setCropperTitle] = React.useState('');
    const [chooseText, setChooseText] = React.useState('');
    const [chooseColor, setChooseColor] = React.useState('');
    const [cancelText, setCancelText] = React.useState('');
    const [cancelColor, setCancelColor] = React.useState('');
    const [cropperRotate, setCropperRotate] = React.useState(false);
    const [showCropGuidelines, setShowCropGuidelines] = React.useState(true);
    const [showCropFrame, setShowCropFrame] = React.useState(true);
    const [multiple, setMultiple] = React.useState(false);
    const [includeExif, setIncludeExif] = React.useState(false);
    const [avoidEmptySpace, setAvoidEmptySpace] = React.useState(false);
    const [writeTempFile, setTempFile] = React.useState(true);
    const [includeBase64, setBase64] = React.useState(false);
    const [freeStyleCropEnabled, setFreeStyleCropEnabled] = React.useState(false);
    const [forceJpg, setForceJpg] = React.useState(false);
    const [showsSelectedCount, setShowsSelectedCount] = React.useState(true);
    const [selectedButton, setSelectedButton] = React.useState('any');
    const [useFrontCamera, setUseFrontCamera] = React.useState(false);
    const [croppingCamera, setCroppingCamera] = React.useState(false);
    const [writeTempFileCamera, setTempFileCamera] = React.useState(true);
    const [includeBase64Camera, setBase64Camera] = React.useState(false);
    const [includeExifCamera, setIncludeExifCamera] = React.useState(false);
    const [avoidEmptySpaceCamera, setAvoidEmptySpaceCamera] = React.useState(false);
    const [freeStyleCropEnabledCamera, setFreeStyleCropEnabledCamera] = React.useState(false);
    const [forceJpgCamera, setForceJpgCamera] = React.useState(false);
    const [mediaTypeCamera, setMediaTypeCamera] = React.useState('any');
    const [imageQualityCamera, setImageQualityCamera] = React.useState('');
    const [cropperTitleCamera, setCropperTitleCamera] = React.useState('');
    const [chooseTextCamera, setChooseTextCamera] = React.useState('');
    const [chooseColorCamera, setChooseColorCamera] = React.useState('');
    const [cancelTextCamera, setCancelTextCamera] = React.useState('');
    const [cancelColorCamera, setCancelColorCamera] = React.useState('');
    const [cropperRotateCamera, setCropperRotateCamera] = React.useState(false);
    const [showCropGuidelinesCamera, setShowCropGuidelinesCamera] = React.useState(true);
    const [showCropFrameCamera, setShowCropFrameCamera] = React.useState(true);
    const [writeTempFileCropper, setTempFileCropper] = React.useState(true);
    const [forceJpgCropper, setForceJpgCropper] = React.useState(false);
    const [includeBase64Cropper, setBase64Cropper] = React.useState(false);
    const [includeExifCropper, setIncludeExifCropper] = React.useState(false);
    const [avoidEmptySpaceCropper, setAvoidEmptySpaceCropper] = React.useState(false);
    const [freeStyleCropEnabledCropper, setFreeStyleCropEnabledCropper] = React.useState(false);
    const [imageQualityCropper, setimageQualityCropper] = React.useState('');

    const handleButtonPress = (buttonName) => {
        setSelectedButton(buttonName);
    };

    const handleMediaType = (buttonName) => {
        setMediaTypeCamera(buttonName);
    };

    return (
        <ScrollView style={styles.container}>
            <Text style={styles.title}>Camera, Gallery, Cropping Functionality</Text>
            <View style={styles.container}>

                <View style={styles.TextInputBox}>

                    <Text style={styles.inputLable}>multiple:</Text>
                    <Button
                        title={`${multiple}`}
                        onPress={() => multiple ? setMultiple(false) : setMultiple(true)}
                    />

                    <Text style={styles.inputLable}>writeTempFile:</Text>
                    <Button
                        title={`${writeTempFile}`}
                        onPress={() => writeTempFile ? setTempFile(false) : setTempFile(true)}
                    />
                </View>

                <View style={styles.TextInputBox}>

                    <Text style={styles.inputLable}>includeBase64:</Text>
                    <Button
                        title={`${includeBase64}`}
                        onPress={() => includeBase64 ? setBase64(false) : setBase64(true)}
                    />

                    <Text style={styles.inputLable}>includeExif:</Text>
                    <Button
                        title={`${includeExif}`}
                        onPress={() => includeExif ? setIncludeExif(false) : setIncludeExif(true)}
                    />

                </View>

                <View style={styles.TextInputBox}>

                    <Text style={styles.inputLable}>avoidEmptySpaceAroundImage :</Text>
                    <Button
                        title={`${avoidEmptySpace}`}
                        onPress={() => avoidEmptySpace ? setAvoidEmptySpace(false) : setAvoidEmptySpace(true)}
                    />

                </View>

                <View style={styles.TextInputBox}>

                    <Text style={styles.inputLable}>freeStyleCropEnabled :</Text>
                    <Button
                        title={`${freeStyleCropEnabled}`}
                        onPress={() => freeStyleCropEnabled ? setFreeStyleCropEnabled(false) : setFreeStyleCropEnabled(true)}
                    />

                </View>

                <View style={styles.TextInputBox}>

                    <Text style={styles.inputLable}>forceJpg:</Text>
                    <Button
                        title={`${forceJpg}`}
                        onPress={() => forceJpg ? setForceJpg(false) : setForceJpg(true)}
                    />

                    <Text style={styles.inputLable}>showsSelectedCount:</Text>
                    <Button
                        title={`${showsSelectedCount}`}
                        onPress={() => showsSelectedCount ? setShowsSelectedCount(false) : setShowsSelectedCount(true)}
                    />

                </View>


                <View style={styles.TextInputBox}>
                    <Text style={styles.inputLable}>mediaType:</Text>
                    <Button
                        title='photo'
                        onPress={() => handleButtonPress('photo')}
                        accessibilityState={{ selected: selectedButton === 'photo' }}
                    />
                    <Button
                        title='video'
                        onPress={() => handleButtonPress('video')}
                        accessibilityState={{ selected: selectedButton === 'video' }}
                    />
                    <Button
                        title='any'
                        onPress={() => handleButtonPress('any')}
                        accessibilityState={{ selected: selectedButton === 'any' }}
                    />
                </View>
                <View style={styles.TextInputBox}>
                     <Text style={{color:'red'}}>mediaType is {selectedButton}</Text>
                </View>

                <View style={styles.TextInputBox}>
                    <Text style={styles.inputLable}>minFiles:</Text>
                    <Text style={styles.inputLable}>1</Text>
                </View>

                <View style={styles.TextInputBox}>
                    <Text style={styles.inputLable}>maxFiles:</Text>
                    <TextInput
                       keyboardType="numeric"
                       maxLength={1}
                       style={styles.numberInput}
                       onChangeText={setMaxFiles}
                       value={maxFiles}
                    />
                    <Text style={styles.lableType}>(number)</Text>
                  </View>

                <View style={styles.TextInputBox}>
                    <Text style={styles.inputLable}>compressImageQuality:</Text>
                    <TextInput
                        style={styles.numberInput}
                        onChangeText={setImageQuality}
                        value={imageQuality}
                    />
                    <Text style={styles.lableType}>(0.1 到 1)</Text>
                </View>

                <View >
                    <View style={styles.buttonSty}>
                        <Button
                            title='openPicker'
                            onPress={() => {
                                openPicker({
                                    multiple: multiple,
                                    writeTempFile: writeTempFile,
                                    includeBase64: includeBase64,
                                    includeExif: includeExif,
                                    avoidEmptySpaceAroundImage: avoidEmptySpace,
                                    freeStyleCropEnabled: freeStyleCropEnabled,
                                    forceJpg: forceJpg,
                                    showsSelectedCount: showsSelectedCount,
                                    mediaType: selectedButton,
                                    minFiles: 1,
                                    maxFiles: maxFiles,
                                    compressImageQuality: imageQuality,
                                }).then(image => {
                                    console.log(TAG + ' openPicker result ' + JSON.stringify(image))
                                });
                            }}
                        />
                    </View>

                    <View style={styles.TextInputBox}>

                        <Text style={styles.inputLable}>cropping:</Text>
                        <Button
                            title={`${croppingCamera}`}
                            onPress={() => croppingCamera ? setCroppingCamera(false) : setCroppingCamera(true)}
                        />

                        <Text style={styles.inputLable}>writeTempFile:</Text>
                        <Button
                            title={`${writeTempFileCamera}`}
                            onPress={() => writeTempFileCamera ? setTempFileCamera(false) : setTempFileCamera(true)}
                        />

                    </View>

                    <View style={styles.TextInputBox}>

                        <Text style={styles.inputLable}>includeBase64:</Text>
                        <Button
                            title={`${includeBase64Camera}`}
                            onPress={() => includeBase64Camera ? setBase64Camera(false) : setBase64Camera(true)}
                        />

                        <Text style={styles.inputLable}>includeExif:</Text>
                        <Button
                            title={`${includeExifCamera}`}
                            onPress={() => includeExifCamera ? setIncludeExifCamera(false) : setIncludeExifCamera(true)}
                        />

                    </View>

                    <View style={styles.TextInputBox}>

                        <Text style={styles.inputLable}>avoidEmptySpaceAroundImage :</Text>
                        <Button
                            title={`${avoidEmptySpaceCamera}`}
                            onPress={() => avoidEmptySpaceCamera ? setAvoidEmptySpaceCamera(false) : setAvoidEmptySpaceCamera(true)}
                        />

                    </View>

                    <View style={styles.TextInputBox}>

                        <Text style={styles.inputLable}>freeStyleCropEnabled :</Text>
                        <Button
                            title={`${freeStyleCropEnabledCamera}`}
                            onPress={() => freeStyleCropEnabledCamera ? setFreeStyleCropEnabledCamera(false) : setFreeStyleCropEnabledCamera(true)}
                        />

                    </View>

                    <View style={styles.TextInputBox}>

                        <Text style={styles.inputLable}>useFrontCamera:</Text>
                        <Button
                            title={`${useFrontCamera}`}
                            onPress={() => useFrontCamera ? setUseFrontCamera(false) : setUseFrontCamera(true)}
                        />

                        <Text style={styles.inputLable}>forceJpg:</Text>
                        <Button
                            title={`${forceJpgCamera}`}
                            onPress={() => forceJpgCamera ? setForceJpgCamera(false) : setForceJpgCamera(true)}
                        />
                    </View>

                    <View style={styles.TextInputBox}>
                        <Text style={styles.inputLable}>mediaType:</Text>
                        <Button
                            title='photo'
                            onPress={() => handleMediaType('photo')}
                            accessibilityState={{ selected: mediaTypeCamera === 'photo' }}
                        />
                        <Button
                            title='video'
                            onPress={() => handleMediaType('video')}
                            accessibilityState={{ selected: mediaTypeCamera === 'video' }}
                        />
                        <Button
                            title='any'
                            onPress={() => handleMediaType('any')}
                            accessibilityState={{ selected: mediaTypeCamera === 'any' }}
                        />
                    </View>
                    <View style={styles.TextInputBox}>
                        <Text style={{ color: 'red' }}>mediaType is {mediaTypeCamera}</Text>
                    </View>

                    <View style={styles.TextInputBox}>
                        <Text style={styles.inputLable}>compressImageQuality:</Text>
                        <TextInput
                            style={styles.numberInput}
                            onChangeText={setImageQualityCamera}
                            value={imageQualityCamera}
                        />
                        <Text style={styles.lableType}>(0.1 to 1)</Text>
                    </View>

                    <View style={styles.TextInputBox}>
                        <Text style={styles.textLable}>cropperToolbarTitle:</Text>
                    </View>

                    <View style={styles.TextInputBox}>

                        <TextInput
                            style={styles.textInput}
                            maxLength={5}
                            onChangeText={(value) => setCropperTitleCamera(value)}
                            value={cropperTitleCamera}
                        />
                    </View>

                    <View style={styles.TextInputBox}>
                        <Text style={styles.textLable}>cropperChooseText:</Text>
                    </View>

                    <View style={styles.TextInputBox}>

                        <TextInput
                            style={styles.textInput}
                            maxLength={5}
                            onChangeText={(value) => setChooseTextCamera(value)}
                            value={chooseTextCamera}
                        />
                    </View>

                    <View style={styles.TextInputBox}>
                        <Text style={styles.textLable}>cropperChooseColor:#FF0000</Text>
                    </View>

                    <View style={styles.TextInputBox}>

                        <TextInput
                            style={styles.textInput}
                            maxLength={7}
                            onChangeText={(value) => setChooseColorCamera(value)}
                            value={chooseColorCamera}
                        />
                    </View>

                    <View style={styles.TextInputBox}>
                        <Text style={styles.textLable}>cropperCancelText:</Text>
                    </View>

                    <View style={styles.TextInputBox}>

                        <TextInput
                            style={styles.textInput}
                            maxLength={5}
                            onChangeText={(value) => setCancelTextCamera(value)}
                            value={cancelTextCamera}
                        />
                    </View>

                    <View style={styles.TextInputBox}>
                        <Text style={styles.textLable}>cropperCancelColor: #FF0000</Text>
                    </View>

                    <View style={styles.TextInputBox}>

                        <TextInput
                            style={styles.textInput}
                            maxLength={7}
                            onChangeText={(value) => setCancelColorCamera(value)}
                            value={cancelColorCamera}
                        />
                    </View>

                    <View style={styles.TextInputBox}>

                        <Text style={styles.inputLable}>cropperRotateButtonsHidden:</Text>
                        <Button
                            title={`${cropperRotateCamera}`}
                            onPress={() => cropperRotateCamera ? setCropperRotateCamera(false) : setCropperRotateCamera(true)}
                        />
                    </View>

                    <View style={styles.TextInputBox}>

                        <Text style={styles.inputLable}>showCropGuidelines:</Text>
                        <Button
                            title={`${showCropGuidelinesCamera}`}
                            onPress={() => showCropGuidelinesCamera ? setShowCropGuidelinesCamera(false) : setShowCropGuidelinesCamera(true)}
                        />
                    </View>

                    <View style={styles.TextInputBox}>

                        <Text style={styles.inputLable}>showCropFrame:</Text>
                        <Button
                            title={`${showCropFrameCamera}`}
                            onPress={() => showCropFrameCamera ? setShowCropFrameCamera(false) : setShowCropFrameCamera(true)}
                        />
                    </View>

                    <View style={styles.buttonSty}>
                        <Button
                            title="openCamera"
                            onPress={() => {
                                ImagePicker.openCamera({
                                    cropping: croppingCamera,
                                    writeTempFile: writeTempFileCamera,
                                    includeBase64: includeBase64Camera,
                                    includeExif: includeExifCamera,
                                    avoidEmptySpaceAroundImage: avoidEmptySpaceCamera,
                                    freeStyleCropEnabled: freeStyleCropEnabledCamera,
                                    useFrontCamera: useFrontCamera,
                                    forceJpg: forceJpgCamera,
                                    mediaType: mediaTypeCamera,
                                    compressImageQuality: imageQualityCamera,
                                    cropperToolbarTitle: cropperTitleCamera,
                                    cropperChooseText: chooseTextCamera,
                                    cropperChooseColor: chooseColorCamera,
                                    cropperCancelText: cancelTextCamera,
                                    cropperCancelColor: cancelColorCamera,
                                    cropperRotateButtonsHidden: cropperRotateCamera,
                                    showCropGuidelines: showCropGuidelinesCamera,
                                    showCropFrame: showCropFrameCamera,
                                }).then(image => {
                                    console.log(TAG + ' openCamera result ' + JSON.stringify(image))
                                });
                            }}
                        />
                    </View>

                    <View style={styles.TextInputBox}>
                        <Text style={styles.textLable}>Please enter the address of the image that needs to be cropped:</Text>
                    </View>

                    <View style={styles.TextInputBox}>

                        <TextInput
                            style={styles.textInput}
                            onChangeText={(value) => setImagePath(value)}
                            value={imagePath}
                        />

                    </View>

                    <View style={styles.TextInputBox}>

                        <Text style={styles.inputLable}>writeTempFile:</Text>
                        <Button
                            title={`${writeTempFileCropper}`}
                            onPress={() => writeTempFileCropper ? setTempFileCropper(false) : setTempFileCropper(true)}
                        />

                        <Text style={styles.inputLable}>forceJpg:</Text>
                        <Button
                            title={`${forceJpgCropper}`}
                            onPress={() => forceJpgCropper ? setForceJpgCropper(false) : setForceJpgCropper(true)}
                        />
                    </View>

                    <View style={styles.TextInputBox}>

                        <Text style={styles.inputLable}>includeBase64:</Text>
                        <Button
                            title={`${includeBase64Cropper}`}
                            onPress={() => includeBase64Cropper ? setBase64Cropper(false) : setBase64Cropper(true)}
                        />

                        <Text style={styles.inputLable}>includeExif:</Text>
                        <Button
                            title={`${includeExifCropper}`}
                            onPress={() => includeExifCropper ? setIncludeExifCropper(false) : setIncludeExifCropper(true)}
                        />

                    </View>

                    <View style={styles.TextInputBox}>

                        <Text style={styles.inputLable}>avoidEmptySpaceAroundImage :</Text>
                        <Button
                            title={`${avoidEmptySpaceCropper}`}
                            onPress={() => avoidEmptySpaceCropper ? setAvoidEmptySpaceCropper(false) : setAvoidEmptySpaceCropper(true)}
                        />

                    </View>

                    <View style={styles.TextInputBox}>

                        <Text style={styles.inputLable}>freeStyleCropEnabled :</Text>
                        <Button
                            title={`${freeStyleCropEnabledCropper}`}
                            onPress={() => freeStyleCropEnabledCropper ? setFreeStyleCropEnabledCropper(false) : setFreeStyleCropEnabledCropper(true)}
                        />

                    </View>

                    <View style={styles.TextInputBox}>
                        <Text style={styles.inputLable}>compressImageQuality:</Text>
                        <TextInput
                            style={styles.numberInput}
                            onChangeText={setimageQualityCropper}
                            value={imageQualityCropper}
                        />
                        <Text style={styles.lableType}>(0.1 to 1)</Text>
                    </View>


                    <View style={styles.TextInputBox}>
                        <Text style={styles.textLable}>cropperToolbarTitle:</Text>
                    </View>

                    <View style={styles.TextInputBox}>

                        <TextInput
                            style={styles.textInput}
                            maxLength={5}
                            onChangeText={(value) => setCropperTitle(value)}
                            value={cropperTitle}
                        />
                    </View>

                    <View style={styles.TextInputBox}>
                        <Text style={styles.textLable}>cropperChooseText:</Text>
                    </View>

                    <View style={styles.TextInputBox}>

                        <TextInput
                            style={styles.textInput}
                            maxLength={5}
                            onChangeText={(value) => setChooseText(value)}
                            value={chooseText}
                        />
                    </View>

                    <View style={styles.TextInputBox}>
                        <Text style={styles.textLable}>cropperChooseColor:#FF0000</Text>
                    </View>

                    <View style={styles.TextInputBox}>

                        <TextInput
                            style={styles.textInput}
                            maxLength={7}
                            onChangeText={(value) => setChooseColor(value)}
                            value={chooseColor}
                        />
                    </View>

                    <View style={styles.TextInputBox}>
                        <Text style={styles.textLable}>cropperCancelText:</Text>
                    </View>

                    <View style={styles.TextInputBox}>

                        <TextInput
                            style={styles.textInput}
                            maxLength={5}
                            onChangeText={(value) => setCancelText(value)}
                            value={cancelText}
                        />
                    </View>

                    <View style={styles.TextInputBox}>
                        <Text style={styles.textLable}>cropperCancelColor:#FF0000</Text>
                    </View>

                    <View style={styles.TextInputBox}>

                        <TextInput
                            style={styles.textInput}
                            maxLength={7}
                            onChangeText={(value) => setCancelColor(value)}
                            value={cancelColor}
                        />
                    </View>

                    <View style={styles.TextInputBox}>

                        <Text style={styles.inputLable}>cropperRotateButtonsHidden:</Text>
                        <Button
                            title={`${cropperRotate}`}
                            onPress={() => cropperRotate ? setCropperRotate(false) : setCropperRotate(true)}
                        />
                    </View>

                    <View style={styles.TextInputBox}>

                        <Text style={styles.inputLable}>showCropGuidelines:</Text>
                        <Button
                            title={`${showCropGuidelines}`}
                            onPress={() => showCropGuidelines ? setShowCropGuidelines(false) : setShowCropGuidelines(true)}
                        />
                    </View>

                    <View style={styles.TextInputBox}>

                        <Text style={styles.inputLable}>showCropFrame:</Text>
                        <Button
                            title={`${showCropFrame}`}
                            onPress={() => showCropFrame ? setShowCropFrame(false) : setShowCropFrame(true)}
                        />
                    </View>



                    <View style={styles.buttonSty}>
                        <Button
                            title='openCropper'
                            onPress={() => {

                                ImagePicker.openCropper({
                                    path: imagePath,
                                    width: 300,
                                    height: 400,
                                    writeTempFile: writeTempFileCropper,
                                    includeBase64: includeBase64Cropper,
                                    includeExif: includeExifCropper,
                                    avoidEmptySpaceAroundImage: avoidEmptySpaceCropper,
                                    freeStyleCropEnabled: freeStyleCropEnabledCropper,
                                    compressImageQuality: imageQualityCropper,
                                    forceJpg: forceJpgCropper,
                                    cropperToolbarTitle: cropperTitle,
                                    cropperChooseText: chooseText,
                                    cropperChooseColor: chooseColor,
                                    cropperCancelText: cancelText,
                                    cropperCancelColor: cancelColor,
                                    cropperRotateButtonsHidden: cropperRotate,
                                    showCropGuidelines: showCropGuidelines,
                                    showCropFrame: showCropFrame,
                                }).then((image => {
                                    console.log(TAG + ' openCropper result ' + JSON.stringify(image))
                                }))
                            }}
                        />
                    </View>

                </View>
            </View>

                <Text style={styles.title}> Delete File</Text>

                <View style={styles.buttonBox}>
                    <View style={styles.buttonSty}>
                        <Button
                            title='clean'
                            onPress={() => {
                                ImagePicker.clean({}).then(image => {
                                    console.log(TAG + ' clean result ' + JSON.stringify(image))
                                });
                            }}
                        />
                    </View>

                    <View style={styles.TextInputBox}>
                        <Text style={styles.textLable}>Please enter the address of the image that needs to be cleared:</Text>
                    </View>

                    <View style={styles.TextInputBox}>

                        <TextInput
                            style={styles.textInput}
                            onChangeText={(value) => setClearImagePath(value)}
                            value={clearImagePath}
                        />
                    </View>

                    <View style={styles.buttonSty}>
                        <Button
                            title='cleanSingle'
                            onPress={() => {
                                console.log(TAG + " cleanSingle path " + clearImagePath)
                                ImagePicker.cleanSingle('/data/storage/el2/base/haps/entry/temp/rn_image_crop_picker_lib_temp_' + clearImagePath).then(image => {

                                })
                            }}
                        />
                    </View>

                    <View style={styles.emptyView}></View>

                </View>

        </ScrollView>
    );
}
const styles = StyleSheet.create({
    container: {
    },
    TextInputBox: {
        flexDirection: 'row',
        alignItems: 'center',
        margin: 10,
    },
    textLable: {
        width: '100%'
    },
    emptyView: {
        width: 50,
        height: 500
    },
    inputLable: {
        width: 'auto'
    },
    lableType: {
        width: '18%'
    },
    numberInput: {
        width: 50,
        height: 30,
        color: 'black',
        borderColor: 'gray',
        borderWidth: 1
    },
    textInput: {
        width: '50%',
        height: 36,
        color: 'black',
        borderColor: 'gray',
        bordeWidth: 1
    },
    switchType: {
        width: 60,
        height: 36
    },
    buttonBox: {
        marginTop: 20,
    },
    buttonSty: {
        marginTop: 0,
        marginRight: 60,
        marginBottom: 20,
        marginLeft: 60,
        textAlign: 'center'
    },
    title: {
        fontWeight: '500',
        fontSize: 20,
        marginTop: 10,
    }
});
export default ImageCropPickDemo;
```

## Use Codegen

If this repository has been adapted to `Codegen`, generate the bridge code of the third-party library by using the `Codegen`. For details, see [Codegen Usage Guide](/en/codegen.md).

## Link

Currently, HarmonyOS does not support AutoLink. Therefore, you need to manually configure the linking.

Open the `harmony` directory of the HarmonyOS project in DevEco Studio.

```
Adding the overrides Field to oh-package.json5 File in the Root Directory of the Project
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "./react_native_openharmony"
  }
}
```

### 1. Configuration Entry

**(1)Create ImageEditAbility.ets under entry/src/main/ets/entryability**

```
import UIAbility from '@ohos.app.ability.UIAbility'
import window from '@ohos.window'

const TAG = 'ImageEditAbility';

export default class ImageEditAbility extends UIAbility {

  onWindowStageCreate(windowStage: window.WindowStage) {
    this.setWindowOrientation(windowStage, window.Orientation.PORTRAIT)
    windowStage.loadContent('pages/ImageEdit', (err, data) => {
      if (err.code) {
        console.info(TAG,'Failed to load the content. Cause: %{public}s',
          JSON.stringify(err) ?? '')
        return;
      }
      console.info(TAG,'Succeeded in loading the content')
    });
    try {
      windowStage.getMainWindowSync().setWindowLayoutFullScreen(true, (err)=>{
        if (err.code) {
          console.error('Failed to enable the full-screen mode. Cause: ' + JSON.stringify(err));
          return;
        }
        console.info('Succeeded in enabling the full-screen mode.');
      })
    } catch (exception) {
      console.error('Failed to set the system bar to be invisible. Cause: ' + JSON.stringify(exception));
    }
  }

  setWindowOrientation(stage: window.WindowStage, orientation: window.Orientation): void {
    console.info(TAG,"into setWindowOrientation :")
    if (!stage || !orientation) {
      return;
    }
    stage.getMainWindow().then(windowInstance => {
      windowInstance.setPreferredOrientation(orientation);
    })
  }

  onBackground() {
    this.context.terminateSelf();
  }
}
```

**(2)Register ImageEditAbility in entry/src/main/module.json5.**

```
"abilities":[{
        "name": "ImageEditAbility",
        "srcEntry": "./ets/entryability/ImageEditAbility.ets",
        "description": "$string:EntryAbility_desc",
        "icon": "$media:icon",
        "startWindowIcon": "$media:startIcon",
        "startWindowBackground": "$color:start_window_background",
        "removeMissionAfterTerminate": true,

}
...
]

```

**(3)Create entry/src/main/ets/pages under ImageEdit.ets**

```
import { ImageEditInfo } from '@react-native-oh-tpl/react-native-image-crop-picker';

@Entry
@Component
struct ImageEdit {

 build() {
  Row(){
   Column(){
    ImageEditInfo();
   }
   .width('100%')
  }
  .height('100%')
 }
}
```

**(4)Add configuration in entry/src/main/resources/base/profile/main_pages.json**

```
{
 "src": [
  "pages/Index",
  "pages/ImageEdit"
 ]
}
```

### 2. Introducing Native Code

Currently, two methods are available:

Method 1 (recommended): Use the HAR file.

> [!TIP] The HAR file is stored in the `harmony` directory in the installation path of the third-party library.

Open `entry/oh-package.json5` file and add the following dependencies:

```
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-image-crop-picker": "file:../../node_modules/@react-native-oh-tpl/react-native-image-crop-picker/harmony/image_crop_picker.har"
  }
```

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```
cd entry
ohpm install
```

Method 2: Directly link to the source code.

> [!TIP] For details, see [Directly Linking Source Code](/en/link-source-code.md).

### 3. Introducing ImageCropPickerPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+ import { ImageCropPickerPackage } from '@react-native-oh-tpl/react-native-image-crop-picker/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new ImageCropPickerPackage(ctx),
  ];
}
```

### 4. Running

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```
cd entry
ohpm install
```

Then build and run the code.

## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-image-crop-picker Releases ](https://github.com/react-native-oh-library/react-native-image-crop-picker/releases)

## API

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name        | Description                                                  | Type     | Required | Platform    | HarmonyOS Support |
| ----------- | ------------------------------------------------------------ | -------- | -------- | ----------- | ----------------- |
| openPicker  | Call single image picker with cropping                       | function | no       | iOS/Android | yes               |
| clean       | Module is creating tmp images which are going to be cleaned up automatically somewhere in the future. If you want to force cleanup, you can use `clean` to clean all tmp files, or `cleanSingle(path)` to clean single tmp file. | function | no       | iOS/Android | yes               |
| openCropper | Crop image and rotate,                                       | function | no       | iOS/Android | yes               |
| cleanSingle | Delete a single cache file                                   | function | no       | iOS/Android | yes               |
| openCamera  | Select from camera                                           | function | no       | iOS/Android | yes               |

## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

**cropData**

| Name                                      | Type                             | Description                                               | Required | Platform | HarmonyOS Support |
| ----------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | -------- | -------- | -------- |
| cropping                                  | bool (default false)                                         | Enable or disable cropping                                   | no       | All      | yes      |
| width                                   | number                                                       | Width of result image when used with `cropping` option       | no       | All      | yes      |
| height                                    | number                                                       | Height of result image when used with `cropping` option      | no       | All      | yes      |
| multiple                                  | bool (default false)                                         | Enable or disable multiple image selection                   | no       | All      | yes      |
| writeTempFile (iOS only)               | bool (default true)                                          | When set to false, does not write temporary files for the selected images. This is useful to improve performance when you are retrieving file contents with the `includeBase64` option and don't need to read files from disk. | no       | iOS   | yes      |
| includeBase64                             | bool (default false)                                         | When set to true, the image file content will be available as a base64-encoded string in the `data` property. Hint: To use this string as an image source, use it like: `<Image source={{uri: `data:image.mime;base64,𝑖𝑚𝑎𝑔𝑒.𝑚𝑖𝑚𝑒;𝑏𝑎𝑠𝑒64,{image.data}`}} />` | no       | All      | yes      |
| includeExif                               | bool (default false)                                         | Include image exif data in the response                      | no       | All      | yes      |
| avoidEmptySpaceAroundImage (iOS only)  | bool (default true)                                          | When set to true, the image will always fill the mask space. | no       | iOS   | no       |
| cropperActiveWidgetColor (Android only) | string (default `"#424242"`)                                 | When cropping image, determines ActiveWidget color.          | no       | Android | no       |
| cropperStatusBarColor (Android only) | string (default `#424242`)                                   | When cropping image, determines the color of StatusBar.      | no       | Android | no       |
| cropperToolbarColor (Android only) | string (default `#424242`)                                   | When cropping image, determines the color of Toolbar.        | no       | Android | no       |
| cropperToolbarWidgetColor (Android only) | string (default `darker orange`)                             | When cropping image, determines the color of Toolbar text and buttons. | no       | Android | no       |
| freeStyleCropEnabled                      | bool (default false)                                         | Enables user to apply custom rectangle area for cropping     | no       | All      | yes      |
| cropperToolbarTitle                       | string (default `Edit Photo`)                                | When cropping image, determines the title of Toolbar.        | no       | All      | yes      |
| cropperCircleOverlay                      | bool (default false)                                         | Enable or disable circular cropping mask.                    | no       | All      | no      |
| disableCropperColorSetters (Android only) | bool (default false)                                         | When cropping image, disables the color setters for cropping library. | no       | Android | no       |
| minFiles (iOS only)                    | number (default 1)                                           | Min number of files to select when using `multiple` option   | no       | iOS   | no      |
| maxFiles (iOS only)                    | number (default 5)                                           | Max number of files to select when using `multiple` option   | no       | iOS   | yes      |
| waitAnimationEnd (iOS only)            | bool (default true)                                          | Promise will resolve/reject once ViewController `completion` block is called | no       | iOS   | no       |
| smartAlbums (iOS only)                 | array ([supported values](https://gitee.com/link?target=https%3A%2F%2Fgithub.com%2Fivpusic%2Freact-native-image-crop-picker%2Fblob%2Fmaster%2FREADME.md%23smart-album-types-ios)) (default ['UserLibrary', 'PhotoStream', 'Panoramas', 'Videos', 'Bursts']) | List of smart albums to choose from                          | no       | iOS   | no       |
| useFrontCamera                            | bool (default false)                                         | Whether to default to the front/'selfie' camera when opened. Please note that not all Android devices handle this parameter, see [issue #1058](https://gitee.com/link?target=https%3A%2F%2Fgithub.com%2Fivpusic%2Freact-native-image-crop-picker%2Fissues%2F1058) | no       | All      | yes      |
| compressVideoPreset (iOS only)         | string (default MediumQuality)                               | Choose which preset will be used for video compression       | no       | iOS   | no       |
| compressImageMaxWidth                     | number (default none)                                        | Compress image with maximum width                            | no       | All      | no      |
| compressImageMaxHeight                    | number (default none)                                        | Compress image with maximum height                           | no       | All      | no      |
| compressImageQuality                      | number (default 1 (Android)/0.8 (iOS))                       | Compress image with quality (from 0 to 1, where 1 is best quality). On iOS, values larger than 0.8 don't produce a noticeable quality increase in most images, while a value of 0.8 will reduce the file size by about half or less compared to a value of 1. | no       | All      | yes      |
| loadingLabelText (iOS only)            | string (default "Processing assets...")                      | Text displayed while photo is loading in picker              | no       | iOS   | no      |
| mediaType                                 | string (default any)                                         | Accepted mediaType for image selection, can be one of: 'photo', 'video', or 'any' | no       | All      | yes      |
| showsSelectedCount (iOS only)          | bool (default true)                                          | Whether to show the number of selected assets                | no       | iOS   | no      |
| sortOrder (iOS only)                   | string (default 'none', supported values: 'asc', 'desc', 'none') | Applies a sort order on the creation date on how media is displayed within the albums/detail photo views when opening the image picker | no       | iOS   | no       |
| forceJpg (iOS only)                    | bool (default false)                                         | Whether to convert photos to JPG. This will also convert any Live Photo into its JPG representation | no       | iOS   | yes      |
| showCropGuidelines (Android only) | bool (default true)                                          | Whether to show the 3x3 grid on top of the image during cropping | no       | Android | yes      |
| showCropFrame (Android only)      | bool (default true)                                          | Whether to show crop frame during cropping                   | no       | Android | yes      |
| hideBottomControls (Android only) | bool (default false)                                         | Whether to display bottom controls                           | no       | Android | no       |
| enableRotationGesture (Android only) | bool (default false)                                         | Whether to enable rotating the image by hand gesture         | no       | Android | yes      |
| cropperChooseText (iOS only)           | string (default choose)                                      | Choose button text                                           | no       | iOS   | yes      |
| cropperChooseColor (iOS only)          | string (default `#FFCC00`)                                   | HEX format color for the Choose button. [Default color is controlled by TOCropViewController](https://gitee.com/link?target=https%3A%2F%2Fgithub.com%2FTimOliver%2FTOCropViewController%2Fblob%2Fa942414508012b13102f776eb65dac655f31cabb%2FObjective-C%2FTOCropViewController%2FViews%2FTOCropToolbar.m%23L444). | no       | iOS   | yes      |
| cropperCancelText (iOS only)           | string (default Cancel)                                      | Cancel button text                                           | no       | iOS   | yes      |
| cropperCancelColor (iOS only)          | string (default tint `iOS` color )                           | HEX format color for the Cancel button. Default value is the default tint iOS color [controlled by TOCropViewController](https://gitee.com/link?target=https%3A%2F%2Fgithub.com%2FTimOliver%2FTOCropViewController%2Fblob%2Fa942414508012b13102f776eb65dac655f31cabb%2FObjective-C%2FTOCropViewController%2FViews%2FTOCropToolbar.m%23L433) | no       | iOS   | yes      |
| cropperRotateButtonsHidden (iOS only)  | bool (default false)                                         | Enable or disable cropper rotate buttons                     | no       | iOS   | yes      |

## Known Issues

- [ ] Images in react-native-image-crop-picker will always fill the mask space [#4](https://github.com/react-native-oh-library/react-native-image-crop-picker/issues/4)
- [ ] Change the color of ActiveWidget in Android Demo [#5](https://github.com/react-native-oh-library/react-native-image-crop-picker/issues/5)
- [ ] Change the status bar color in Android Demo [#6](https://github.com/react-native-oh-library/react-native-image-crop-picker/issues/6)
- [ ] Change the toolbar color in Android Demo [#7](https://github.com/react-native-oh-library/react-native-image-crop-picker/issues/7)
- [ ] Disable the color picker in the cropping library when cropping images [#8](https://github.com/react-native-oh-library/react-native-image-crop-picker/issues/8)
- [ ] Determine the colors of toolbar text and buttons when cropping images [#9](https://github.com/react-native-oh-library/react-native-image-crop-picker/issues/9)
- [ ] Call the ViewController "completion" block, where the Promise will be resolved/rejected; HarmonyOS is not supported [#10](https://github.com/react-native-oh-library/react-native-image-crop-picker/issues/10)
- [ ] iOS support for smart album lists  [#11](https://github.com/react-native-oh-library/react-native-image-crop-picker/issues/11)
- [ ] Presets for video compression on iOS [#12](https://github.com/react-native-oh-library/react-native-image-crop-picker/issues/12)
- [ ] Sorting of smart albums on iOS  [#13](https://github.com/react-native-oh-library/react-native-image-crop-picker/issues/13)
- [ ] Set whether to show bottom controls in Android Demo [#14](https://github.com/react-native-oh-library/react-native-image-crop-picker/issues/14)
- [ ] Cannot set a minimum number of files when using the multiple option  [#39](https://github.com/react-native-oh-library/react-native-image-crop-picker/issues/39)
- [ ] Cannot set whether to display the number of selected assets when using the multiple option [#40](https://github.com/react-native-oh-library/react-native-image-crop-picker/issues/40)
- [ ] photoAccessHelper lacks a loading transition animation effect after selection [#45](https://github.com/react-native-oh-library/react-native-image-crop-picker/issues/45)
- [ ] @ohos.multimedia.image cannot perform circular cropping [#46](https://github.com/react-native-oh-library/react-native-image-crop-picker/issues/46)
- [ ] The PackingOption in @ohos.multimedia.image cannot set width and height properties [#47](https://github.com/react-native-oh-library/react-native-image-crop-picker/issues/47)

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/ivpusic/react-native-image-crop-picker/blob/master/LICENSE).
