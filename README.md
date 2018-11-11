# libmergepdf

[![Packagist Version](https://img.shields.io/packagist/v/iio/libmergepdf.svg?style=flat-square)](https://packagist.org/packages/iio/libmergepdf)
[![Build Status](https://img.shields.io/travis/hanneskod/libmergepdf/master.svg?style=flat-square)](https://travis-ci.org/hanneskod/libmergepdf)
[![Quality Score](https://img.shields.io/scrutinizer/g/hanneskod/libmergepdf.svg?style=flat-square)](https://scrutinizer-ci.com/g/hanneskod/libmergepdf)

PHP library for merging multiple PDFs.

## Installation

Install using [composer](http://getcomposer.org/).

```shell
composer require iio/libmergepdf:^4.0
```

## Usage

Append the first ten pages of **bar.pdf** to **foo.pdf**:

```php
use iio\libmergepdf\Merger;
use iio\libmergepdf\Pages;

$merger = new Merger;
$merger->addFile('foo.pdf');
$merger->addFile('bar.pdf', new Pages('1-10'));
$createdPdf = $merger->merge();
```

Bulk add files from an iterator:

```php
use iio\libmergepdf\Merger;
$merger = new Merger;
$merger->addIterator(['A.pdf', 'B.pdf']);
$createdPdf = $merger->merge();
```

## Merging pdfs of version 1.5 and later

The default `FPDI` driver is not able handle compressed pdfs of version 1.5 or later.
Circumvent this limitation by using th slightly more experimental `TCPDI` driver.

```php
use iio\libmergepdf\Merger;
use iio\libmergepdf\Driver\TcpdiDriver;

$merger = new Merger(new TcpdiDriver);
```

## Known issues

* Links and other content outside a page content stream is removed at merge.
  This is due to limitations in FPDI and not possible to resolve with the
  current strategy. For more information see [FPDI](https://www.setasign.com/support/faq/fpdi/after-importing-a-page-all-links-are-gone/#question-84).
