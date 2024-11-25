> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-material-ui</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/xotahal/react-native-material-ui">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20windows%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
        <a href="https://github.com/xotahal/react-native-material-ui/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>


> [!TIP] [Github 地址](https://github.com/xotahal/react-native-material-ui)

## 安装与使用

请到三方库的 Releases
发布地址查看配套的版本信息：[@react-native-oh-tpl/react-material-ui Releases](https://gitee.com/link?target=https%3A%2F%2Fgithub.com%2Freact-native-oh-library%2Freact-native-material-ui%2Freleases) 。对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-material-ui
```

#### **yarn**

```bash
yarn add react-native-material-ui
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js

import { ActionButton} from 'react-native-material-ui';
import { View, StyleSheet,ScrollView,Text } from 'react-native'
import { useState } from 'react';

const ActionButtonDemo = () => {
  const [actionText,setActionText] = useState('')
  return (
      <>
        <ScrollView style={styles.scrollView}>
              <View style={styles.view}>
                <ActionButton
                  actions={[
                    { icon: 'email', label: 'Email',name:'email'},
                    { icon: 'phone', label: 'Phone',name:'Phone' },
                    { icon: 'sms', label: 'Text',name:'Text' },
                    { icon: 'chat', label: 'chat',name:'chat' },
                ]}
                  icon='email'
                  transition="speedDial"
                />
              </View>

              <View style={styles.view}>
                <ActionButton
                  onPress={()=>setActionText("onPress actionText")}
                  actions={[
                    { icon: 'email', label: 'Email',name:'email'},
                    { icon: 'phone', label: 'Phone',name:'Phone' },
                    { icon: 'sms', label: 'Text',name:'Text' },
                    { icon: 'chat', label: 'chat',name:'chat' },
                ]}
                  icon='email'
                  transition="speedDial"
                />
                <Text>{actionText}</Text>
              </View>

              <View style={styles.view}>
                <ActionButton
                  actions={[{ icon: 'email', label: 'email', name: 'email' },
                  { icon: 'phone', label: 'Phone', name: 'phone' },
                  { icon: 'sms', label: 'text', name: 'text' },
                  { icon: 'chat', label: 'chat', name: 'chat' }]}
                  icon="share"
                  transition="toolbar"
                />
              </View>

              <View style={styles.view}>
                <ActionButton
                  style={{container:{backgroundColor:'blue'},icon:{color:'red'},positionContainer:{top:2,bottom:2}}}
                  actions={[
                    { icon: 'email', label: 'Email',name:'email'},
                    { icon: 'phone', label: 'Phone',name:'Phone' },
                    { icon: 'sms', label: 'Text',name:'Text' },
                    { icon: 'chat', label: 'chat',name:'chat' },
                ]}
                  icon='email'
                  transition="speedDial"
                />
                <Text>{actionText}</Text>
              </View>

              <View style={styles.view}>
                <ActionButton
                style={{toolbarContainer:{backgroundColor:'blue'}}}
                  actions={[{ icon: 'email', label: 'email', name: 'email' },
                  { icon: 'phone', label: 'Phone', name: 'phone' },
                  { icon: 'sms', label: 'text', name: 'text' },
                  { icon: 'chat', label: 'chat', name: 'chat' }]}
                  icon="share"
                  transition="toolbar"
                />
              </View>
          </ScrollView>  
          </>
  )
}

const styles = StyleSheet.create({
  view: {
    width: '100%',
    height: 350,
  },
  scrollView:{
    marginBottom:70
  }
});


export default ActionButtonDemo
```
### 在 ArkTs 侧引入和注册字体文件

步骤一： 复制字体文件到 `entry/src/main/resources/rawfile/assets/assets/fonts` 目录下(如使用了外部字体文件，需要将*.ttf 文件复制过来)

步骤二： 打开 `entry/src/main/ets/pages/Index.ets`，添加以下代码

```
 const fonts: Record<string, Resource> = {
   "Pacifico-Regular": $rawfile("assets/assets/fonts/Pacifico-Regular.ttf"),
   "StintUltraCondensed-Regular": $rawfile("assets/assets/fonts/StintUltraCondensed-Regular.ttf"),
   'Entypo': $rawfile('assets/assets/fonts/Entypo.ttf'),
   'EvilIcons': $rawfile('assets/assets/fonts/EvilIcons.ttf'),
   'Feather': $rawfile('assets/assets/fonts/Feather.ttf'),
   'FontAwesome': $rawfile('assets/assets/fonts/FontAwesome.ttf'),
   'FontAwesome5Brands-Regular': $rawfile('assets/assets/fonts/FontAwesome5_Brands.ttf'),
   'FontAwesome5Free-Regular': $rawfile('assets/assets/fonts/FontAwesome5_Regular.ttf'),
   'FontAwesome5Free-Solid': $rawfile('assets/assets/fonts/FontAwesome5_Solid.ttf'),
   'FontAwesome6Brands-Regular': $rawfile('assets/assets/fonts/FontAwesome6_Brands.ttf'),
   'FontAwesome6Free-Regular': $rawfile('assets/assets/fonts/FontAwesome6_Regular.ttf'),
   'FontAwesome6Free-Solid': $rawfile('assets/assets/fonts/FontAwesome6_Solid.ttf'),
   'fontcustom': $rawfile('assets/assets/fonts/Foundation.ttf'),
   'Ionicons': $rawfile('assets/assets/fonts/Ionicons.ttf'),
   'Material Design Icons': $rawfile('assets/assets/fonts/MaterialCommunityIcons.ttf'),
   'Material Icons': $rawfile('assets/assets/fonts/MaterialIcons.ttf'),
   'Octicons': $rawfile('assets/assets/fonts/Octicons.ttf'),
   'simple-line-icons': $rawfile('assets/assets/fonts/SimpleLineIcons.ttf'),
   'zocial': $rawfile('assets/assets/fonts/Zocial.ttf'),
 }

@Entry
@Component
struct Index {
  //...
  build() {
    Column(){
      //...

      //注册字体文件
      RNApp({
        rnInstanceConfig: {
          //...
          fontResourceByFontFamily: fonts
        },
        //...
      })

    }
    //...
  }
}
```

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-material-ui Releases](https://github.com/react-native-oh-library/react-native-material-ui/releases)

## 组件

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

### ActionButton

| Name       |                                                                                 Description                                                                                 |                   Type                    | Required |               Platform               | HarmonyOS Support |
|:-----------|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|:-----------------------------------------:|:--------:|:------------------------------------:|:-----------------:|
| actions    | Array of names of icons (or elements) that will be shown after the main button is pressed 。 Remember, you should specify key for each element, if you use array of elements |                 string[]                  |    no    |             iOS/Android              |       yes        |
| onPress    |                                                           Called when button is pressed. Text is passed as param                                                            |              PropTypes.func               |    no    |             iOS/Android              |        yes        |
| icon       |                                                                   If specified it'll be shown before text                                                                   |   PropTypes.element<br>PropTypes.string   |    no    |             iOS/Android              |        yes        |
| transition |               Leave it empty if you don't want any transition after press. Otherwise, it will be transformed . to another view - depends on transition value.               | PropTypes.oneOf(['toolbar', 'speedDial']) |    no    |             iOS/Android              |        yes        |
| style      |                                                                  ou can override any style for this button                                                                  |       **ActionButton style props**        |    no    |             iOS/Android              |        yes        |

**ActionButton style props**

| Name              | Description             | Type                 | Required | Platform    | HarmonyOS Support |
|-------------------|-------------------------|----------------------|----------|-------------|-------------------|
| container         | container style         | View.propTypes.style | no       | iOS/Android | yes               |
| icon              | icon style              | Text.propTypes.style | no       | iOS/Android | yes               |
| positionContainer | positionContainer style | View.propTypes.style | no       | iOS/Android | yes               |
| toolbarContainer  | Toolbar styles          | View.propTypes.style | no       | iOS/Android | yes               |

### Avatar

| Name      |                                    Description                                    |                               Type                               | Required |  Platform   | HarmonyOS Support |
|:----------|:---------------------------------------------------------------------------------:|:----------------------------------------------------------------:|:--------:|:-----------:|:-----------------:|
| image     |                  If passed in, this component will render image.                  |       PropTypes.shape({ type: PropTypes.oneOf([Image]) }),       |    no    | iOS/Android |        yes        |
| icon      |       If passed in, this component will render icon element inside avatar.        |                         PropTypes.string                         |    no    | iOS/Android |        yes        |
| iconColor |         If passed in, this component will render an icon with this color.         |                         PropTypes.string                         |    no    | iOS/Android |        yes        |
| iconSize  |         If passed in, this component will render an icon with this size.          |                         PropTypes.number                         |    no    | iOS/Android |        yes        |
| text      |       If passed in, this component will render text element inside avatar.        |                         PropTypes.string                         |    no    | iOS/Android |        yes        |
| size      | It's just sugar for: style: { width: size, height: size, borderRadius: size / 2 } |                         PropTypes.number                         |    no    | iOS/Android |        yes        |
| style     |                              Inline style of avatar                               | container: View.propTypes.style<br>content: Text.propTypes.style |    no    | iOS/Android |        yes        |

### Badge

| Name     |                                        Description                                         |                     Type                      | Required |  Platform   | HarmonyOS Support |
|:---------|:------------------------------------------------------------------------------------------:|:---------------------------------------------:|:--------:|:-----------:|:-----------------:|
| children |                      The badge will be added relatively to this node                       |                PropTypes.node                 |    no    | iOS/Android |        yes        |
| text     |                       This is the content rendered within the badge                        |               PropTypes.string                |    no    | iOS/Android |        yes        |
| icon     |           When the icon is set, the content will be <Icon name={icon} /> element           | PropTypes.string,<br>{name:string,color,size} |    no    | iOS/Android |        yes        |
| size     | Just sugar for style={{ container: { width: size, height: size, borderRadius: size / 2 }}} |               PropTypes.number                |    no    | iOS/Android |        yes        |
| stroke   |                                      Stroke on Badge                                       |               PropTypes.number                |    no    | iOS/Android |        yes        |

### Icon

| Name  |      Description      |   Type    | Required |  Platform   | HarmonyOS Support |
|:------|:---------------------:|:---------:|:--------:|:-----------:|:-----------------:|
| name  |       Icon name       |  string   |   yes    | iOS/Android |        yes        |
| style | The style of the icon | ViewStyle |    no    |    iOS/Android    |        yes        |
| size  | The size of the icon  |  number   |    no    | iOS/Android |        yes        |
| color | The color of the icon |  string   |    no    | iOS/Android |        yes        |

### IconToggle

| Name       |                       Description                        |            Type             | Required |  Platform   | HarmonyOS Support |
|:-----------|:--------------------------------------------------------:|:---------------------------:|:--------:|:-----------:|:-----------------:|
| color      |                  The color of the icon                   |      PropTypes.string       |    no    | iOS/Android |        yes        |
| maxOpacity |               Max opacity of ripple effect               |      PropTypes.number       |    no    | iOS/Android |        yes        |
| percent    |                  Size of underlayColor                   |      PropTypes.number       |    no    | iOS/Android |        yes        |
| disabled   |        If true, the interaction will be forbidden        |       PropTypes.bool        |    no    | iOS/Android |        yes        |
| size       |  Size of icon (default is 24 - see spacing in palette)   |      PropTypes.number       |    no    | iOS/Android |        yes        |
| name       |                   Name of icon to show                   | PropTypes.string.isRequired |   yes    | iOS/Android |        yes        |
| children   | It'll be used instead of icon (see props name) if exists |      PropTypes.element      |    no    | iOS/Android |        yes        |

### BottomNavigation

| Name     |                   Description                   |              Type               | Required |  Platform   | HarmonyOS Support |
|:---------|:-----------------------------------------------:|:-------------------------------:|:--------:|:-----------:|:-----------------:|
| active   |         The key of selected/active tab          |        PropTypes.string         |    no    | iOS/Android |        yes        |
| children |          BottomNavigation.Action nodes          |    PropTypes.node.isRequired    |   yes    | iOS/Android |        yes        |
| hidden   | Whether or not the BottomNavigation should show |         PropTypes.bool          |    no    | iOS/Android |        No         |
| style    |        Inline style of bottom navigation        | container: View.propTypes.style |    no    | iOS/Android |        yes        |

### BottomNavigation.Action

| Name    |                                Description                                 |                                               Type                                                | Required |  Platform   | HarmonyOS Support |
|:--------|:--------------------------------------------------------------------------:|:-------------------------------------------------------------------------------------------------:|:--------:|:-----------:|:-----------------:|
| icon    |        Will be rendered above the label as a content of the action.        |                                    PropTypes.string.isRequired                                    |   yes    | iOS/Android |        yes        |
| label   |         Will be rendered under the icon as a content of the action         |                                         PropTypes.string                                          |    no    | iOS/Android |        yes        |
| active  | True if the action is active (for now it'll be highlight by primary color) |                                     PropTypes.bool.isRequired                                     |   yes    | iOS/Android |        yes        |
| onPress |                        Callback for on press event                         |                                          PropTypes.func                                           |    no    | iOS/Android |        yes        |
| style   |                     Inline style of bottom navigation                      | container: View.propTypes.style<br>active: Text.propTypes.style<br>disabled: Text.propTypes.style |    no    | iOS/Android |        yes        |

### Button

| Name      |                      Description                       |                             Type                              | Required |  Platform   | HarmonyOS Support |
|:----------|:------------------------------------------------------:|:-------------------------------------------------------------:|:--------:|:-----------:|:-----------------:|
| disabled  |            If true button will be disabled             |                        PropTypes.bool                         |    no    | iOS/Android |        yes        |
| raised    |             If true button will be raised              |                        PropTypes.bool                         |    no    | iOS/Android |        yes        |
| primary   |        If the button should have primary color         |                        PropTypes.bool                         |    no    | iOS/Android |        yes        |
| accent    |         If the button should have accent color         |                       PropTypes.number                        |    no    | iOS/Android |        yes        |
| onPress   | Called when button is pressed. Text is passed as param |                        PropTypes.func                         |    no    | iOS/Android |        yes        |
| text      |              Text will be shown on button              |                  PropTypes.string.isRequired                  |   yes    | iOS/Android |        yes        |
| upperCase |        Button text will be in uppercase letters        |                        PropTypes.bool                         |    no    | iOS/Android |        yes        |
| icon      |        If specified it'll be shown before text         |                       PropTypes.string                        |    no    | iOS/Android |        yes        |
| style     |       You can override any style for this button       | container: View.propTypes.style<br>text: Text.propTypes.style |    no    | iOS/Android |        yes        |

### Card

| Name    |               Description                |       Type       | Required |  Platform   | HarmonyOS Support |
|:--------|:----------------------------------------:|:----------------:|:--------:|:-----------:|:-----------------:|
| onPress |       Called when card is pressed        |  PropTypes.func  |    no    | iOS/Android |        yes        |
| style   | You can override any style for this card | PropTypes.object |    no    | iOS/Android |        yes        |

### Checkbox

| Name          |                 Description                  |                                 Type                                 | Required |  Platform   | HarmonyOS Support |
|:--------------|:--------------------------------------------:|:--------------------------------------------------------------------:|:--------:|:-----------:|:-----------------:|
| label         |        Text will be shown after Icon         |                           PropTypes.string                           |   yes    | iOS/Android |        yes        |
| value         | Value will be returned when onCheck is fired | PropTypes.oneOfType([PropTypes.string, PropTypes.number]).isRequired |   yes    | iOS/Android |        yes        |
| checked       |              True if it's check              |                            PropTypes.bool                            |    no    | iOS/Android |        yes        |
| disabled      |              Is checkbox active              |                           PropTypes.bool,                            |    no    | iOS/Android |        yes        |
| uncheckedIcon |     Will be shown when checked is false      |                           PropTypes.string                           |    no    | iOS/Android |        yes        |
| checkedIcon   |      Will be shown when checked is true      |                           PropTypes.string                           |    no    | iOS/Android |        yes        |
| onCheck       |  Event that is called when state is changed  |                           PropTypes.func,                            |   yes    | iOS/Android |        yes        |

### Dialog:DialogDefaultActions

| Name          |                Description                |                                      Type                                       | Required |  Platform   | HarmonyOS Support |
|:--------------|:-----------------------------------------:|:-------------------------------------------------------------------------------:|:--------:|:-----------:|:-----------------:|
| actions       |        Button for displaying cards        |                 PropTypes.arrayOf(PropTypes.string).isRequired                  |   yes    | iOS/Android |        yes        |
| options       |       this will disable the button        |     PropTypes.shape({       actionName: { disabled: PropTypes.bool }     })     |    no    | iOS/Android |        yes        |
| onActionPress | Event triggered by pressing a card button |                            PropTypes.func.isRequired                            |   yes    | iOS/Android |        yes        |
| style         | You can override any style for this Card  | PropTypes.shape({         defaultActionsContainer: ViewPropTypes.style,     }), |    no    | iOS/Android |        yes        |

### Divider

| Name  |                 Description                 |                        Type                         | Required |  Platform   | HarmonyOS Support |
|:------|:-------------------------------------------:|:---------------------------------------------------:|:--------:|:-----------:|:-----------------:|
| inset |              Divider Move Back              |                   PropTypes.bool                    |    no    | iOS/Android |        yes        |
| style | You can override any style for this Divider | PropTypes.shape({container: View.propTypes.style }) |    no    | iOS/Android |        yes        |

### Drawer

| Name     |                Description                 |                                                       Type                                                        | Required |  Platform   | HarmonyOS Support |
|:---------|:------------------------------------------:|:-----------------------------------------------------------------------------------------------------------------:|:--------:|:-----------:|:-----------------:|
| children |           Subnodes in the drawer           |                                             PropTypes.node.isRequired                                             |   yes    | iOS/Android |        yes        |
| style    | You can override any style for this Drawer | style: PropTypes.shape({ container: ScrollView.propTypes.style,         contentContainer: View.propTypes.style}), |    no    | iOS/Android |        yes        |

#### Drawer:header

| Name            |                    Description                    |                                                  Type                                                   | Required |  Platform   | HarmonyOS Support |
|:----------------|:-------------------------------------------------:|:-------------------------------------------------------------------------------------------------------:|:--------:|:-----------:|:-----------------:|
| image           |              image for Drawer.header              |                           PropTypes.shape({ type: PropTypes.oneOf([Image]) })                           |    no    | iOS/Android |        yes        |
| backgroundColor |      Background image of the drawer header.       |                                            PropTypes.string                                             |    no    | iOS/Android |        No         |
| children        |           Subnodes in the drawer.header           |                                             PropTypes.node                                              |    no    | iOS/Android |        yes        |
| style           | You can override any style for this drawer.header | style: PropTypes.shape({contentContainer: View.propTypes.style,container: View.propTypes.style,     }), |    no    | iOS/Android |        yes        |

#### Drawer:HeaderAccount

| Name     |                    Description                    |                       Type                       | Required |  Platform   | HarmonyOS Support |
|:---------|:-------------------------------------------------:|:------------------------------------------------:|:--------:|:-----------:|:-----------------:|
| avatar   |          avatar for Drawer.HeaderAccount          |                PropTypes.element                 |    no    | iOS/Android |        yes        |
| accounts |         accounts for Drawer.HeaderAccount         |                 PropTypes.string                 |    no    | iOS/Android |        yes        |
| footer   |        footer in the Drawer.HeaderAccount         |                ListItem.propTypes                |    no    | iOS/Android |        yes        |
| style    | You can override any style for this drawer.header | PropTypes.shape({**Drawer:HeaderAccout style**}) |    no    | iOS/Android |        yes        |

##### Drawer:HeaderAccout style

| name                    | Type                 | Required | Platform    | HarmonyOS Support |
|-------------------------|----------------------|----------|-------------|-------------------|
| container               | View.propTypes.style | no       | iOS/Android | yes               |
| accountContainer        | View.propTypes.style | no       | iOS/Android | yes               |
| topContainer            | View.propTypes.style | no       | iOS/Android | yes               |
| avatarsContainer        | View.propTypes.style | no       | iOS/Android | yes               |
| activeAvatarContainer   | View.propTypes.style | no       | iOS/Android | yes               |
| inactiveAvatarContainer | View.propTypes.style | no       | iOS/Android | yes               |

#### Drawer:Section

| Name    |                    Description                     |                     Type                     | Required |  Platform   | HarmonyOS Support |
|:--------|:--------------------------------------------------:|:--------------------------------------------:|:--------:|:-----------:|:-----------------:|
| title   |             title of drawers:sections              |               PropTypes.string               |   yes    | iOS/Android |        yes        |
| items   |             tems of drawers:isections              |          **Drawer:Section  items**           |   yes    | iOS/Android |        yes        |
| divider |             dividerof drawers:sections             |                PropTypes.bool                |    no    | iOS/Android |        yes        |
| style   | You can override any style for this Drawer:Section | PropTypes.shape({**Drawer:Section  style**}) |    no    | iOS/Android |        No         |

##### Drawer:Section  items

| name        | Type                                                                  | Required | Platform    | HarmonyOS Support |
|-------------|-----------------------------------------------------------------------|----------|-------------|-------------------|
| icon        | PropTypes.string                                                      | no       | iOS/Android | yes               |
| value       | PropTypes.oneOfType([PropTypes.string, PropTypes.element]).isRequired | yes      | iOS/Android | yes               |
| label       | PropTypes.string                                                      | no       | iOS/Android | yes               |
| onPress     | PropTypes.func                                                        | no       | iOS/Android | yes               |
| onLongPress | PropTypes.func                                                        | no       | iOS/Android | No                |
| active      | PropTypes.bool                                                        | no       | iOS/Android | yes               |
| disabled    | PropTypes.bool                                                        | no       | iOS/Android | No                |

##### 

### ListItem

| Name                |                   Description                    |                                                                                               Type                                                                                                | Required |  Platform   | HarmonyOS Support |
|:--------------------|:------------------------------------------------:|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|:--------:|:-----------:|:-----------------:|
| dense               |                    generally                     |                                                                                          PropTypes.bool                                                                                           |    no    | iOS/Android |        yes        |
| divider             |                     divider                      |                                                                                          PropTypes.bool                                                                                           |    no    | iOS/Android |        yes        |
| onPress             |          Called when ListItemis pressed          |                                                                                          PropTypes.func                                                                                           |    no    | iOS/Android |        yes        |
| numberOfLines       |                   line number                    |                                                                               PropTypes.oneOf([1, 2, 3, 'dynamic'])                                                                               |    no    | iOS/Android |        yes        |
| style               |   You can override any style for this Listltem   |                                                                                          ListItem  style                                                                                          |    no    | iOS/Android |        yes        |
| leftElement         |                    left side                     |                                                                PropTypes.oneOfType([         PropTypes.element,PropTypes.string ]                                                                 |    no    | iOS/Android |        yes        |
| onLeftElementPress  | Event triggered when the left button is pressed  |                                                                                          PropTypes.func                                                                                           |    no    | iOS/Android |        No         |
| centerElement       |                   center side                    | PropTypes.oneOfType([PropTypes.element,         PropTypes.string,  PropTypes.shape({primaryText: PropTypes.string.isRequired,secondaryText: PropTypes.string,tertiaryText: PropTypes.string }) ]) |   yes    | iOS/Android |        yes        |
| rightElement        |                    right side                    |                          PropTypes.element, PropTypes.string,         PropTypes.shape({ menu: PropTypes.shape({                 labels: PropTypes.array.isRequired}) })                           |    no    | iOS/Android |        yes        |
| onRightElementPress | Event triggered when the right button is pressed |                                                                                          PropTypes.func                                                                                           |    no    | iOS/Android |        yes        |
| children            |                    child node                    |                                                                                          PropTypes.node                                                                                           |    no    | iOS/Android |        yes        |

##### ListItem  style

| name                   | Type                 | Required | Platform    | HarmonyOS Support |
|------------------------|----------------------|----------|-------------|-------------------|
| container              | View.propTypes.style | no       | iOS/Android | yes               |
| contentViewContainer   | View.propTypes.style | no       | iOS/Android | yes               |
| leftElementContainer   | View.propTypes.style | no       | iOS/Android | yes               |
| centerElementContainer | View.propTypes.style | no       | iOS/Android | yes               |
| textViewContainer      | View.propTypes.style | no       | iOS/Android | yes               |
| primaryText            | Text.propTypes.style | no       | iOS/Android | yes               |
| firstLine              | View.propTypes.style | no       | iOS/Android | yes               |
| primaryTextContainer   | Text.propTypes.style | no       | iOS/Android | yes               |
| secondaryText          | Text.propTypes.style | no       | iOS/Android | yes               |
| tertiaryText           | Text.propTypes.style | no       | iOS/Android | yes               |
| rightElementContainer  | View.propTypes.style | no       | iOS/Android | yes               |
| leftElement            | View.propTypes.style | no       | iOS/Android | yes               |
| rightElement           | View.propTypes.style | no       | iOS/Android | yes               |

### Subheader

| Name  |                  Description                  |                                     Type                                      | Required |  Platform   | HarmonyOS Support |
|:------|:---------------------------------------------:|:-----------------------------------------------------------------------------:|:--------:|:-----------:|:-----------------:|
| text  |                Displayed text                 |                          PropTypes.string.isRequired                          |   yes    | iOS/Android |        yes        |
| inset |              Subheader Move Back              |                                PropTypes.bool                                 |    no    | iOS/Android |        yes        |
| lines |            Subheader lines number             |                               PropTypes.number                                |    no    | iOS/Android |        yes        |
| style | You can override any style for this Subheader | PropTypes.shape({container: View.propTypes.style ,text:Text.propTypes.style}) |    no    | iOS/Android |        yes        |

### Snackbar

| Name             |                        Description                         |                               Type                                | Required |  Platform   | HarmonyOS Support |
|:-----------------|:----------------------------------------------------------:|:-----------------------------------------------------------------:|:--------:|:-----------:|:-----------------:|
| message          |                The text message to display.                |                    PropTypes.string.isRequired                    |   yes    | iOS/Android |        yes        |
| visible          |          Whether or not the snackbar is visible.           |                          PropTypes.bool                           |    no    | iOS/Android |        yes        |
| timeout          |  The amount of time in milliseconds to show the snackbar   |                         PropTypes.number                          |    no    | iOS/Android |        yes        |
| onRequestClose   |          Callback for when the timeout finishes.           |                     PropTypes.func.isRequired                     |   yes    | iOS/Android |        yes        |
| bottomNavigation | Whether or not there is a bottom navigation on the screen. |                          PropTypes.bool                           |    no    | iOS/Android |        yes        |
| onActionPress    |    The function to execute when the action is clicked.     |                          PropTypes.func                           |    no    | iOS/Android |        yes        |
| actionText       |    The function to execute when the action is clicked.     |                          PropTypes.func                           |    no    | iOS/Android |        yes        |
| style            |                  Inline style of snackbar                  | container: ViewPropTypes.style,     message: ViewPropTypes.style, |    no    | iOS/Android |        yes        |
| button           |                           button                           |                            ButtonProps                            |    no    | iOS/Android |        yes        |

### Toolbar

| Name                |                                         Description                                          |         Type         | Required |     Platform     | HarmonyOS Support |
|:--------------------|:--------------------------------------------------------------------------------------------:|:--------------------:|:--------:|:----------------:|:-----------------:|
| isSearchActive      |                             Indicates if search is active or not                             |    PropTypes.bool    |   yes    |   iOS/Android    |        yes        |
| searchable          | When you want to activate search feature you have to pass this object with config of search. | **searchable props** |   yes    |   iOS/Android    |        yes        |
| size                |                        This size is used for each icon on the toolbar                        |   PropTypes.number   |    no    |   iOS/Android    |        yes        |
| style               |                  You can override any style for the component via this prop                  |  **Toolbar style**   |    no    |   iOS/Android    |        yes        |
| hidden              |                            Wether or not the Toolbar should show                             |    PropTypes.bool    |    no    |   iOS/Android    |        No         |
| onPress             |                            Called when centerElement was pressed.                            |    PropTypes.func    |    no    |   iOS/Android    |        yes        |
| leftElement         |                               Will be shown on the left side.                                |  PropTypes.element   |    no    |   iOS/Android    |        yes        |
| onLeftElementPress  |                             Called when leftElement was pressed.                             |    PropTypes.func    |    no    |   iOS/Android    |        yes        |
| centerElement       |          Will be shown between leftElement and rightElement. Usually use for title.          | PropTypes.element    |    no    |   iOS/Android    |        yes        |
| rightElement        |                               Will be shown on the right side                                |  rightElement props  |    no    |   iOS/Android    |        yes        |
| onRightElementPress |                             Called when rightElement was pressed                             |    PropTypes.func    |    no    |   iOS/Android    |        yes        |

##### searchable props

| name                   | Description                                                        | Type             | Required | Platform    | HarmonyOS Support |
|------------------------|--------------------------------------------------------------------|------------------|----------|-------------|-------------------|
| onChangeText           | Called when search text was changed.                               | PropTypes.func   | no       | iOS/Android | yes               |
| onSearchClosed         | Called when search was closed.                                     | PropTypes.func   | no       | iOS/Android | yes               |
| onSearchCloseRequested | Called when action to close search was requested.                  | PropTypes.func   | no       | iOS/Android | yes               |
| onSearchPressed        | Called when search was opened                                      | PropTypes.func   | no       | iOS/Android | yes               |
| onSubmitEditing        | Called when user press submit button on hw keyboard                | PropTypes.func   | no       | iOS/Android | yes               |
| placeholder            | Will shown as placeholder for search input.                        | PropTypes.string | no       | iOS/Android | yes               |
| autoFocus              | Indicates when input should be focused after the search is opened. | PropTypes.bool   | no       | iOS/Android | yes               |
| autoCapitalize         | Enable auto-capitalize for search input                            | PropTypes.string | no       | iOS/Android | No                |
| autoCorrect            | Enable auto-correct for search input                               | PropTypes.bool   | no       | iOS/Android | No                |
| icon                   | Override default search icon                                       | PropTypes.string | no       | iOS/Android | yes               |

##### rightElement props

| name                                 | Description                                                    | Required | Platform    | HarmonyOS Support |
|--------------------------------------|----------------------------------------------------------------|----------|-------------|-------------------|
| PropTypes.element                    | One action (name of icon). Alias for<Icon>.                    | no       | iOS/Android | yes               |
| PropTypes.string                     | One action (name of icon). Alias for ['icon1'].                | no       | iOS/Android | yes               |
| PropTypes.arrayOf(PropTypes.string), | For many actions: ['icon1', 'icon2', ...]                      | no       | iOS/Android | yes               |
| PropTypes.shape                      | For actions and menu. The menu will be shown as last one icon. | no       | iOS/Android | yes               |

##### Toolbar style

| name                   | Type                          | Required | Platform    | HarmonyOS Support |
|------------------------|-------------------------------|----------|-------------|-------------------|
| container              | Animated.View.propTypes.style | no       | iOS/Android | yes               |
| leftElementContainer   | View.propTypes.style          | no       | iOS/Android | yes               |
| leftElement            | Text.propTypes.style,         | no       | iOS/Android | yes               |
| centerElementContainer | View.propTypes.style          | no       | iOS/Android | yes               |
| titleText              | Text.propTypes.style,         | no       | iOS/Android | yes               |
| rightElementContainer  | View.propTypes.style          | no       | iOS/Android | yes               |
| rightElement           | Text.propTypes.style          | no       | iOS/Android | yes               |

## 主题

**如果您想使用默认主题，可以跳过此步骤**

如果您想更改应用程序的主色，只需将自己的设置传递给 ThemeContext.Provider 对象即可。这些设置将与默认主题合并。

```jsx
import React, { Component } from 'react';
import { Navigator, NativeModules } from 'react-native';

import { COLOR, ThemeContext, getTheme } from 'react-native-material-ui';

// you can set your style right here, it'll be propagated to application
const uiTheme = {
  palette: {
    primaryColor: COLOR.green500,
  },
  toolbar: {
    container: {
      height: 50,
    },
  },
};

class Main extends Component {
  render() {
    return (
      <ThemeContext.Provider value={getTheme(uiTheme)}>
        <App />
      </ThemeContext.Provider>
    );
  }
}

```

## 遗留问题

## 其他

- RadioButton组件功能在Android和iOS不生效， HarmonyOS与Android,iOS表现一致。[原库 issue](https://github.com/xotahal/react-native-material-ui/issues/25)
-  BottomNavigation和Toolbar组件hidden属性功能在Android和iOS不生效， HarmonyOS与Android,iOS表现一致。[原库 issue](https://github.com/xotahal/react-native-material-ui/issues/357)
-  Toolbar组件autoCapitalize属性和autoCorrect功能在Android和iOS不生效， HarmonyOS与Android,iOS表现一致。[原库 issue](https://github.com/xotahal/react-native-material-ui/issues/520)
-  Drawer:Section组件中的style属性设置样式在Android和iOS不生效，HarmonyOS与Android,iOS表现一致。[原库 issue](https://github.com/xotahal/react-native-material-ui/issues/160)
-  Drawer:Section组件中itmes属性对象中的onLongPress属性和disabled属性在Android和iOS不生效，HarmonyOS与Android,iOS表现一致。[原库 issue](https://github.com/xotahal/react-native-material-ui/issues/521)
-  ListItem组件中onLeftElementPress属性在Android和iOS不生效，HarmonyOS与Android,iOS表现一致。[原库 issue](https://github.com/xotahal/react-native-material-ui/issues/522)
-  Drawer:Header组件中backgroundColor属性与子元素中的Style属性冲突在Android和iOS不生效，HarmonyOS与Android,iOS表现一致。[原库 issue](https://github.com/xotahal/react-native-material-ui/issues/523)

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/xotahal/react-native-material-ui/blob/master/LICENSE)，请自由地享受和参与开源。

