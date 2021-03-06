# metalsmith-metadata-directory

[![npm](https://img.shields.io/npm/v/metalsmith-metadata-directory.svg)](https://www.npmjs.com/package/metalsmith-metadata-directory)
[![Build Status](https://travis-ci.org/fephil/metalsmith-metadata-directory.svg?branch=master)](https://travis-ci.org/fephil/metalsmith-metadata-directory)
[![GitHub license](https://img.shields.io/badge/license-MIT-blue.svg)](https://raw.githubusercontent.com/fephil/metalsmith-metadata-directory/master/LICENSE)

> A Metalsmith plugin to add a directory of JSON and/or YAML files for use as global metadata in templates, partials and pages.

* Author: [Phil Lennon](https://phil.dev)
* Source: [github.com/fephil/metalsmith-metadata-directory](https://github.com/fephil/metalsmith-metadata-directory)
* Issues & Suggestions: [github.com/fephil/metalsmith-metadata-directory/issues](https://github.com/fephil/metalsmith-metadata-directory/issues)
* Releases: [https://github.com/fephil/metalsmith-metadata-directory/releases](https://github.com/fephil/metalsmith-metadata-directory/releases)
* Twitter: [@frontendphil](https://twitter.com/frontendphil)
* Email: [enquiry@phil.dev](mailto:enquiry@phil.dev)

***

## About

This plugin supports adding a directory of `.json` & `.yml/.yaml` files and makes their contents available to the Metalsmith global metadata, without needing to declare multiple file names. Subdirectories and multiple files are supported by using a globbing pattern.

## Node support

This plugin is supported and tested against all the current Node LTS versions (10 & 12). This plugin should work on Node 6 & 8 but is not supported for these versions.

## Installation

Install the plugin using npm, and specify the directory of metadata files you want to use, along with a globbing pattern.

```
$ npm install metalsmith-metadata-directory --save-dev
```

### With Metalsmith CLI

Add the plugin to your metalsmith.json file:

```js
{
  "plugins": {
    "metalsmith-metadata-directory": {
      "directory": "/src/data/**/*.json"
    }
  }
}
```

**NOTE:** .yml and .yaml file extensions are also supported.

### With JavaScript

Pass the plugin into metalsmith.use:

```js
var metalsmith = require('metalsmith')
var metadata = require('metalsmith-metadata-directory')

metalsmith.use(metadata({
  directory: '/src/data/**/*.json',
  // or for YAML respectively; be sure to use 'yml' or 'yaml' as file suffix
  directory: '/src/data/**/*.yml'
}));
```

## Plugin ordering

It is vital to order Metalsmith plugins correctly. Please make sure this plugin is included above metalsmith-layouts and metalsmith-in-place and any other plugin which may use your metadata.

## Usage within Metalsmith

Data is called by referencing the filename without an extension. For example, if there was a global.json file containing a url key, the reference in your page or template would look like:

```js
{{global.url}}
```

## Debug mode

This plugin supports debugging output. To enable, use the following command when running Metalsmith:

```
$ DEBUG=metalsmith-metadata-directory metalsmith
```

## Using with metalsmith auto-reload 

This plugin check for duplicate key, as most of auto-reload plugin (like metalsmith-watch) will keep the metadata of the previous executions. The error must be disabled in this case.

A valid usage with metalsmith-watch : 
```
metalsmith.use(metadata({
  directory: '/src/data/**/*.json',
  returnErrorOnDuplicate: false
}));
```

Be aware this configuration is recommand only in dev-mode. The duplicate keys will not be checked otherwise.

## Licence

MIT
