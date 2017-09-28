# Using the API

This guide will show you how to create and use the open.DASH Class to create an angularjs module.

This guide assumes that you have a build process up and running. If you don't want to use open.DASH in an existing angularjs app, you might want to read the [Using the CLI](/guides/using-the-cli.md) guide.

**Contents:**
<!-- TOC depthFrom:2 depthTo:3 -->

- [Installation](#installation)
- [Usage](#usage)
- [Methods](#methods)
  - [instance.registerUserAdapter(adapter)](#instanceregisteruseradapteradapter)
  - [instance.registerDataAdapter(name, adapter)](#instanceregisterdataadaptername-adapter)
  - [instance.registerWidget(widget)](#instanceregisterwidgetwidget)
  - [instance.registerWidgets(widgets)](#instanceregisterwidgetswidgets)
  - [instance.env(key, value)](#instanceenvkey-value)
  - [instance.config(settings)](#instanceconfigsettings)
  - [instance.start()](#instancestart)

<!-- /TOC -->

## Installation

Simply pull opendash from npm:

```
npm install --save opendash
```

## Usage

Get the open.DASH Class by importing it in the file you want to use open.DASH in. Secondly, create an instance to be able to use the API.

```js
import openDASH from 'opendash';

const instance = new openDASH();
```

## Methods

Once you have an instance, you can use the following methods:

### instance.registerUserAdapter(adapter)
TODO Description
### instance.registerDataAdapter(name, adapter)
TODO Description
### instance.registerWidget(widget)
TODO Description
### instance.registerWidgets(widgets)
TODO Description
### instance.env(key, value)
TODO Description
### instance.config(settings)
TODO Description
### instance.start()
TODO Description
