> Template version: v0.2.0

<p align="center">
  <h1 align="center"> <code>Moment</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/moment/moment/blob/develop/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github address](https://github.com/moment/moment)

## Installation and Usage

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
npm install moment@2.30.1
```

#### **yarn**

```bash
yarn add moment@2.30.1
```

<!-- tabs:end -->

quick use:

```bash
import moment from 'moment';
moment().format();
```

Set the moment area:

```bash
// Import method
import 'moment/locale/zh-cn';
moment.locale('zh-cn');
```

## Constraints

## Compatibility

This document is verified based on the following versions:

1. RNOH: 0.72.20; SDK: HarmonyOS NEXT Developer Preview2; IDE: DevEco Studio 5.0.3.200; ROM: 205.0.0.18;

## APIs

For details, see the [Moment.js Documentation](https://momentjs.com/docs/#/use-it/).

The following **moment** is the object exported from **moment.js**:

```bash
import moment from 'moment';
```

The following code shows the basic use scenarios of the repository:

```js
// Obtain 00:00:00 today.
moment().startOf("day");
// Obtain 00:00:00 in the first day of the current month.
moment().startOf("month");
// Obtain the total number of days of the current month.
moment().daysInMonth();
// Obtain the timestamp (in seconds).
moment().format("X"); // The return value is of the string type.
moment().unix (); // The return value is of the numeric type.
// Obtain the timestamp (in milliseconds).
moment().format("x"); // The return value is of the string type.
moment().valueOf(); // The return value is of the numeric type.
// Obtain the year.
moment().year();
moment().get("year");
// Obtain the month.
moment().month(); // (0~11, 0: January, 11: December)
moment().get("month");
// Obtain a day in a week.
moment().date();
moment().get("date");
// Obtain the hour.
moment().hours();
moment().get("hours");
// Obtain the minute.
moment().minutes();
moment().get("minutes");
// Obtain the current year, month, day, hour, minute, second, and millisecond.
moment().toArray(); // [years, months, date, hours, minutes, seconds, milliseconds]
moment().toObject(); // {years: xxxx, months: x, date: xx ...}

// Set the year.
moment().year(2019);
moment().set("year", 2019);
moment().set({ year: 2019 });
// Set the month.
moment().month(11); // (0~11, 0: January, 11: December)
moment().set("month", 11);
// Set a day in a month.
moment().date(15);
moment().set("date", 15);
// Set a day in a week.
moment().weekday(0); // Set the date to the first day (Sunday) of this week.
moment().isoWeekday(1); // Set the date to Monday of this week.
moment().set("weekday", 0);
moment().set("isoWeekday", 1);
// Set the hour.
moment().hours(12);
moment().set("hours", 12);
// Plus one year base on this year.
moment().add(1, "years");
moment().add({ years: 1 });

// Obtain the time difference between two dates.
let start_date = moment().subtract(1, "weeks");
let end_date = moment();
end_date.diff(start_date); // Return the number of milliseconds.
end_date.diff(start_date, "months"); // 0
end_date.diff(start_date, "weeks"); // 1
end_date.diff(start_date, "days"); // 7
start_date.diff(end_date, "days"); // -7
// Convert the moment object to a native JavaScript Date object.
moment().toDate();
new Date(moment());

// Set the year, month, and day to the "MM DD, YYYY" format.
moment().format("MM DD, YYYY");
// Set the year, month, and day to the "YYYY-MM-DD" format.
moment().format("YYYY-MM-DD");
// Set the hour, minute, and second to the 24-hour clock format.
moment().format("HH:mm:ss");
// Set the hour, minute, and second to the 12-hour clock format.
moment().format("hh:mm:ss a");
```

The following shows the verified APIs:

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

#### **Get + Set**

| Name          | Description                                                  | Type     | Required | HarmonyOS Support |
| ------------- | ------------------------------------------------------------ | -------- | -------- | ----------------- |
| millisecond   | Gets or sets the milliseconds.                               | function | no       | yes               |
| second        | Gets or sets the seconds.                                    | function | no       | yes               |
| minute        | Gets or sets the minutes.                                    | function | no       | yes               |
| hour          | Gets or sets the hour.                                       | function | no       | yes               |
| date          | Gets or sets the day of the month                            | function | no       | yes               |
| day           | Gets or sets the day of the week.                            | function | no       | yes               |
| weekday       | Gets or sets the day of the week according to the locale.    | function | no       | yes               |
| isoWeekday    | Gets or sets the ISO day of the week with 1 being Monday and 7 being Sunday. | function | no       | yes               |
| dayOfYear     | Gets or sets the day of the year.                            | function | no       | yes               |
| week          | Gets or sets the week of the year.                           | function | no       | yes               |
| isoWeek       | Gets or sets the ISO week of the year.                       | function | no       | yes               |
| month         | Gets or sets the month.                                      | function | no       | yes               |
| quarter       | Gets the quarter (1 to 4).                                   | function | no       | yes               |
| year          | Gets or sets the year.                                       | function | no       | yes               |
| weekYear      | Gets or sets the week-year according to the locale.          | function | no       | yes               |
| isoWeekYear   | Gets or sets the ISO week-year.                              | function | no       | yes               |
| weeksInYear   | Gets the number of weeks according to locale in the current moment's year. | function | no       | yes               |
| isoWeeksInYea | Gets the number of weeks in the current moment's year, according to ISO weeks. | function | no       | yes               |
| get           | String getter. In general <br> Units are case insensitive, and support plural and short forms: year (years, y), month (months, M), date (dates, D), hour (hours, h), minute (minutes, m), second (seconds, s), millisecond (milliseconds, ms). | function | no       | yes               |
| set           | Generic setter, accepting unit as first argument, and value as second: <br> Units are case insensitive, and support plural and short forms: year (years, y), month (months, M), date (dates, D), hour (hours, h), minute (minutes, m), second (seconds, s), millisecond (milliseconds, ms). | function | no       | yes               |

#### **Manipulate**

| Name      | Description                                                  | Type     | Required | HarmonyOS Support |
| --------- | ------------------------------------------------------------ | -------- | -------- | ----------------- |
| add       | Mutates the original moment by adding time.                  | function | no       | yes               |
| subtract  | Mutates the original moment by subtracting time.             | function | no       | yes               |
| startOf   | Mutates the original moment by setting it to the start of a unit of time. | function | no       | yes               |
| endOf     | Mutates the original moment by setting it to the end of a unit of time. | function | no       | yes               |
| local     | Sets a flag on the original moment to use local time to display a moment instead of the original moment's time. | function | no       | yes               |
| utc       | Sets a flag on the original moment to use UTC to display a moment instead of the original moment's time. | function | no       | yes               |
| utcOffset | Get or set the UTC offset in minutes.                        | function | no       | yes               |

#### **Display**

| Name        | Description                                                  | Type     | Required | HarmonyOS Support |
| ----------- | ------------------------------------------------------------ | -------- | -------- | ----------------- |
| format      | This is the most robust display option. It takes a string of tokens and replaces them with their corresponding values. | function | no       | yes               |
| fromNow     | A common way of displaying time is handled by moment#fromNow. This is sometimes called timeago or relative time. | function | no       | yes               |
| from        | You may want to display a moment in relation to a time other than now. In that case, you can use moment#from. | function | no       | yes               |
| toNow       | A common way of displaying time is handled by moment#toNow. This is sometimes called timeago or relative time. | function | no       | yes               |
| to          | You may want to display a moment in relation to a time other than now. In that case, you can use moment#to. | function | no       | yes               |
| calendar    | Calendar time displays time relative to a given referenceDay (defaults to the start of today), but does so slightly differently than moment#fromNow. | function | no       | yes               |
| diff        | To get the difference in milliseconds, use moment#diff like you would use moment#from. | function | no       | yes               |
| valueOf     | moment#valueOf simply outputs the number of milliseconds since the Unix Epoch, just like Date#valueOf. | function | no       | yes               |
| unix        | moment#unix outputs a Unix timestamp (the number of seconds since the Unix Epoch). | function | no       | yes               |
| daysInMonth | Get the number of days in the current month.                 | function | no       | yes               |
| toDate      | To get a copy of the native Date object that Moment.js wraps, use moment#toDate. | function | no       | yes               |
| toArray     | This returns an array that mirrors the parameters from new Date(). | function | no       | yes               |
| toJSON      | When serializing an object to JSON, if there is a Moment object, it will be represented as an ISO8601 string, adjusted to UTC. | function | no       | yes               |
| toISOString | Formats a string to the ISO8601 standard.                    | function | no       | yes               |
| toObject    | This returns an object containing year, month, day-of-month, hour, minute, seconds, milliseconds. | function | no       | yes               |
| toString    | Returns an english string in a similar format to JS Date's .toString(). | function | no       | yes               |
| inspect     | Returns a machine readable string, that can be evaluated to produce the same moment. Because of the name it is also used in node interactive shell to display objects. | function | no       | yes               |

#### **Query**

| Name           | Description                                                  | Type     | Required | HarmonyOS Support |
| -------------- | ------------------------------------------------------------ | -------- | -------- | ----------------- |
| isBefore       | Check if a moment is before another moment. The first argument will be parsed as a moment, if not already so. | function | no       | yes               |
| isSame         | Check if a moment is the same as another moment. The first argument will be parsed as a moment, if not already so. | function | no       | yes               |
| isAfter        | Check if a moment is after another moment. The first argument will be parsed as a moment, if not already so. | function | no       | yes               |
| isSameOrBefore | Check if a moment is before or the same as another moment. The first argument will be parsed as a moment, if not already so. | function | no       | yes               |
| isSameOrAfter  | Check if a moment is after or the same as another moment. The first argument will be parsed as a moment, if not already so. | function | no       | yes               |
| isBetween      | Check if a moment is between two other moments, optionally looking at unit scale (minutes, hours, days, etc). | function | no       | yes               |
| isDST          | moment#isDST checks if the current moment is in daylight saving time. | function | no       | yes               |
| isLeapYear     | moment#isLeapYear returns true if that year is a leap year, and false if it is not. | function | no       | yes               |
| isMoment       | To check if a variable is a moment object, use moment.isMoment(). | function | no       | yes               |
| isDate         | To check if a variable is a native js Date object, use moment.isDate(). | function | no       | yes               |

#### **Durations**

| Name     | Description                                                  | Type     | Required | HarmonyOS Support |
| -------- | ------------------------------------------------------------ | -------- | -------- | ----------------- |
| duration | To create a duration, call moment.duration() with the length of time in milliseconds. | function | no       | yes               |

#### **Formatted time**

| **Format Code** | **Description**                                              | **Return Value**                                             |
| --------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| M               | Month represented by a number, without a leading zero.       | The value ranges from 1 to 12.                               |
| MM              | Month represented by a number, with a leading zero.          | The value ranges from 01 to 12.                              |
| MMM             | Month represented by a three-letter abbreviation.            | The value ranges from Jan to Dec.                            |
| MMMM            | Month, in its full name.                                     | January to December.                                         |
| Q               | Quarter.                                                     | The value ranges from 1 to 4.                                |
| D               | Day of the month, without a leading zero.                    | The value ranges from 1 to 31.                               |
| DD              | Day of the month, with a leading zero.                       | The value ranges from 01 to 31.                              |
| d               | Day of the week, represented by a number.                    | The value ranges from 0 to 6. The value **0** indicates Sunday, and **6** indicates Saturday. |
| ddd             | Day of the week, represented by a three-letter abbreviation. | The value ranges from Sun to Sat.                            |
| dddd            | Day of the week, in its full name.                           | The value ranges from Sunday to Saturday.                    |
| w               | Week of a year.                                              | For example, **42** indicates the 42nd week.                 |
| YYYY            | Year represented by four digits.                             | For example, **2014** or **2000**.                           |
| YY              | Year represented by two digits.                              | For example, **14** or **98**.                               |
| A               | Uppercase of the time units.                                 | AM or PM.                                                    |
| a               | Lowercase of the time units.                                 | am or pm.                                                    |
| HH              | Hour, in 24-hour clock, with a leading zero.                 | The value ranges from 00 to 23.                              |
| H               | Hour, in 24-hour clock, without a leading zero.              | The value ranges from 0 to 23.                               |
| hh              | Hour, in 12-hour clock, with a leading zero.                 | The value ranges from 00 to 12.                              |
| h               | Hour, in 12-hour clock, without a leading zero.              | The value ranges from 0 to 12.                               |
| m               | Minute, without a leading zero.                              | The value ranges from 0 to 59.                               |
| mm              | Minute, with a leading zero.                                 | The value ranges from 00 to 59.                              |
| s               | Second, without a leading zero.                              | The value ranges from 1 to 59.                               |
| ss              | Second, with a leading zero.                                 | The value ranges from 01 to 59.                              |
| X               | Unix timestamp.                                              | For example, **1411572969**.                                 |

## Others

## License