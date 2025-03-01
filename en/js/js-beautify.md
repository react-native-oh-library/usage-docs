> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>js-beautify</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/beautifier/js-beautify/blob/main/LICENSE>">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/beautifier/js-beautify)

## Installation and Usage

<!-- tabs:start -->

#### **npm**

```bash
npm install js-beautify@^1.15.1
```

#### **yarn**

```bash
ynpm install js-beautify@^1.15.1
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

For details, see [js-beautify Official demo](https://beautifier.io/)

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React from 'react';
import type {PropsWithChildren} from 'react';
import {
  SafeAreaView,
  ScrollView,
  StatusBar,
  StyleSheet,
  Text,
  useColorScheme,
  View,
} from 'react-native';

import {js_beautify, html_beautify, css_beautify} from 'js-beautify';

var uglyJs = "function(){console.log('Hello, World!');}";
var prettyJs = js_beautify(uglyJs);
console.log(uglyJs);
console.log(prettyJs);

var uglyHtml =
  '<!DOCTYPE html><head><title>Simple HTML5 Website</title></head><body><p>Welcome to My Website</p></body></html>';
var prettyHtml = html_beautify(uglyHtml);
console.log(uglyHtml);
console.log(prettyHtml);

var uglyCss =
  '<style>header{background-color: #333;color: #fff;padding: 10px 0;text-align: center;}</style>';
var prettyCss = css_beautify(uglyCss);
console.log(uglyCss);
console.log(prettyCss);

('use strict');

var code = 'x=3.14;myFunction();function myFunction() {y=3.14,z=1024}';
var code1 = js_beautify(code, {indent_size: 8}); 
var code2 = js_beautify(code, {indent_char: '\t'});
var code3 = js_beautify(code, {indent_with_tabs: true});
console.log(code);
console.log(code1);
console.log(code2);
console.log(code3);

//"end_with_newline": false, 
var obj1 = {completed: false, id: 1, title: 'delectus aut autem', userId: 1};
var dataJson1 = JSON.stringify(obj1);
var prettyObj1 = js_beautify(dataJson1, {
  end_with_newline: false,
});
console.log(dataJson1);
console.log(prettyObj1);

//"max_preserve_newlines": 2,
var text1 = `Is there any





available space here`;
var prettyText1 = js_beautify(text1, {
  max_preserve_newlines: 2,
});
console.log(text1);
console.log(prettyText1);

// "space_after_anon_function": true
var text2 = `(function(){
  alert(1);
})();`;
var prettyText2 = js_beautify(text2, {
  space_after_anon_function: true, 
});
console.log(text2);
console.log(prettyText2);

var text3 = `[{id:1,title:"Trendy Women's Clothing"},
  {id:2,title:"Branded menswear"},
  {id:3,title:"Mobile phone and computer"}] `;
var prettyText3 = js_beautify(text3, {
  keep_array_indentation: true,
});
console.log(text3);
console.log(prettyText3);

//e4x test
var text4 = `<book>
  <title>Catch 22</title>
  <author>Joseph Heller</author>
  <year>1961</year>
  <publisher>Simon & Schuster</publisher>
