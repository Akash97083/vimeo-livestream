![build](https://github.com/francis94c/vimeo-livestream/workflows/build/badge.svg) [![Coverage Status](https://coveralls.io/repos/github/francis94c/vimeo-livestream/badge.svg?branch=master)](https://coveralls.io/github/francis94c/vimeo-livestream?branch=master) [![Maintainability](https://api.codeclimate.com/v1/badges/5f2940c68fd16c1812fc/maintainability)](https://codeclimate.com/github/francis94c/vimeo-livestream/maintainability) 

# vimeo-livestream
PHP Client Library for Vimeo Live Stream.

<p style="text-align:center;"><img width="200" src="https://livestream.com/assets/images/shared/livestream_og_image.jpg"/></p>

## Installation ##
This Live Stream API is available on Packagist as francis94c/vimeo-livestream

```php
$ composer require francis94c/vimeo-livestream
```

## Usage ##
Creating a LiveStream Instance.

```php
use LiveStream\LiveStream;

$livestream = new LiveStream('[YOUR_API_KEY]');
```

Before you proceed, note that `$livestream` function calls that return null, indicates that the requested resource was not found. In summary, a 404 HTTP Response Code was received as a result of the call. 

__Every other HTTP Response Code will throw an Exception.__

### Get Accounts ###
```php
$accounts = $livestream->getAccounts(); // Returns an array of account resources.
```

### Get Specific Account ###
```php
$account = $livestream->getAccount(23456 /*Account ID*/); // Returns \LiveStream\Resources\Account.
```

### Create an Event ###
```php
use LiveStream\Resources\Event;

$event = new Event("A Career Master Class" /*fullName*/);
// See https://livestream.com/developers/docs/api/#event-object
$event->setShortName("Master Class"); /*Or*/ $event->shortName = 'Master Class';
$event->setStartTime("2020-07-20 23:56:20"); /*Or*/ $event->startTime = /*Time in ISO8601 date time format*/
```

### Get RTMP Key ###
```php
$key = $livestream->getRtmpKey(3456 /*Account ID*/, 4567, /*Event ID*/); // Returns \LiveStream\Resources\RTMPKey.
echo $key->id . ' --- ' . $key->rtmpUrl;
// OR
echo $key->getId() . ' --- ' . $key->getRtmpUrl();
```

### Reset RTMP Key ###
```php
$key = $livestream->resetRtmpKey(3456 /*Account ID*/, 4567, /*Event ID*/);
```