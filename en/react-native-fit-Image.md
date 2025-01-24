> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-fit-image</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/huiseoul/react-native-fit-image/blob/master">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|web|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/huiseoul/react-native-fit-image/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/lisense-BEER-WARE?color=%238bb903
" alt="License" />
    </a>
</p>



> [!TIP] [GitHub address](https://github.com/huiseoul/react-native-fit-image)

## Installation and Usage

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-fit-image@1.5.5
```

#### **yarn**

```bash
yarn add react-native-fit-image@1.5.5
```

<!-- tabs:end -->

The following code shows the basic use scenarios of the repository:

```tsx
import React,{useState,useEffect} from 'react'
import {View,StyleSheet,Text,ScrollView,SafeAreaView,Image,Button} from "react-native"
import FitImage from "react-native-fit-image"
var styles = StyleSheet.create({
    fitImage:{
        borderRadius:20,
        borderColor:'red',
        borderWidth:1
    },
    fitImageWithSize:{
        height:200,
        width:'100%'
    }
});
const FitImageDemo=()=>{
    // Test onLoad.
    const [onLoadDatea,setOnLoad] = useState('Initial onLoad not executed')
    // Test onError.
    const [onErrorDatea,setOnError] = useState('Initial onError not executed')
    // Test onLoadStart.
    const [onLoadStartDatea,setOnLoadStart] = useState('onLoadStart not executed')
    // Test onLayOut.
    const [onLayOutData,setOnLayout] = useState('OnLayout not executed')
    // Refresh.
    const [refLoadData,setRefLoadBtn] = useState(true)
    // Obtain the local image size.
    const [imgSizeNum,getImageSizeNum] = useState({width:0,height:0})
    const img1 = require('./assets/expo.png')
    const getImageSize = ()=>{
        let res = Image.resolveAssetSource(img1)
        getImageSizeNum({width:res.width,height:res.height})
    }
    // Obtain the network image size.
    const imgHttp={uri:"https://octodex.github.com/images/stormtroopocat.jpg"}
    const [imgHttpSize,getHttpSizeNum] = useState({width:0,height:0})
    // Refresh.
    const [reshUiData,setReshUi] = useState(0)
    useEffect(() => {;
        getReloadFres()
      }, []);
      const getReloadFres =()=>{
         // HTTP remote file.
         Image.getSize(imgHttp.uri, (width,height) => {
            getHttpSizeNum({ width,height });
          },
         (failure) => { console.log('failure', failure)});
      }
    // Refresh.
    const reLoadFun = () =>{
        setRefLoadBtn(false)
        setReshUi(reshUiData+1)
        getImageSizeNum({width:0,height:0})
        getHttpSizeNum({width:0,height:0})
        setRefLoadBtn(true)
        getReloadFres()
    }
    return (
        <SafeAreaView>
            <ScrollView>
                {/* Refresh for pressure test */}
                <Button onPress={()=>{reLoadFun()}} title='Refresh'></Button>
                {refLoadData&&(
                    <View style={{width:'100%',height:'100%'}}>
                    <Text>Refreshed {reshUiData} times</Text>
                     <View>
                         <Text>Test onLoad</Text>
                         <Text>{onLoadDatea}</Text>
                         <FitImage onLoad={()=>{console.log('onLoad executed'); setOnLoad('onLoad executed')}}
                             style={styles.fitImageWithSize} source={require('./assets/expo.png')} />                        
                     </View>
                     <View>
                         <Text>Test the Base64-encoded image.</Text>
                         <FitImage
                              source={{
                                 uri: 'data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADMAAAAzCAYAAAA6oTAqAAAAEXRFWHRTb2Z0d2FyZQBwbmdjcnVzaEB1SfMAAABQSURBVGje7dSxCQBACARB+2/ab8BEeQNhFi6WSYzYLYudDQYGBgYGBgYGBgYGBgYGBgZmcvDqYGBgmhivGQYGBgYGBgYGBgYGBgYGBgbmQw+P/eMrC5UTVAAAAABJRU5ErkJggg==',
                               }}
                               style={{...styles.fitImageWithSize}}
                             />
                     </View>
                     <View>
                         <Text>Local image set with originalWidth and originalHeight but without width and height of style.</Text>
                         <FitImage
                             source={require('./assets/expo.png')}
                             originalWidth={400}
                             originalHeight={400}
                             />
                     </View>
                     <View>
                         <Text>Local image set without originalWidth, originalHeight, and width and height of style.</Text>
                         <FitImage
                             source={require('./assets/expo.png')}
                             />
                     </View>
                     <View>
                         <Text>Local image set with width and height of style but without originalWidth and originalHeight.</Text>
                         <FitImage
                             source={require('./assets/expo.png')}
                             style={{...styles.fitImageWithSize}}
                             />
                     </View>
                     <View>
                         <Text>Network image set with width and height of style but without originalWidth and originalHeight.</Text>
                         <FitImage
                             source={{uri:"https://octodex.github.com/images/stormtroopocat.jpg"}}
                             style={{...styles.fitImageWithSize}}
                             />
                     </View>
                     <View>
                         <Text>Network image set with originalWidth and originalHeight but without width and height of style.</Text>
                         <FitImage
                             source={{uri:"https://octodex.github.com/images/stormtroopocat.jpg"}}
                             originalWidth={400}
                             originalHeight={400}
                             />
                     </View>
                     <View>
                         <Text>Local image set with originalWidth, originalHeight, and width and height of style.</Text>
                         <FitImage
                             source={require('./assets/expo.png')}
                             originalWidth={400}
                             originalHeight={400}
                             style={{...styles.fitImageWithSize}}
                             />
                     </View>
                     <View>
                         <View>
                             <Text>indicator (value: true); indicatorColor (value: specified color); indicatorSize (value: large, small, or number)</Text>
                             <Text>value: large</Text>
                             <FitImage indicator={true}  indicatorColor='red' indicatorSize='large' 
                                 style={{...styles.fitImageWithSize}} source={require('./assets/expo.png')} />                  
                         </View>
                         <View>
                             <Text>indicator (value: true); indicatorColor (value: specified color); indicatorSize (value: large, small, or number)</Text>
                             <Text>value: small</Text>
                             <FitImage indicator={true}  indicatorColor='red' indicatorSize='small' 
                                 style={{...styles.fitImageWithSize}} source={require('./assets/expo.png')} />                   
                         </View>
                         <View>
                             <Text>indicator (value: true); indicatorColor (value: specified color); indicatorSize (value: large, small, or number)</Text>
                             <Text>number: A larger value indicates a larger indicator.</Text>
                             <FitImage indicator={true}  indicatorColor='red' indicatorSize={100} 
                                 style={{...styles.fitImageWithSize}} source={require('./assets/expo.png')} />                   
                         </View>
                         <View>
                             <Text>indicator (value: false)</Text>
                             <Text>number: A larger value indicates a larger indicator.</Text>
                             <FitImage indicator={false}   style={{...styles.fitImageWithSize}} 
                                 source={require('./assets/expo.png')} />                             
                         </View>
                     </View>
                     <View>
                         <Text>Verify a network image.</Text>
                         <FitImage  style={styles.fitImageWithSize}  
                             source={{uri:"https://octodex.github.com/images/stormtroopocat.jpg"}} />                        
                     </View>
                     <View>
                         <Text>Obtain the width and height of a local image.</Text>
                         <FitImage  style={styles.fitImageWithSize} source={require('./assets/expo.png')} />                        
                         <Text>Width: {imgSizeNum.width}; Height: {imgSizeNum.height}</Text>
                         <Button onPress={()=>{getImageSize()}} title='Call the Image Width and Height'></Button>
                     </View>
                     <View>
                         <Text>Verify the width and height of a network image.</Text>
                         <Text>Width: {imgHttpSize.width}; Height: {imgHttpSize.height}</Text>
                         <FitImage  style={{...styles.fitImageWithSize,...styles.fitImage}} 
                             source={{uri:"https://octodex.github.com/images/stormtroopocat.jpg"}} />                         
                     </View>
                     <View>
                         <Text>Verify rounded corners of the image.</Text>
                         <FitImage  style={{...styles.fitImageWithSize,...styles.fitImage}} 
                             source={require('./assets/expo.png')} />                        
                     </View>
                     <View>
                         <Text>Test resizeMode. The value is cover.</Text>
                         <FitImage resizeMode='cover' style={{...styles.fitImageWithSize}} 
                             source={require('./assets/expo.png')} />                        
                     </View>
                     <View>
                         <Text>Test resizeMode. The value is contain.</Text>
                         <FitImage resizeMode='contain' style={{...styles.fitImageWithSize}}
                             source={require('./assets/expo.png')} />                        
                     </View>
                     <View>
                         <Text>Test resizeMode. The value is stretch.</Text>
                         <FitImage resizeMode='stretch' style={{...styles.fitImageWithSize}} 
                             source={require('./assets/expo.png')} />                        
                     </View>
                     <View>
                         <Text>Test resizeMode. The value is repeat.</Text>
                         <FitImage resizeMode='repeat' style={{...styles.fitImageWithSize}} 
                             source={require('./assets/expo.png')} />                        
                     </View>
                     <View>
                         <Text>Test resizeMode. The value is center.</Text>
                         <FitImage resizeMode='center' style={{...styles.fitImageWithSize}} 
                             source={require('./assets/expo.png')} />                        
                     </View>
                    
                     <View>
                         <Text>Test onError.</Text>
                         <Text>{onErrorDatea}</Text>
                         <FitImage onError={()=>{console.log('onError executed'); setOnError('onError executed')}}
                             style={styles.fitImageWithSize} source={{uri:'https://ok.gitHub.io123.png'}} />    
                     </View>
                     <View>
                         <Text>Test onLoadStart.</Text>
                         <Text>{onLoadStartDatea}</Text>
                         <FitImage onLoadStart={()=>{console.log('onLoadStart executed'); setOnLoadStart('onLoadStart executed')}}
                             style={{...styles.fitImageWithSize,borderRadius:20}} source={require('./assets/expo.png')} />     
                     </View>
                     <View>
                         <Text>Test onLayOut.</Text>
                         <Text>{onLayOutData}</Text>
                         <FitImage onLoadStart={()=>{console.log('onLayout executed');setOnLayout('onLayout executed')}}
                             style={{...styles.fitImageWithSize,borderRadius:20}} source={require('./assets/expo.png')} />     
                     </View>
                     <View>
                         <Text>Test blurRadius. A larger value indicates a stronger blur.</Text>
                         <FitImage
                             source={require('./assets/expo.png')}
                             blurRadius={20}
                             style={{...styles.fitImage,...styles.fitImageWithSize}}
                             />
                     </View>
                 </View>
                )}
               {!refLoadData&&(
                <View style={{width:'100%',height:'100%'}}>
                    <Text>
                        Loading...
                    </Text>
                </View>
               )}
            </ScrollView>
        </SafeAreaView>
    )
}
export default FitImageDemo;
```

## Constraints

### Compatibility

This document is verified based on the following versions

1. RNOH: 0.72.20; SDK: HarmonyOS NEXT Developer Preview2; IDE: DevEco Studio 5.0.3.200; ROM: 3.0.0.21;
2. RNOH: 0.72.33; SDK: OpenHarmony 5.0.0.71 (API Version 12 Release); IDE: DevEco Studio 5.0.3.900; ROM: NEXT.0.0.71;

## Properties

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name               | Description                                                  | Type          | Required | Platform                                      | HarmonyOS Support | Remark                                                       |
| ------------------ | ------------------------------------------------------------ | ------------- | -------- | --------------------------------------------- | ----------------- | ------------------------------------------------------------ |
| `style`            | Width, height, and border style of the image.                | object        | yes      | Android and iOS                               | yes               | If **orginalWidth** and **orginalHeight** are not set, the **width** and **height** must be set in **style** so that the image can be loaded. |
| `source`           | Image source:<br>For local image, source={require('./assets/expo.png')}.<br>For network image, source={{uri:"xxx"}}. | string        | yes      | Android and iOS                               | yes               |                                                              |
| `width`            | Property of an image style.                                  | number        | yes      | Android and iOS                               | yes               |                                                              |
| `height`           | Property of an image style.                                  | number        | yes      | Android and iOS                               | yes               |                                                              |
| `borderRadius`     | Image style (rounded corner).                                | number        | no       | Not supported on Android, iOS, and HarmonyOS. | no                | This property does not take effect on HarmonyOS, Android, and iOS: [issues](https://github.com/huiseoul/react-native-fit-image/issues/111) |
| `indicator`        | Indicator. The value can be **true** (default) or **false**. | boolean       | no       | Android and iOS                               | yes               |                                                              |
| `indicatorColor`   | Indicator color.                                             | string        | no       | Android and iOS                               | yes               |                                                              |
| `indicatorSize`    | Indicator size. The value can be `large`, `small`, or number (for example, indicatorSize={20}). | string/number | no       | Android and iOS                               | yes               |                                                              |
| resizeMode         | Image layout. The options are as follows:<br>`cover`: scales the image with the aspect ratio retained until the width and height are greater than or equal to the container size. If the container has padding, the padding is subtracted accordingly. **Note**: In this way, the image completely covers or even exceeds the container, and no space is left in the container.<br> `contain`: scales the image with the aspect ratio retained until the width and height are less than or equal to the container size. If the container has padding, the padding is subtracted accordingly. **Note**: In this way, the image is completely wrapped in the container, and there may be blank space in the container.<br> `stretch`: stretches the image without retaining the aspect ratio until the width and height fit the container size.<br> `repeat`: tiles the image repeatedly until the image covers the whole container. The original size of the image is retained. However, when the image size exceeds the container size, the image is scaled to be wrapped by the container while the aspect ratio is retained.<br> `center`: places the image at the center of the container without stretching it. | string        | no       | Android and iOS                               | yes               |                                                              |
| blurRadius         | Image blur filter. A larger value indicates a stronger blur. | number        | no       | Android and iOS                               | yes               |                                                              |
| onLoad             | Callback invoked when the image is successfully loaded.      | function      | no       | Android and iOS                               | yes               |                                                              |
| resolveAssetSource | Function used to obtain the width and height of a local image.<br>Example: const img1 = require('./assets/expo.png')<br>let  res = Image.resolveAssetSource(img1) | function      | no       | Android and iOS                               | yes               |                                                              |
| getSize            | Function used to obtain the network image size.<br>Example: Image.getSize(uri,(width,height)=>{},(fail)=>{}) | function      | no       | Android and iOS                               | yes               |                                                              |
| onError            | Callback invoked when the image resource fails to be obtained. | function      | no       | Not supported on Android, iOS, and HarmonyOS. | no                | As described in the original library, some properties are not working: [issues](https://github.com/huiseoul/react-native-fit-image/issues/76). |
| onLoadStart        | Callback invoked when resources are just loaded.             | function      | no       | Not supported on Android, iOS, and HarmonyOS. | no                | As described in the original library, some properties are not working: [issues](https://github.com/huiseoul/react-native-fit-image/issues/76). |
| onLayout           | Callback invoked when the resource size is changed or the resource is loaded. | function      | no       | Not supported on Android, iOS, and HarmonyOS. | no                | As described in the original library, some properties are not working: [issues](https://github.com/huiseoul/react-native-fit-image/issues/76). |
| orginalWidth       | Original image width.                                        | number        | no       | Android and iOS                               | yes               |                                                              |
| orginalHeight      | Original image height.                                       | number        | no       | Android and iOS                               | yes               |                                                              |

## Known Issues

- [ ] The `onError`, `onLoadStart`, and `onLayout` callbacks are not supported on Android, iOS, and HarmonyOS: [issues](https://github.com/huiseoul/react-native-fit-image/issues/76).
- [ ] The `borderRadius` property is not supported on HarmonyOS, iOS, and Android: [issues](https://github.com/huiseoul/react-native-fit-image/issues/111).

## Others

## License

This project is licensed under [BEER-WARE License](https://github.com/huiseoul/react-native-fit-image/blob/master/LICENSE).