</book>`;
var prettyText4 = js_beautify(text4, {
  e4x: false, 
});
console.log(text4);
console.log(prettyText4);

// "space-after-named-function": true
var text5 = ` function foo(){
    return true;
  }`;
var prettyText5 = js_beautify(text5, {
  'space-after-named-function': true, 
});
console.log(text5);
console.log(prettyText5);

var text6 = `const array = [1, 2, 3, 4, 5];
    const newArray = array
        .map(item => item * 2)
        .filter(item => item > 5)
        .reduce((acc, cur) => acc + cur, 0);`;

var prettyText6 = js_beautify(text6, {
  'unindent-chained-methods': false,
});
console.log(text6);
console.log(prettyText6);

// "break-chained-methods": true
var text7 = `var arr = [1, 2, 3, 4, 5];
  var sum = arr.map(x => x * 2).filter(x => x > 5).reduce((a, b) => a + b);
  console.log(sum);`;

var prettyText7 = js_beautify(text7, {
  'break-chained-methods': true,
});
console.log(text7);
console.log(prettyText7);

var text8 = "function hello(name){return 'Hello, '+name+'!';}";
var prettyText8 = js_beautify(text8, {
  space_in_paren: true, 
});
console.log(text8);
console.log(prettyText8);

var text9 = `function greet(){
    console.log('Hello, world!');
}
greet();`;
var prettyText9 = js_beautify(text9, {
  space_in_empty_paren: true,
});
console.log(text9);
console.log(prettyText9);

var text10 = `var arr = [1,2,3,
  4,
  5, 6,     7,
  8,
  9];`;

var prettyText10 = js_beautify(text10, {
  indent_size: 0,
  keep_array_indentation: false,
});
var prettyCode11 = js_beautify(text10, {
  indent_size: 0,
  keep_array_indentation: true,
});
console.log(text10);
console.log(prettyText10);
console.log(prettyCode11);

var text12 = 'let a = 1+2+3+4+5+6\n+7+8+9+10;';
var prettyText12 = js_beautify(text12, {operator_position: 'before-newline'});
var prettyCode13 = js_beautify(text12, {operator_position: 'after-newline'});
var prettyCode14 = js_beautify(text12, {operator_position: 'preserve-newline'});

console.log('Original code:' + text12);
console.log(prettyText12);
console.log(prettyCode13);
console.log(prettyCode14);


var text13 = `function() {

  return 'Hello world!';

  }`;
var prettyText13 = js_beautify(text13, {indent_empty_lines: true});
console.log(text13);
console.log('indent_empty_lines:' + prettyText13);


var text14 =
  "This is a very long string that definitely.exceeds the typical line length you'd see in most code editors. It should be automatically wrapped by js-beautify.";
var prettyText14 = js_beautify(text14, {indent_size: 2, wrap_line_length: 20});
var prettyText15 = js_beautify(text14, {indent_size: 2, wrap_line_length: 10});
console.log(prettyText14);

var sourceCode =
  'h1 {color: red; font-size: 20px;} h2 {color: blue; font-size: 18px;}';

var prettySourceCode1 = css_beautify(sourceCode, {indent_size: 2});
console.log(prettySourceCode1);


var prettySourceCode2 = css_beautify(sourceCode, {indent_char: ' '});
console.log(prettySourceCode2);


var prettySourceCode3 = css_beautify(sourceCode, {indent_with_tabs: true});
console.log(prettySourceCode3);


var prettySourceCode4 = css_beautify(sourceCode, {eol: '\n'});
console.log(prettySourceCode4);


var prettySourceCode5 = css_beautify(sourceCode, {end_with_newline: false});
var prettySourceCode55 = css_beautify(sourceCode, {end_with_newline: true});
console.log(prettySourceCode5);
console.log(prettySourceCode55);


var prettySourceCode6 = css_beautify(sourceCode, {brace_style: 'expand'});
console.log(prettySourceCode6);

var sourceCode1 = 'div, p, span { color: red; }';

var prettySourceCode7 = css_beautify(sourceCode1, {
  selector_separator_newline: 'true',
});
console.log(prettySourceCode7);

var sourceCode2 = '.class1 {color: red;} .class2 {background-color: blue;}';

var prettySourceCode8 = css_beautify(sourceCode2, {
  newline_between_rules: 'true',
});
console.log(prettySourceCode8);

var sourceCode3 =
  '<html><head><title>My Title</title></head><body></body></html>';
var prettySourceCode9 = html_beautify(sourceCode3, {indent_size: 10});
console.log(prettySourceCode9);

var prettySourceCode10 = html_beautify(sourceCode3, {indent_char: ' '});
console.log(prettySourceCode10);

var prettySourceCode11 = html_beautify(sourceCode3, {indent_with_tabs: false});
console.log(prettySourceCode11);

var prettySourceCode12 = html_beautify(sourceCode3, {eol: '\n'});
console.log(prettySourceCode12);

var prettySourceCode13 = html_beautify(sourceCode3, {end_with_newline: false});
console.log(prettySourceCode13);

var prettySourceCode14 = html_beautify(sourceCode3, {
  'indent-inner-html': true,
});
console.log(prettySourceCode14);

var sourceCode4 =
  '<html><head><title>My \nTitle</title></head><body></body></html>';
var prettySourceCode15 = html_beautify(sourceCode4, {preserve_newlines: true});
console.log(prettySourceCode15);

var sourceCode5 = `<html><head></head>
<body>
<p>Hello</p>
<p>World!</p>




