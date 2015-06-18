php-date-formatter
==================

[![BOWER version](https://badge-me.herokuapp.com/api/bower/kartik-v/php-date-formatter.png)](http://badges.enytc.com/for/bower/kartik-v/php-date-formatter)
[![Latest Stable Version](https://poser.pugx.org/kartik-v/php-date-formatter/v/stable)](https://packagist.org/packages/kartik-v/php-date-formatter)
[![License](https://poser.pugx.org/kartik-v/php-date-formatter/license)](https://packagist.org/packages/kartik-v/php-date-formatter)
[![Packagist Downloads](https://poser.pugx.org/kartik-v/php-date-formatter/downloads)](https://packagist.org/packages/kartik-v/php-date-formatter)
[![Monthly Downloads](https://poser.pugx.org/kartik-v/php-date-formatter/d/monthly)](https://packagist.org/packages/kartik-v/php-date-formatter)

A JQuery datetime library that allows you to manipulate date/times using PHP date-time formats in javascript. This library was built with an intention 
to read and write date/timestamps to the database easily when working with PHP server code. Use cases for this library would involve reading and saving a 
timestamp to database in one format, but displaying it on client or html forms in another format. Maintaining a consistent PHP Date time format for both 
server side and client side validation should help in building extensible applications with various PHP frameworks easily.

The latest release of the library is v1.3.1. Check the [CHANGE LOG](https://github.com/kartik-v/php-date-formatter/blob/master/CHANGE.md) for details.

## Features

- Parse date/time strings or a Date object, and convert it into Javascript Date Object by passing any of the [PHP DateTime formats](http://php.net/manual/en/function.date.php).
- Automatically guess date/time strings, even if it does not exactly match the format, and convert it into Javascript Date Object.
- Read date/time strings or a Date object, and format it as per a [PHP DateTime format](http://php.net/manual/en/function.date.php).
- Size of the entire library is less than 2KB when gzipped, or < 6KB, when minified.

## Demo

View the [library documentation](http://plugins.krajee.com/php-date-formatter) and
[library demos](http://plugins.krajee.com/php-date-formatter/demo) at Krajee JQuery plugins.

## Pre-requisites

1. Latest [JQuery](http://jquery.com/)

## Installation

### Using Bower
You can use the `bower` package manager to install. Run:

    bower install php-date-formatter

### Using Composer
You can use the `composer` package manager to install. Either run:

    $ php composer.phar require kartik-v/php-date-formatter "@dev"

or add:

    "kartik-v/php-date-formatter": "@dev"

to your composer.json file

### Manual Install

You can also manually install the plugin easily to your project. Just download the source
[ZIP](https://github.com/kartik-v/php-date-formatter/zipball/master) or
[TAR ball](https://github.com/kartik-v/php-date-formatter/tarball/master) and extract the
plugin assets (css and js folders) into your project.

## Usage

**Step 1** Load the following assets in your header.

```html
<script src="//ajax.googleapis.com/ajax/libs/jquery/1.11.0/jquery.min.js"></script>
<script src="path/to/js/php-date-formatter.min.js" type="text/javascript"></script>
```

If you noticed, you need to load the `jquery.min.js` in addition to the `php-date-formatter.min.js` for the plugin to work with default settings.

**Step 2** You can now access the library using the `DateFormatter` object. For example, you can convert any date string to javascript date object for a specific PHP date format.

```js
var fmt = new DateFormatter();
var d1 = fmt.DateFormatter.parseDate('23-Sep-2013 09:24:12', 'd-M-Y H:i:s');
```

### DateFormatter Methods
The **php-date-formatter** library supports these methods:

#### parseDate
This method allows you to convert any date string or date object to a javascript Date object for a specific PHP date format. This method takes in the following properties:

- `vDate`: Input date. Must be _string_ or a javascript _Date_ object.
- `vFormat`: The [PHP DateTime format](http://php.net/manual/en/function.date.php), used for parsing the date.

**Example:**

```js
var fmt = new DateFormatter();
var d1 = fmt.parseDate('23-Sep-2013 09:24:12', 'd-M-Y H:i:s');
// d1 will return Javascript date object for your timezone
alert(d1); // will return: Mon Sep 23 2013 09:24:12 GMT+0530 (India Standard Time)
```

#### guessDate
This method allows you to intelligently guess the date by closely matching the specific format. You can guess a date for any date string or date object to return a javascript Date object. This method takes in the following properties:

- `vDate`: Input date. Must be _string_ or a javascript _Date_ object.
- `vFormat`: The [PHP DateTime format](http://php.net/manual/en/function.date.php), used for guessing the date.

**Example:**

```js
// note the passed string and the PHP date-time format differ
var fmt = new DateFormatter();
var d1 = fmt.guessDate('23-09-13 09:24:12', 'd-M-Y H:i:s'); 
// d1 will again return Javascript date object for your timezone
alert(d1); // will return: Mon Sep 23 2013 09:24:12 GMT+0530 (India Standard Time)
```

#### formatDate
This method allows you to return a formatted date string using a specific PHP datetime format. You can format a date for any date string or date object to return a javascript Date object. This method takes in the following properties:

- `vDate`: Input date. Must be _string_ or a javascript _Date_ object.
- `vFormat`: The [PHP DateTime format](http://php.net/manual/en/function.date.php), used for formatting the date.

```js
var d1 = new Date();
var fmt = new DateFormatter();
var d2 = fmt.formatDate(d1, 'd-M-Y H:i:s');
alert(d2); // will return: 23-Sep-2013 09:24:12
```

### DateFormatter Options

You can control the following options/settings for DateFormatter. 

#### dateSettings
This property allows you to configure the terms used for short/long days and months, and the meridiem. This is defaulted to:

```js
{
    longDays: ['Sunday', 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday'],
    shortDays: ['Sun', 'Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat'],
    shortMonths: ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec'],
    longMonths: ['January', 'February', 'March', 'April', 'May', 'June',
        'July', 'August', 'September', 'October', 'November', 'December'],
    meridiem: ['AM', 'PM']
}
```

You can override these settings for your language, as shown in the example below:

```js
var fmt = new DateFormatter({
    dateSettings: {
        longMonths: ['janvier', 'février', 'mars', 'avril', 'mai', 'juin', 
            'juillet', 'août', 'septembre', 'octobre', 'novembre', 'décembre']
    }
});
```

#### separators
This property defines all the separators that are possible in the date string. This defaults to `/[ \-+\/\.T:@]/g`.

#### validParts
This property defines all the valid format patterns that are possible in the date string. This defaults to `/[djDlwSFmMnyYaAgGhHisU]/g`.

## License

**php-date-formatter** is released under the BSD 3-Clause License. See the bundled `LICENSE.md` for details.