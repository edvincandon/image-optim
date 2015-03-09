# image-optim [![Build Status](https://travis-ci.org/eGavr/image-optim.svg)](https://travis-ci.org/eGavr/image-optim) [![Coverage Status](https://coveralls.io/repos/eGavr/image-optim/badge.svg?branch=master)](https://coveralls.io/r/eGavr/image-optim?branch=master) [![Dependency Status](https://david-dm.org/eGavr/image-optim.svg)](https://david-dm.org/eGavr/image-optim) [![devDependency Status](https://david-dm.org/eGavr/image-optim/dev-status.svg)](https://david-dm.org/eGavr/image-optim#info=devDependencies)

Node.js wrapper for some images compression algorithms.

<!-- TOC -->
- [Types](#types)
- [Patches](#patches)
  - [Overview](#overview)
- [Install](#install)
- [Usage](#usage)
  - [API](#api)
    - [imageOptim.optim](#imageoptimoptim)
    - [imageOptim.lint](#imageoptimlint)
    - [SUCCESS](#imageoptimsuccess)
    - [CANT_COMPRESS](#imageoptimcant_compress)
    - [DOESNT_EXIST](#imageoptimdoesnt_exist)
  - [CLI](#cli)

<!-- TOC END -->

## Types

* PNG – [PNGOUT](http://www.advsys.net/ken/util/pngout.htm), [Zopflipng](https://github.com/pornel/zopfli), [Pngcrush](http://pmt.sourceforge.net/pngcrush/), [AdvPng](http://advancemame.sourceforge.net/doc-advpng.html) and [OptiPNG](http://optipng.sourceforge.net/).

Supporting of other types of images are coming soon.

## Patches

You can view all the _patches_ which are applied to the algorithms [here](https://github.com/eGavr/image-optim/tree/master/patch).

<!-- TOC:display:Overview -->
#### Overview:

* **optipng.patch** – adds to **OptiPNG** the ability to remove _RGB_ components or transparent pixels in _RGB+alpha_ images.

* **zopflipng.patch** – makes **Zopflipng** work on _Linux_.

## Install

```bash
$ npm install imageoptim
```

This command will install **image-optim** and all supported compression algorithms automatically. The installation of the compression algorithms is subscribed in script [env-setup](https://github.com/eGavr/image-optim/blob/master/env-setup).

## Usage

### API

```js
var imageOptim = require('imageoptim');
```

#### imageOptim.optim

Optimizes the given files.

**@param** *{Array}* – a list of paths to files to optimize<br>
**@param** *{Object}* – options:<br>

  * **reporters** *{Array}* - reporters of the results. _flat_ - writes the results to `stdout`, _html_ - creats the HTML report of the results in file `imageoptim-report.html`.

**@returns** *{Promise * Array}* – the information about optimized files:<br>

```js
[{ name: 'file.ext', savedBytes: 12345, exitCode: 0 }]
```

#### imageOptim.lint

Checks whether the given files can be optimized further.

**@param** *{Array}* – a list of paths to files to check<br>
**@param** *{Object}* – options:<br>

  * **tolerance** *{Number}* – sets the _measurement error_ in percentages. The file will be considered to be optimized if the percentage of saved bytes after the compression is less than the specified value.

  * **reporters** *{Array}* - reporters of the results. _flat_ - writes the results to `stdout`, _html_ - creats the HTML report of the results in file `imageoptim-report.html`.

**@returns** *{Promise * Array}* – the information about linted files:<br>

```js
[{ name: 'file.ext', isOptimized: false, exitCode: 0 }]
```

<!-- TOC:display:SUCCESS -->
#### imageOptim.SUCCESS

If the file was processed without errors its exit code will be equal to `0`.

<!-- TOC:display:CANT_COMPRESS -->
#### imageOptim.CANT_COMPRESS

If the file can not be compressed its exit code will be equal to `1`.

<!-- TOC:display:DOESNT_EXIST -->
#### imageOptim.DOESNT_EXIST

If the file does not exist its exit code will be equal to `2`.

### CLI

```bash
$ imageoptim --help
Node.js wrapper for some images compression algorithms

Usage:
  imageoptim [OPTIONS] [ARGS]

Options:
  -h, --help : Help
  -v, --version : Shows the version number
  -l, --lint : Lint mode
  -t TOLERANCE, --tolerance=TOLERANCE : Sets the measurement error in percentages (default: 0)
  -r REPORTERS, --reporter=REPORTERS : flat or/and html (default: flat)

Arguments:
  FILES : Paths to files (required)
```