<p>More content!</p>
</body></html>`;
var options = {
  indent_size: '4',
  indent_char: ' ',
  max_preserve_newlines: 2,
  preserve_newlines: true,
};
var prettySourceCode16 = html_beautify(sourceCode5, options);
console.log(prettySourceCode16);

var sourceCode6 = `<!DOCTYPE html>
<html>
  <head>
    <style type="text/css">
      body {background-color: #f0f0f0;}
    </style>
  </head>
  <body>
    <p>The background color of this page is gray.</p>
  </body>
</html>`;
var prettySourceCode17 = html_beautify(sourceCode6, {brace_style: 'collapse'});
console.log(prettySourceCode17);


var sourceCode7 = `
<html>
<head>
<script>var a = 1;
var b = 2;</script>
</head>
<body>
<h1>Test</h1>
<p>Hello World</p>
</body>
</html>`;
var prettySourceCode18 = html_beautify(sourceCode7, {indent_scripts: 'normal'});
console.log(prettySourceCode18);


var options1 = {
  indent_size: '2', 
  indent_char: ' ', 
  wrap_line_length: '50',
};
var sourceCode8 =
  '<p>This is a very long paragraph, and it contains a lot of text and tags, which makes it difficult to present clearly in one line.</p><div><h1>title</h1><p>content</p></div>';
var prettySourceCode19 = html_beautify(sourceCode8, options1);
console.log(prettySourceCode19);


var sourceCode9 = `<a href="http://example.com" id="someid" class="someclass" style="color:blue;">Link</a>`;
console.log('Original HTML:');
console.log(sourceCode9);
var prettySourceCode20 = html_beautify(sourceCode9, {
  wrap_attributes: 'auto',
  wrap_line_length: 80,
});
console.log("\n'auto':");
console.log(prettySourceCode20);
var prettySourceCode21 = html_beautify(sourceCode9, {wrap_attributes: 'force'});
console.log("\n'force':");
console.log(prettySourceCode21);
var prettySourceCode22 = html_beautify(sourceCode9, {
  wrap_attributes: 'force-aligned',
});
console.log("\n'force-aligned':");
console.log(prettySourceCode22);
var prettySourceCode23 = html_beautify(sourceCode9, {
  wrap_attributes: 'force-expand-multiline',
});
console.log("\n'force-expand-multiline':");
console.log(prettySourceCode23);

//wrap_attributes_min_attrs 设置属性的个数到达多少时，每个属性都会换行,默认为2
var options3 = {
  indent_size: 2,
  wrap_attributes: 'force-expand-multiline',
  wrap_attributes_min_attrs: 2,
};
var prettySourceCode24 = html_beautify(sourceCode9, options3);
console.log("\n'wrap_attributes_min_attrs':2");
console.log(prettySourceCode24);

var options4 = {
  indent_size: 2,
  wrap_attributes: 'force-expand-multiline',
  wrap_attributes_min_attrs: 6,
};
var prettySourceCode25 = html_beautify(sourceCode9, options4);
console.log("\n'wrap_attributes_min_attrs':6");
console.log(prettySourceCode25);

var prettySourceCode26 = html_beautify(sourceCode9, {
  wrap_attributes: 'force-expand-multiline', 
  wrap_attributes_indent_size: 10, 
});
console.log("\n'wrap_attributes_indent_size':10");
console.log(prettySourceCode26);

var sourceCode10 = '<p><span>Hello</span></p><p><span>World</span></p>';
var prettySourceCode27 = html_beautify(sourceCode10, {inline: ['span']});
console.log('Original code');
console.log(sourceCode10);
console.log("\n'inline': ['span']");
console.log(prettySourceCode27);


var sourceCode11 = `<button-component>lorem ipsum</button-component>`;
var prettySourceCode28 = html_beautify(sourceCode11, {
  nline_custom_elements: true,
});
console.log('Original code');
console.log(sourceCode11);
console.log("\n'nline_custom_elements':true");
console.log(prettySourceCode28);


var sourceCode12 =
  '<div><span>This is a test</span><b>test<b/><i>test<i/></div>';
var prettySourceCode29 = html_beautify(sourceCode12, {
  unformatted: ['span', 'b', 'i'],
});
console.log('Original code');
console.log(sourceCode12);
console.log("\n''unformatted': ['span', 'b', 'i']");
console.log(prettySourceCode29);


var sourceCode13 = `
<pre>
This is some preformatted text.
It should be preserved just like this.
</pre>
<div>
This is some div content.
The formatting should be improved.
</div>`;
var prettySourceCode30 = html_beautify(sourceCode13, {
  content_unformatted: ['pre'],
});
console.log('Original code');
console.log(sourceCode13);
console.log("\n'content_unformatted': ['pre']");
console.log(prettySourceCode30);


var sourceCode14 = `<div><p>Hello World!</p></div>`;
var prettySourceCode31 = html_beautify(sourceCode14, {extra_liners: ['p']});
console.log('Original code');
console.log(sourceCode14);
console.log("\n'extra_liners': ['p']");
console.log(prettySourceCode31);

function BeautifyDemo(): JSX.Element {
  0;

  return (
    <ScrollView contentInsetAdjustmentBehavior="automatic">
      <View>
        <Text style={styles.titleStyle}>{'\nOriginal JS:'}</Text>
        <Text>{uglyJs}</Text>
        <Text style={styles.titleStyle}>{'\nprettyJs:'}</Text>
        <Text>{prettyJs}</Text>
        <Text style={styles.titleStyle}>{'\nOriginal HTML:'}</Text>
        <Text>{uglyHtml}</Text>
        <Text style={styles.titleStyle}>{'\npretty HTML:'}</Text>
        <Text>{prettyHtml}</Text>
        <Text style={styles.titleStyle}>{'\nOriginal CSS:'}</Text>
        <Text>{uglyCss}</Text>
        <Text style={styles.titleStyle}>{'\npretty CSS:'}</Text>
        <Text>{prettyCss}</Text>
        <Text style={styles.textStyle}>Js TEST</Text>
        <Text style={styles.titleStyle}>{'\nOriginal JS:'}</Text>
        <Text>{code}</Text>
        <Text style={styles.titleStyle}>{"\n'indent_size': 8"}</Text>
        <Text>{code1}</Text>
        <Text style={styles.titleStyle}>{"\n'indent_char':'\t'"}</Text>
        <Text>{code2}</Text>
        <Text style={styles.titleStyle}>{"\n'indent_with_tabs': true"}</Text>
        <Text>{code3}</Text>
        <Text style={styles.titleStyle}>{'\nOriginal JS:'}</Text>
        <Text>{dataJson1}</Text>
        <Text style={styles.titleStyle}>{"\n'end_with_newline'："}</Text>
        <Text>{prettyObj1}</Text>
        <Text style={styles.titleStyle}>{'\nOriginal JS:'}</Text>
        <Text>{text1}</Text>
        <Text style={styles.titleStyle}>{"\n'max_preserve_newlines':2"}</Text>
        <Text>{prettyText1}</Text>
        <Text style={styles.titleStyle}>{'\nOriginal JS:'}</Text>
        <Text>{text2}</Text>
        <Text style={styles.titleStyle}>
          {"\n'space_after_anon_function':true"}
        </Text>
        <Text>{prettyText2}</Text>
        <Text style={styles.titleStyle}>{'\nOriginal JS:'}</Text>
        <Text>{text3}</Text>
        <Text style={styles.titleStyle}>
          {"\n'keep_array_indentation':true"}
        </Text>
        <Text>{prettyText3}</Text>
        <Text style={styles.titleStyle}>{'\nOriginal JS:'}</Text>
        <Text>{text4}</Text>
        <Text style={styles.titleStyle}>{"\n'e4x': false"}</Text>
        <Text>{prettyText4}</Text>
        <Text style={styles.titleStyle}>{'\nOriginal JS:'}</Text>
        <Text>{text5}</Text>
        <Text style={styles.titleStyle}>
          {"\n'space-after-named-function':true"}
        </Text>
        <Text>{prettyText5}</Text>
        <Text style={styles.titleStyle}>{'\nOriginal JS:'}</Text>
        <Text>{text6}</Text>
        <Text style={styles.titleStyle}>
          {"\n'unindent-chained-methods':false"}
        </Text>
        <Text>{prettyText6}</Text>
        <Text style={styles.titleStyle}>{'\nOriginal JS:'}</Text>
        <Text>{text7}</Text>
        <Text style={styles.titleStyle}>
          {"\n'break-chained-methods':true"}
        </Text>
        <Text>{prettyText7}</Text>
        <Text style={styles.titleStyle}>{'\nOriginal JS:'}</Text>
        <Text>{text8}</Text>
        <Text style={styles.titleStyle}>{"\n'space_in_paren':true"}</Text>
        <Text>{prettyText8}</Text>
        <Text style={styles.titleStyle}>{'\nOriginal JS:'}</Text>
        <Text>{text9}</Text>
        <Text style={styles.titleStyle}>{"\n'space_in_empty_paren':true"}</Text>
        <Text>{prettyText9}</Text>
        <Text style={styles.titleStyle}>{'\nOriginal JS:'}</Text>
        <Text>{text10}</Text>
        <Text style={styles.titleStyle}>
          {"\n'keep_array_indentation': false ,:"}
        </Text>
        <Text>{prettyText10}</Text>
        <Text style={styles.titleStyle}>
          {"\n'keep_array_indentation': true ,:"}
        </Text>
        <Text>{prettyCode11}</Text>
        <Text style={styles.titleStyle}>{'\nOriginal JS:'}</Text>
        <Text>{text12}</Text>
        <Text style={styles.titleStyle}>
          {"\noperator_position: 'before-newline'："}
        </Text>
        <Text>{prettyText12}</Text>
        <Text style={styles.titleStyle}>
          {"\noperator_position: 'after-newline'："}
        </Text>
        <Text>{prettyCode13}</Text>
        <Text style={styles.titleStyle}>
          {"\noperator_position: 'preserve-newline'："}
        </Text>
        <Text>{prettyCode14}</Text>
        <Text style={styles.titleStyle}>{'\nOriginal JS:'}</Text>
        <Text>{text13}</Text>
        <Text style={styles.titleStyle}>{"\n'indent-empty-lines'： "}</Text>
        <Text>{prettyText13}</Text>
        <Text style={styles.titleStyle}>{'\nOriginal JS:'}</Text>
        <Text>{text14}</Text>
        <Text style={styles.titleStyle}>{"\n'wrap_line_length': 20，： "}</Text>
        <Text>{prettyText14}</Text>
        <Text style={styles.titleStyle}>{"\n'wrap_line_length': 10，："}</Text>
        <Text>{prettyText15}</Text>
        <Text style={styles.textStyle}>Css TEST</Text>
        <Text style={styles.titleStyle}>{'\npretty CSS:'}</Text>
        <Text>{sourceCode}</Text>
        <Text style={styles.titleStyle}>{"\n'indent_size: 2'"}</Text>
        <Text>{prettySourceCode1}</Text>
        <Text style={styles.titleStyle}>{"\n'indent_char': ' '"}</Text>
        <Text>{prettySourceCode2}</Text>
        <Text style={styles.titleStyle}>{"\n'indent_with_tabs': true"}</Text>
        <Text>{prettySourceCode3}</Text>
        <Text style={styles.titleStyle}>{"\n'eol: \n'"}</Text>
        <Text>{prettySourceCode4}</Text>
        <Text style={styles.titleStyle}>{"\n'end_with_newline': false"}</Text>
        <Text>{prettySourceCode5}this use " end_with_newline": false,it can't change the line</Text>
        <Text style={styles.titleStyle}>{"\n'end_with_newline': true"}</Text>
        <Text>{prettySourceCode55}this use " end_with_newline": true,it can change the line</Text>
        <Text style={styles.titleStyle}>{"\n'brace_style': 'collapse'"}</Text>
        <Text>{prettySourceCode6}</Text>
        <Text style={styles.titleStyle}>{'\npretty CSS:'}</Text>
        <Text>{sourceCode1}</Text>
        <Text style={styles.titleStyle}>
          {"\n'selector_separator_newline': 'true'"}
        </Text>
        <Text>{prettySourceCode7}</Text>
        <Text style={styles.titleStyle}>{'\npretty CSS:'}</Text>
        <Text>{sourceCode2}</Text>
        <Text style={styles.titleStyle}>
          {"\n'newline_between_rules': 'true'"}
        </Text>
        <Text>{prettySourceCode8}</Text>

        <Text style={styles.textStyle}>html TEST</Text>
        <Text style={styles.titleStyle}>{'Original HTML:'}</Text>
        <Text>{sourceCode3}</Text>
        <Text style={styles.titleStyle}>{"\n'indent_size': 10"}</Text>
        <Text>{prettySourceCode9}</Text>
        <Text style={styles.titleStyle}>{"\n'indent_char':''"}</Text>
        <Text>{prettySourceCode10}</Text>
        <Text style={styles.titleStyle}>{"\n'indent_with_tabs': false"}</Text>
        <Text>{prettySourceCode11}</Text>
        <Text style={styles.titleStyle}>{"\n'eol': 换行符"}</Text>
        <Text>{prettySourceCode12}</Text>
        <Text style={styles.titleStyle}>{"\n'end_with_newline': false"}</Text>
        <Text>{prettySourceCode13}this use " end_with_newline": false,it can't change the line</Text>
        <Text style={styles.titleStyle}>{"\n'indent-inner-html': true"}</Text>
        <Text>{prettySourceCode14}</Text>
        <Text style={styles.titleStyle}>{"\n'preserve_newlines': true"}</Text>
        <Text>{prettySourceCode15}</Text>
        <Text style={styles.titleStyle}>
          {"\n'max_preserve_newlines': '2', 'preserve_newlines': true"}
        </Text>
        <Text>{prettySourceCode16}</Text>
        <Text style={styles.titleStyle}>{"\n'brace_style': collapse"}</Text>
        <Text>{prettySourceCode17}</Text>
        <Text style={styles.titleStyle}>{"\n'indent_scripts': normal"}</Text>
        <Text>{prettySourceCode18}</Text>
        <Text style={styles.titleStyle}>{"\n'wrap_line_length': 50"}</Text>
        <Text>{prettySourceCode19}</Text>
        <Text style={styles.titleStyle}>{'Original HTML:'}</Text>
        <Text>{sourceCode9}</Text>
        <Text style={styles.titleStyle}>{"\n'auto':"}</Text>
        <Text>{prettySourceCode20}</Text>
        <Text style={styles.titleStyle}>{"\n'force':"}</Text>
        <Text>{prettySourceCode21}</Text>
        <Text style={styles.titleStyle}>{"\n'force-aligned':"}</Text>
        <Text>{prettySourceCode22}</Text>
        <Text style={styles.titleStyle}>{"\n'force-expand-multiline':"}</Text>
        <Text>{prettySourceCode23}</Text>
        <Text style={styles.titleStyle}>
          {"\n'wrap_attributes_min_attrs':2"}
        </Text>
        <Text>{prettySourceCode24}</Text>
        <Text style={styles.titleStyle}>
          {"\n'wrap_attributes_min_attrs':6"}
        </Text>
        <Text>{prettySourceCode25}</Text>
        <Text style={styles.titleStyle}>
          {"\n'wrap_attributes_indent_size':5"}
        </Text>
        <Text>{prettySourceCode26}</Text>
        <Text style={styles.titleStyle}>{'Original HTML:'}</Text>
        <Text>{sourceCode10}</Text>
        <Text style={styles.titleStyle}>{"\n'inline': ['span']"}</Text>
        <Text>{prettySourceCode27}</Text>
        <Text style={styles.titleStyle}>{'Original HTML'}</Text>
        <Text>{sourceCode11}</Text>
        <Text style={styles.titleStyle}>
          {"\n'nline_custom_elements':true"}
        </Text>
        <Text>{prettySourceCode28}</Text>
        <Text style={styles.titleStyle}>{'Original HTML'}</Text>
        <Text>{sourceCode12}</Text>
        <Text style={styles.titleStyle}>
          {"\n''unformatted': ['span', 'b', 'i']"}
        </Text>
        <Text>{prettySourceCode29}</Text>
        <Text style={styles.titleStyle}>{'Original HTML'}</Text>
        <Text>{sourceCode13}</Text>
        <Text style={styles.titleStyle}>
          {"\n'content_unformatted': ['pre']"}
        </Text>
        <Text>{prettySourceCode30}</Text>
        <Text style={styles.titleStyle}>{'Original HTML'}</Text>
        <Text>{sourceCode14}</Text>
        <Text style={styles.titleStyle}>{"\n'extra_liners': ['p']"}</Text>
        <Text>{prettySourceCode31}</Text>
      </View>
    </ScrollView>
  );
}

const styles = StyleSheet.create({
  textStyle: {
    fontSize: 20,
    fontWeight: '600',
  },
  titleStyle: {
    fontSize: 16,
    fontWeight: '500',
  },
});

export default BeautifyDemo;
```

## Constraints

### Compatibility

1. RNOH：0.72.11; SDK：OpenHarmony(api11) 4.1.0.53; IDE：DevEco Studio 4.1.3.412; ROM：2.0.0.52;
2. RNOH：0.72.13; SDK：HarmonyOS NEXT Developer Preview1; IDE：DevEco Studio 4.1.3.500; ROM：2.0.0.59;
3. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;

## Static Methods

For details, see [js-beautify document](https://github.com/beautifier/js-beautify)

### js_beautify

The interface of the library is 'js_beautify', and different 'options' are passed in to implement the corresponding functions.

| Name        | Description                                                                                                    | Type     | Required | HarmonyOS Support |
| ----------- | -------------------------------------------------------------------------------------------------------------- | -------- | -------- | ----------------- |
| js_beautify | options need to be passed in；options is an object with the settings you would like used to beautify the code. | function | NO       | yes               |

### options

The following parameters are used for options, and if the corresponding attributes are not specified, the default values are as follows.

```
{
    "indent_size": 4,
    "indent_char": " ",
    "indent_with_tabs": false,
    "editorconfig": false,
    "eol": "\n",
    "end_with_newline": false,
    "indent_level": 0,
    "preserve_newlines": true,
    "max_preserve_newlines": 10,
    "space_in_paren": false,
    "space_in_empty_paren": false,
    "jslint_happy": false,
    "space_after_anon_function": false,
    "space_after_named_function": false,
    "brace_style": "collapse",
    "unindent_chained_methods": false,
    "break_chained_methods": false,
    "keep_array_indentation": false,
    "unescape_strings": false,
    "wrap_line_length": 0,
    "e4x": false,
    "comma_first": false,
    "operator_position": "before-newline",
    "indent_empty_lines": false,
    "templating": ["auto"]
}
```

## Known Issues

## License

This project is licensed under [The MIT License (MIT)](https://github.com/beautifier/js-beautify/blob/main/LICENSE).