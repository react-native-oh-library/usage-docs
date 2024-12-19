> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>styled-components</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/styled-components/styled-components/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/styled-components/styled-components)

## Installation and Usage

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
npm install styled-components@6.1.8
```

#### **yarn**

```bash
yarn add styled-components@6.1.8
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

```js
import React, { useState } from 'react';
import styled from 'styled-components/native';

const Container = styled.View`
  flex: 1;
  justify-content: center;
  align-items: center;
  background-color: #f5fcff;
`;

const StyledText = styled.Text`
  font-size: 24px;
  color: ${(props) => (props.children === 'Highlighted!' ? 'tomato' : 'black')};
  margin-bottom: 20px;
`;

const StyledButton = styled.TouchableOpacity`
  background-color: #3498db;
  padding: 10px 20px;
  border-radius: 5px;
`;

const ButtonText = styled.Text`
  color: white;
  font-size: 18px;
`;

const App = () => {
  const [text, setText] = useState('Normal Text');

  const toggleText = () => {
    setText(text === 'Normal Text' ? 'Highlighted!' : 'Normal Text');
  };

  return (
    <Container>
      <StyledText>{text}</StyledText>
      <StyledButton onPress={toggleText}>
        <ButtonText>Toggle Text</ButtonText>
      </StyledButton>
    </Container>
  );
};

export default App;
```

## Constraints

### Compatibility

This document is verified based on the following versions:

1. RNOH：0.72.11; SDK：OpenHarmony(api11) 4.1.0.53; IDE：DevEco Studio 4.1.3.412; ROM：2.0.0.52(SP22C00E52R1P17log);
2. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;

## Properties

For details, see [styled-components GitHub](https://github.com/styled-components/styled-components)

| Name              | Description                                                                                                                                                                                  | Type          | Required | Platform |  HarmonyOS Support |
| ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------- | -------- | -------- | -------- |
| ThemeProvider     | A helper component for theming.                                                                                                                                                       | component     | No       | /        | Yes      |
| css               | The css prop is a convenient way to iterate on your components without settling on fixed component boundaries yet                                                                     | prop          | No       | /        | Yes      |
| toStyleSheet      | convert a style object to a stylesheet object                                                                                                                                         | function      | No       | /        | Yes      |
| ThemeContext      | access the theme object and pass the theme object to the style component                                                                                                              | jsx component | No       | /        | Yes      |
| isStyledComponent | A utility to help identify styled components.                                                                                                                                         | function      | No       | /        | Yes      |
| withTheme         | This is a higher order component factory to get the current theme from a ThemeProvider and pass it to your component as a theme prop.                                                 | function      | No       | /        | Yes      |
| useTheme          | This is a custom hook to get the current theme from a ThemeProvider.                                                                                                                  | function      | No       | /        | Yes      |
| ThemeConsumer     | It passes the current theme (based on a ThemeProvider higher in your component tree) as an argument to the child function. From this function, you may return further JSX or nothing. | jsx component | No       | /        | Yes      |
| createGlobalstyle | A helper function to generate a special StyledComponent that handles global styles                                                                                                    | function      | No       | Web      | No       |
| keyframes         | A helper method to create keyframes for animations.                                                                                                                                   | function      | No       | Web      | No       |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/styled-components/styled-components/blob/main/LICENSE)
