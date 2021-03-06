# Format

[![Build Status](https://travis-ci.org/matriphe/format.svg?branch=master)](https://travis-ci.org/matriphe/format)
[![Latest Stable Version](https://poser.pugx.org/matriphe/format/v/stable.svg)](https://packagist.org/packages/matriphe/format)
[![Total Downloads](https://poser.pugx.org/matriphe/format/downloads.svg)](https://packagist.org/packages/matriphe/format) 
[![License](https://poser.pugx.org/matriphe/format/license.svg)](https://packagist.org/packages/matriphe/format)

Helpers contains common formatting, such as number, bytes, phone, simple hash slug, format duration, and remove new line in string. Very handy for formatting things in Laravel.

## Compatibility

Works with Laravel 5.1, Laravel 5.0, and Laravel 4.2.

## Installation

Open `composer.json` and require this line below.
```json
"matriphe/format": "~1.6"
```
Or you can run this command from your project directory.
```bash
composer require matriphe/format
```

### Laravel Installation

#### Laravel 5.1

Open the `config/app.php` and add this line in `providers` section.
```php
Matriphe\Format\FormatServiceProvider::class,
```
Still in `config/app.php`, add this line in `alias` section.
```php
'Format' => Matriphe\Format\Facades\FormatFacade::class,
```

#### Laravel 5.0

Open the `config/app.php` and add this line in `providers` section.
```php
'Matriphe\Format\FormatServiceProvider',
```
Still in `config/app.php`, add this line in `alias` section.
```php
'Format' => 'Matriphe\Format\Facades\FormatFacade',
```

#### Laravel 4.2

Open the `app/config/app.php` and add this line in `providers` section.
```php
'Matriphe\Format\FormatServiceProvider',
```
Still in `app/config/app.php`, add this line in `alias` section.
```php
'Format' => 'Matriphe\Format\Facades\FormatFacade',
```

## Usage

It's really easy to use the functions, by calling the `Format` facade or simply using global functions helpers.

### Format Number
```php
// Using facade
// (string) Format::number((float) $number, (int) $precision = 0, (string) $decimal = ',', (string) $thousand = '.')
Format::number(1000); // output: '1.000'
Format::number(123456.76,1); // output: '123.456,8'
Format::number(123456.76,1, ",", "."); // output: '123,456.8'

// Using global function
// (string) format_number((float) $number, (int) $precision = 0, (string) $decimal = ',', (string) $thousand = '.')
format_number(1000); // output: '1.000'
format_number(123456.76,1); // output: '123.456,8'
format_number(123456.76,1, ",", "."); // output: '123,456.8'

```

### Format Bytes
```php
// Using facade
// (string) Format::bytes((float) $number, (int) $precision = 1)
Format::bytes(100); // output: '100 B'
Format::bytes(1000); // output: '1,0 kB'
Format::bytes(2000000000,0); // output: '2 GB'

// Using global function
// (string) format_bytes((float) $number, (int) $precision = 1)
format_bytes(100); // output: '100 B'
format_bytes(1000); // output: '1,0 kB'
format_bytes(2000000000,0); // output: '2 GB'
```

### Format to Bytes
```php
// Using facade
// (int) Format::toBytes((string) $stringBytes)
Format::toBytes('10k'); // output: 10240
Format::toBytes('10 M'); // output: 10485760
Format::toBytes('10G'); // output: 10737418240

// Using global function
// (int) format_to_bytes((string) $stringBytes)
format_to_bytes('10k'); // output: 10240
format_to_bytes('10 M'); // output: 10485760
format_to_bytes('10G'); // output: 10737418240
```

### Format Phone
```php
// Using facade
// (string) Format::phone((string) $phone)
Format::phone('085786920412'); // output: +6285786920412
Format::phone('+6285786920412'); // output: +6285786920412
Format::phone('(0274) 513-339'); // output: +62274513339
Format::phone('3-7801 2611','+60'); // output: +60378012611

// Using global function
// (string) format_phone((string) $phone)
format_phone('085786920412'); // output: +6285786920412
format_phone('+6285786920412'); // output: +6285786920412
format_phone('(0274) 513-339'); // output: +62274513339
format_phone('3-7801 2611','+60'); // output: +60378012611
```

### Format DateRange
```php
// Using facade
// (string) Format::dateRange((string) $date1, (string) $date2, (bool) $long)
Format::dateRange('2015-03-03'); // output: 3 March 2015
Format::dateRange('2015-03-03', null,false); // output: 3 Mar 15
Format::dateRange('2015-03-03', '2015-03-03'); // output: 3 March 2015
Format::dateRange('2015-03-03', '2015-03-03',false); // output: 3 Mar 15
Format::dateRange('2015-03-03', '2015-03-05'); // output: 3-5 March 2015
Format::dateRange('2015-03-03', '2015-03-05',false); // output: 3-5 Mar 15
Format::dateRange('2015-03-03', '2015-04-05'); // output: 3 March - 5 April 2015
Format::dateRange('2015-03-03', '2015-04-05',false); // output: 3 Mar - 5 Apr 15
Format::dateRange('2015-03-03', '2016-04-05'); // output: 3 March 2015 - 5 April 2016
Format::dateRange('2015-03-03', '2016-04-05',false); // output: 3 Mar 15 - 5 Apr 16

// Using global function
// (string) format_date_range((string) $date1, (string) $date2, (bool) $long)
format_date_range('2015-03-03'); // output: 3 March 2015
format_date_range('2015-03-03', null,false); // output: 3 Mar 15
format_date_range('2015-03-03', '2015-03-03'); // output: 3 March 2015
format_date_range('2015-03-03', '2015-03-03',false); // output: 3 Mar 15
format_date_range('2015-03-03', '2015-03-05'); // output: 3-5 March 2015
format_date_range('2015-03-03', '2015-03-05',false); // output: 3-5 Mar 15
format_date_range('2015-03-03', '2015-04-05'); // output: 3 March - 5 April 2015
format_date_range('2015-03-03', '2015-04-05',false); // output: 3 Mar - 5 Apr 15
format_date_range('2015-03-03', '2016-04-05'); // output: 3 March 2015 - 5 April 2016
format_date_range('2015-03-03', '2016-04-05',false); // output: 3 Mar 15 - 5 Apr 16
```

### Format Hashed Slug

It's very useful to generate *hashed* URL slug like in URL shortener service. It use UNIX timestamp salt to generate unique ID.
```php
// Using facade
// (string) Format::slugHash((int) $int, (int) $salt)
Format::slugHash(1); // output: zqzbQ8
Format::slugHash(2); // output: aqzbQ8
Format::slugHash(3); // output: qqzbQ8
Format::slugHash(1, strtotime('1984-03-22')); // output: 6O_IoS
Format::slugHash(2, strtotime('1984-03-22')); // output: YO_IoS
Format::slugHash(3, strtotime('1984-03-22')); // output: HO_IoS
Format::slugHash(1, strtotime('1986-10-03')); // output: 4XBzGc
Format::slugHash(2, strtotime('1986-10-03')); // output: RXBzGc
Format::slugHash(3, strtotime('1986-10-03')); // output: FXBzGc

// Using global function
// (string) format_slug_hash((int) $int, (int) $salt)
format_slug_hash(1); // output: zqzbQ8
format_slug_hash(2); // output: aqzbQ8
format_slug_hash(3); // output: qqzbQ8
format_slug_hash(1, strtotime('1984-03-22')); // output: 6O_IoS
format_slug_hash(2, strtotime('1984-03-22')); // output: YO_IoS
format_slug_hash(3, strtotime('1984-03-22')); // output: HO_IoS
format_slug_hash(1, strtotime('1986-10-03')); // output: 4XBzGc
format_slug_hash(2, strtotime('1986-10-03')); // output: RXBzGc
format_slug_hash(3, strtotime('1986-10-03')); // output: FXBzGc
```

#### Note for *hashed* slug
If you want to save this hashed slug into MySQL, make sure the column is case sensitive. To do this, alter the column with this command.
```sql
ALTER TABLE `table` CHANGE `column_slug` `column_slug` VARCHAR(50) BINARY NOT NULL;
```

### Format Duration

It's very useful to generate duration in days, hours, minutes, and seconds.
```php
// Using facade
// (string) Format::duration((string) $date1, (string) $date2, (boolean) $show_second)
Format::duration('2015-05-15 11:22:22', '2015-05-16 11:22:22'); // output: 1 day
Format::duration('2015-05-15 11:22:22', '2015-05-17 11:22:22'); // output: 2 days
Format::duration('2015-05-15 11:22:22', '2015-05-16 12:22:22'); // output: 1 day 1 hour
Format::duration('2015-05-15 11:22:22', '2015-05-16 13:22:22'); // output: 1 day 2 hours
Format::duration('2015-05-15 11:22:22', '2015-05-17 12:22:22'); // output: 2 days 1 hour
Format::duration('2015-05-15 11:22:22', '2015-05-17 13:22:22'); // output: 2 days 2 hours
Format::duration('2015-05-15 11:22:22', '2015-05-16 12:23:22'); // output: 1 day 1 hour 1 minute
Format::duration('2015-05-15 11:22:22', '2015-05-16 12:24:22'); // output: 1 day 1 hour 2 minutes
Format::duration('2015-05-15 11:22:22', '2015-05-16 13:23:22'); // output: 1 day 2 hours 1 minute
Format::duration('2015-05-15 11:22:22', '2015-05-16 11:23:22'); // output: 1 day 1 minute
Format::duration('2015-05-15 11:22:22', '2015-05-16 11:24:22'); // output: 1 day 2 minutes
Format::duration('2015-05-15 11:22:22', '2015-05-17 11:24:22'); // output: 2 days 2 minutes
Format::duration('2015-05-15 11:22:22', '2015-05-16 13:23:25'); // output: 1 day 2 hours 1 minute
Format::duration('2015-05-15 11:22:22', '2015-05-16 11:22:25'); // output: 1 day
Format::duration('2015-05-15 11:22:22', '2015-05-15 11:22:23'); // output: 1 second
Format::duration('2015-05-15 11:22:22', '2015-05-15 11:22:27'); // output: 5 seconds
Format::duration('2015-05-15 11:22:22', '2015-05-15 12:22:22'); // output: 1 hour
Format::duration('2015-05-15 11:22:22', '2015-05-15 13:22:22'); // output: 2 hours
Format::duration('2015-05-15 11:22:22', '2015-05-15 12:23:22'); // output: 1 hour 1 minute
Format::duration('2015-05-15 11:22:22', '2015-05-15 12:23:26'); // output: 1 hour 1 minute
Format::duration('2015-05-15 11:22:22', '2015-05-15 13:23:59'); // output: 2 hours 1 minute
Format::duration('2015-05-15 11:22:22', '2015-05-15 11:23:22'); // output: 1 minute
Format::duration('2015-05-15 11:22:22', '2015-05-15 11:24:22'); // output: 2 minutes
Format::duration('2015-05-15 11:22:22', '2015-05-15 11:24:46'); // output: 2 minutes
Format::duration('2015-05-15 11:22:22', '2015-05-15 11:24:46', true); // output: 2 minutes 24 seconds
Format::duration('2015-05-15 11:22:22', '2015-05-15 11:23:22', true); // output: 1 minute
Format::duration('2015-05-15 11:22:22', '2015-05-15 11:22:23', true); // output: 1 second
Format::duration('2015-05-15 11:22:22', '2015-05-15 11:22:27', true); // output: 5 seconds
Format::duration('2015-05-15 11:22:22', '2015-05-16 13:23:25', true); // output: 1 day 2 hours 1 minute 3 seconds
Format::duration('2015-05-15 11:22:22', '2015-05-16 11:22:25', true); // output: 1 day 3 seconds

// Using global function
// (string) format_duration((string) $date1, (string) $date2, (boolean) $show_second)
format_duration('2015-05-15 11:22:22', '2015-05-16 11:22:22'); // output: 1 day
format_duration('2015-05-15 11:22:22', '2015-05-17 11:22:22'); // output: 2 days
format_duration('2015-05-15 11:22:22', '2015-05-16 12:22:22'); // output: 1 day 1 hour
format_duration('2015-05-15 11:22:22', '2015-05-16 13:22:22'); // output: 1 day 2 hours
format_duration('2015-05-15 11:22:22', '2015-05-17 12:22:22'); // output: 2 days 1 hour
format_duration('2015-05-15 11:22:22', '2015-05-17 13:22:22'); // output: 2 days 2 hours
format_duration('2015-05-15 11:22:22', '2015-05-16 12:23:22'); // output: 1 day 1 hour 1 minute
format_duration('2015-05-15 11:22:22', '2015-05-16 12:24:22'); // output: 1 day 1 hour 2 minutes
format_duration('2015-05-15 11:22:22', '2015-05-16 13:23:22'); // output: 1 day 2 hours 1 minute
format_duration('2015-05-15 11:22:22', '2015-05-16 11:23:22'); // output: 1 day 1 minute
format_duration('2015-05-15 11:22:22', '2015-05-16 11:24:22'); // output: 1 day 2 minutes
format_duration('2015-05-15 11:22:22', '2015-05-17 11:24:22'); // output: 2 days 2 minutes
format_duration('2015-05-15 11:22:22', '2015-05-16 13:23:25'); // output: 1 day 2 hours 1 minute
format_duration('2015-05-15 11:22:22', '2015-05-16 11:22:25'); // output: 1 day
format_duration('2015-05-15 11:22:22', '2015-05-15 11:22:23'); // output: 1 second
format_duration('2015-05-15 11:22:22', '2015-05-15 11:22:27'); // output: 5 seconds
format_duration('2015-05-15 11:22:22', '2015-05-15 12:22:22'); // output: 1 hour
format_duration('2015-05-15 11:22:22', '2015-05-15 13:22:22'); // output: 2 hours
format_duration('2015-05-15 11:22:22', '2015-05-15 12:23:22'); // output: 1 hour 1 minute
format_duration('2015-05-15 11:22:22', '2015-05-15 12:23:26'); // output: 1 hour 1 minute
format_duration('2015-05-15 11:22:22', '2015-05-15 13:23:59'); // output: 2 hours 1 minute
format_duration('2015-05-15 11:22:22', '2015-05-15 11:23:22'); // output: 1 minute
format_duration('2015-05-15 11:22:22', '2015-05-15 11:24:22'); // output: 2 minutes
format_duration('2015-05-15 11:22:22', '2015-05-15 11:24:46'); // output: 2 minutes
format_duration('2015-05-15 11:22:22', '2015-05-15 11:24:46', true); // output: 2 minutes 24 seconds
format_duration('2015-05-15 11:22:22', '2015-05-15 11:23:22', true); // output: 1 minute
format_duration('2015-05-15 11:22:22', '2015-05-15 11:22:23', true); // output: 1 second
format_duration('2015-05-15 11:22:22', '2015-05-15 11:22:27', true); // output: 5 seconds
format_duration('2015-05-15 11:22:22', '2015-05-16 13:23:25', true); // output: 1 day 2 hours 1 minute 3 seconds
format_duration('2015-05-15 11:22:22', '2015-05-16 11:22:25', true); // output: 1 day 3 seconds
```

### Remove New Line in String

Will remove `\n`, `\r`, and spaces in string to make it in one line.
```php
// Using facade
// (string) Format::removeNewLine((string) $string)
Format::removeNewLine("Hello 
        World"); // output: Hello World
Format::removeNewLine("Hello 
        
        
        World
        
        
        "); // output: Hello World
Format::removeNewLine("Hello        World
        
        
        "); // output: Hello World

// Using global function
// (string) format_remove_new_line((string) $string)
format_remove_new_line("Hello 
        World"); // output: Hello World
format_remove_new_line("Hello 
        
        
        World
        
        
        "); // output: Hello World
format_remove_new_line("Hello        World
        
        
        "); // output: Hello World
```