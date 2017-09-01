# Wellcome to the open.DASH Documentation

This page is still under construction.

## About open.DASH

...

## Getting Started

There are two ways to work with open.DASH. You can use our CLI to develop stand alone open.DASH applications or you can use our library to generate an Angularjs module, which you can use in your existing Angularjs application.

### Stand alone apps

If you just want to use the open.DASH Dashboard for now, you might want to use our CLI Tools to generate an instance and then build it. To get started using the CLI, [click here](guides/using-the-cli.md).

### open.DASH Class API

First you need to pull opendash from npm.

```
npm install --save opendash
```

Then you will be able to get the open.DASH Class by requiring it and create a.

```js
import openDASH from 'opendash';

const instance = new openDASH();
```

Once you have an instance, you can use the following methods

#### instance.registerUserAdapter(adapter)
#### instance.registerDataAdapter(name, adapter)
#### instance.registerWidget(widget)
#### instance.registerWidgets(widgets)
#### instance.env(key, value)
#### instance.config(settings)
#### instance.start()