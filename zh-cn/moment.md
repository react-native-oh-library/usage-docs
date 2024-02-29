> 模板版本：v0.1.3

<p align="center">
  <h1 align="center"> <code>Moment</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/moment/moment/blob/develop/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!tip] [Github 地址](https://github.com/moment/moment)

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install moment
```

#### **yarn**

```bash
yarn add moment
```

<!-- tabs:end -->

快速使用：

```bash
import moment from 'moment';
moment().format();
```

设定moment区域：

```bash
// import 方式
import 'moment/locale/zh-cn';
moment.locale('zh-cn');
```

## 约束与限制

## 兼容性

本文档内容基于以下版本验证通过：

1. RNOH：0.72.13; SDK：HarmonyOS NEXT Developer Preview1; IDE：DevEco Studio 4.1.3.500; ROM：2.0.0.59;

## API

详情查看[moment官方文档](https://momentjs.com/docs/#/use-it/)

以下moment为moment.js导出的对象，即：

```bash
import moment from 'moment';
```

如下是已验证接口展示:

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

#### **Get + Set**
| Name | Description | Type | Required | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | ------------------ |
| millisecond  | 获取或设置毫秒 | function  | no | yes |
| second |获取或设置秒 | function | no | yes |
| minute | 获取或设置分钟 | function | no | yes |
| hour | 获取或设置小时 | function | no | yes |
| date | 获取或设置一月中的某一天 | function | no | yes |
| day | 获取或设置星期几 | function | no | yes |
| weekday | 根据区域设置获取或设置星期几 | function | no | yes |
| isoWeekday | 获取或设置[ISO 星期几](https://en.wikipedia.org/wiki/ISO_week_date)，其中`1`星期一和`7`星期日 | function | no | yes |
| dayOfYear | 获取或设置一年中的第几天 | function | no | yes |
| week | 获取或设置一年中的第几周 | function | no | yes |
| isoWeek | 获取或设置 [一年中的 ISO 周](https://en.wikipedia.org/wiki/ISO_week_date) | function | no | yes |
| month | 获取或设置月份 | function | no | yes |
| quarter | 获取季度（1 到 4） | function | no | yes |
| year | 获取或设置年份 | function | no | yes |
| weekYear | 根据区域设置获取或设置周年 | function | no | yes |
| isoWeekYear | 获取或设置 [ISO 周年](https://en.wikipedia.org/wiki/ISO_week_date) | function | no | yes |
| weeksInYear | 根据当前 moment 所在年份的区域设置获取周数 | function | no | yes |
| isoWeeksInYea | 根据 [周数](https://en.wikipedia.org/wiki/ISO_week_date)，获取当前 moment 所在年份的周数 | function | no | yes |
| get | 获取时间或日期 | function | no | yes |
| set | 设置时间或日期 | function | no | yes |

#### **Manipulate**
| Name | Description | Type | Required | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | ------------------ |
| add | 添加时间来改变原始 moment | function | no | yes |
| subtract | 减去时间来改变原始 moment | function | no | yes |
| startOf | 设置时间开端 | function | no | yes |
| endOf | 设置时间终端 | function | no | yes |
| local | 设置标志显示本地时间 | function | no | yes |
| utc | 设置标志以使用UTC显示时间 | function | no | yes |
| utcOffset | 以分钟为单位获取或设置 UTC 偏移量 | function | no | yes |

#### **Display**
| Name | Description | Type | Required | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | ------------------ |
| format | 格式化日期或时间 | function | no | yes |
| fromNow | 从此刻到过去的时间 | function | no | yes |
| from | 从X到过去的时间 | function | no | yes |
| toNow | 从此刻到未来的时间 | function | no | yes |
| to | 从X到未来的时间 | function | no | yes |
| calendar | 日历时间（默认为今天的开始 | function | no | yes |
| diff | 时间差（获得以毫秒为单位的时间差 | function | no | yes |
| valueOf | Unix时间戳（毫秒） | function | no | yes |
| unix | Unix时间戳（秒） | function | no | yes |
| daysInMonth | 获取当月的天数 | function | no | yes |
| toDate | 获取 Moment.js作为JavaScript日期对象 | function | no | yes |
| toArray | 作为数组（返回一个数组，该数组反映了 `new Date()` 中的参数） | function | no | yes |
| toJSON | 将对象序列化为 JSON 时，如果有 `Moment` 对象，将表示为 ISO8601 字符串，调整为 UTC | function | no | yes |
| toISOString | 将字符串格式化为 ISO8601 标准 | function | no | yes |   
| toObject | 返回一个包含年、月、月中某日、小时、分钟、秒、毫秒的对象 | function | no | yes |
| toString | 返回一个英语字符串，格式与 JS Date 的 `.toString()` 类似 | function | no | yes |
| inspect | 返回一个机器可读的字符串，可以对其进行评估以产生相同的 moment | function | no | yes |

#### **Query**
| Name | Description | Type | Required | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | ------------------ |
| isBefore | 检查一个 moment 是否在另一个 moment 之前 | function | no | yes |
| isSame | 检查一个 moment 是否与另一个 moment 相同 | function | no | yes |
| isAfter | 检查一个 moment 是否在另一个 moment 之后 | function | no | yes |
| isSameOrBefore | 检查一个 moment 是否在另一个 moment 之前或与另一个 moment 相同 | function | no | yes |
| isSameOrAfter | 检查一个 moment 是否在另一个 moment 之后或与另一个 moment 相同 | function | no | yes |
| isBetween | 检查某个 moment 是否位于其他两个 moment 之间，可以选择查看单位尺度（分钟、小时、天等） | function | no | yes |
| isDST | 检查当前 moment 是否处于夏令时 | function | no | yes |
| isLeapYear | 判断是否为闰年 | function | no | yes |
| isMoment | 检查变量是否为 moment 对象 | function | no | yes |
| isDate | 检查变量是否为原生 js Date 对象 | function | no | yes |

#### **Durations**
| Name | Description | Type | Required | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | ------------------ |
| duration | 创建持续时间，请使用以毫秒为单位的时间长度调用 | function | no | yes |

下面的代码展示了这个库的基本使用示例：

#### **获取时间**

获取今天0时0分0秒

```bash
moment().startOf('day');
```

获取当前月第一天0时0分0秒

```bash
moment().startOf('month');
```

获取当前月的总天数

```bash
moment().daysInMonth();
```

获取时间戳(以秒为单位)

```bash
moment().format('X'); // 返回值为字符串类型
moment().unix(); // 返回值为数值型
```

获取时间戳(以毫秒为单位)

```bash
moment().format('x'); // 返回值为字符串类型
moment().valueOf(); // 返回值为数值型
```

获取年份

```bash
moment().year();
moment().get('year');
```

获取月份

```bash
moment().month();  // (0~11, 0: January, 11: December)
moment().get('month');
```

获取一个星期中的某一天

```bash
moment().date();
moment().get('date');
```

获取小时

```bash
moment().hours();
moment().get('hours');
```

获取分钟

```bash
moment().minutes();
moment().get('minutes');
```

获取当前的年月日时分秒

```bash
moment().toArray();  // [years, months, date, hours, minutes, seconds, milliseconds]
moment().toObject(); // {years: xxxx, months: x, date: xx ...}
```

#### **设置时间**

设置年份

```bash
moment().year(2019);
moment().set('year', 2019);
moment().set({year: 2019});
```

设置月份

```bash
moment().month(11);  // (0~11, 0: January, 11: December)
moment().set('month', 11); 
```

设置某个月中的某一天

```bash
moment().date(15);
moment().set('date', 15);
```

设置某个星期中的某一天

```bash
moment().weekday(0); // 设置日期为本周第一天（周日）
moment().isoWeekday(1); // 设置日期为本周周一
moment().set('weekday', 0);
moment().set('isoWeekday', 1);
```

设置小时

```bash
moment().hours(12);
moment().set('hours', 12);
```

年份+1

```bash
moment().add(1, 'years');
moment().add({years: 1});
```

#### **格式化时间**

| **格式代码** | **说明** | **返回值例子** | 
| ---- | ----------- | ---- | 
| M  | 数字表示的月份，没有前导零 | 1到12  |
| MM | 数字表示的月份，有前导零 | 01到12 |
| MMM | 三个字母缩写表示的月份 | Jan到Dec |
| MMMM | 月份，完整的文本格式 | January到December |
| Q | 季度 | 1到4 |
| D | 月份中的第几天，没有前导零 | 1到31  |
| DD | 月份中的第几天，有前导零  | 01到31  |
| d | 星期中的第几天，数字表示   | 0到6，0表示周日，6表示周六 |
| ddd | 三个字母表示星期中的第几天 | Sun到Sat  |
| dddd | 星期几，完整的星期文本 | 从Sunday到Saturday |
| w | 年份中的第几周  | 如42：表示第42周 |
| YYYY | 四位数字完整表示的年份 | 如：2014 或 2000 |
| YY | 两位数字表示的年份 | 如：14 或 98 |
| A | 大写的AM PM  | AM PM |
| a | 小写的am pm  | am pm |
| HH | 小时，24小时制，有前导零 | 00到23 |
| H | 小时，24小时制，无前导零  | 0到23 |
| hh | 小时，12小时制，有前导零 | 00到12 |
| h | 小时，12小时制，无前导零  | 0到12 |
| m | 没有前导零的分钟数  | 0到59 |
| mm | 有前导零的分钟数 | 00到59 |
| s | 没有前导零的秒数 | 1到59 |
| ss | 有前导零的描述  | 01到59 |
| X | Unix时间戳 | 1411572969 |

格式化年月日： 'xxxx年xx月xx日'

```bash
moment().format('YYYY年MM月DD日');
```

格式化年月日： 'xxxx-xx-xx'

```bash
moment().format('YYYY-MM-DD');
```

格式化时分秒(24小时制)： 'xx时xx分xx秒'

```bash
moment().format('HH时mm分ss秒');
```

格式化时分秒(12小时制)：'xx:xx:xx am/pm'

```bash
moment().format('hh:mm:ss a');
```

#### **比较时间**

获取两个日期之间的时间差

```bash
let start_date = moment().subtract(1, 'weeks');
let end_date = moment();

end_date.diff(start_date); // 返回毫秒数

end_date.diff(start_date, 'months'); // 0
end_date.diff(start_date, 'weeks'); // 1
end_date.diff(start_date, 'days'); // 7
start_date.diff(end_date, 'days'); // -7
```

转化为JavaScript原生Date对象

```bash
moment().toDate();
new Date(moment());
```

## 其他

## 开源协议