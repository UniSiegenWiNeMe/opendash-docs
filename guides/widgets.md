# Widgets Guide

Once you have setup your user and data adapter, you want your users to access all the information. In open.DASH you do this by providing widgets, which can be used by your users, so they can customize their dashboards.

**Contents:**
<!-- TOC depthFrom:2 depthTo:3 -->

- [instance.registerWidget()](#instanceregisterwidget)
    - [instance.registerWidgets()](#instanceregisterwidgets)
- [Widget factory](#widget-factory)
- [Widget object](#widget-object)
    - [name](#name)
    - [widgetController](#widgetcontroller)
    - [widgetTemplate](#widgettemplate)
    - [settingsController](#settingscontroller)
    - [settingsTemplate](#settingstemplate)
    - [presets](#presets)

<!-- /TOC -->

## instance.registerWidget()

Once you have an instance, you can `import` widgets and register them in your instance. You do this in app/js/app.js:

```js
import exampleWidget from 'opendash-widget-example';
// ...
instance.registerWidget(exampleWidget);
```

### instance.registerWidgets()

If you want to save a few keystrokes, you can move all your widgets in an array and use `instance.registerWidgets()`, which takes an array as a parameter and registers every widget in said array.

```js
import exampleWidgetOne from 'opendash-widget-example-one';
import exampleWidgetTwo from 'opendash-widget-example-two';

const widgets = [
  exampleWidgetOne,
  exampleWidgetTwo,
];

instance.registerWidgets(widgets);
```

You can go a step further, if you don't need to follow ES6 strictly and do something like this:

```js
instance.registerWidgets([
  require('opendash-widget-example-one').default,
  require('opendash-widget-example-two').default,
]);
```

## Widget factory
Each widget you pass into the `registerWidget()` method, needs to be a function (widget factory) which returns the widget object.

```js
// widget factory
export default (options) => {
  // widget object
  return {
    name,
    widgetController,
    widgetTemplate,
    settingsController,
    settingsTemplate,
    presets,
  };
};
```

## Widget object

Widgets need two [Angular Components](https://docs.angularjs.org/guide/component). One for the widget itself and one for the settings of the widget.

The widget object needs the following properties:

```js
{
  name,
  widgetController,
  widgetTemplate,
  settingsController,
  settingsTemplate,
  presets,
}
```

### name

The unique identifier of the widget. Needs to start with `opendash-widget-`, should use only lower case letters and `-`.

We suggest doing this:

```js
import pkg from 'path/to/package.json';
const name = pkg.name;
```

### widgetController

A controller for the widget [Angular Component](https://docs.angularjs.org/guide/component).

#### Layout

An controller written in ES6 may look like this:

```js
export default class WidgetController {

  static $inject = ['od.data.service', '$element', '$scope', 'moment', 'lodash'];

  constructor($data, $element, $scope, moment, _) {
    // ...
  }
}
```

Note: The static $inject property is set for Angular to know which dependencies must be injected.

Your Controller may have any methods and properties, but it shouldn't overwrite its properties `this.widget`, `this.state` and `this.config`.

#### Configuration (this.config)

> Warning: Some of the following features are using Proxies, which will not be transformed by Babel. Make sure to use an up-to-date browser to utilise all of the features.

> Note: You may run into an Error (or nothing happens) if you try to access `this` within callbacks, when you are not using arrow functions. Make sure you are accessing `this` in the right scope.

You can access your config using `this.config`, which is an object.

You can but shouldn't write to the config object in your widget controller.

To write to the config, you should utilise the settings component.

```js
export default class WidgetController {

  static $inject = [];

  constructor() {
    // access your configuration object
    console.log(this.config);

    // access a configuration property
    console.log(this.config.key);

    // watch a property for changes
    // the callback will be called immediately
    // and every time the property changes
    this.config.watch('key', (value, oldValue) => {
      // oldValue might be undefined
      console.log(value, oldValue);
    });
  }
}
```

#### State (this.state)

> Note: You may run into an Error (or nothing happens) if you try to access `this` within callbacks, when you are not using arrow functions. Make sure you are accessing `this` in the right scope.

Managing the state of an widget is as easy as setting some booleans to a few variables.

There are currently three states:

##### this.state.loading

When it's `true`, there will be a loading animation covering your widget.

By default this value is `true`.

**Example:**

Set the loading state to false, as soon as all the informations, which are required to show your widget, are loaded:

```js
export default class WidgetController {

  static $inject = ['od.data.service'];

  constructor($data) {
    // ...
    $data.get(id).history(options).then((history) => {
      // Once everything is setup call the following line:
      this.state.loading = false;
    });
  }
}
```

##### this.state.config

Whether the config is valid. When it's `true` nothing will happen, when it's `false` there will be a message asking the user to configurate the widget.

By default this value is `false`.

**Example:**

You may want to set the config state to true as soon as possible in the constructor, make sure to finish the constructor by calling `return;`.

Your widget (and its controller) will be destroyed once this is done and a new widget will be created once there will be a change to the configuration (and the settings modal is closed).

You should also implement some kind of validation in your settings controller, so there's not so much back and forth.

```js
export default class WidgetController {

  static $inject = ['od.data.service'];

  constructor($data) {
    if (!this.config.needed) {
      // an important config is missing, set the state to false:
      this.state.config = false;
      return;
    }
  }
}
```

##### this.state.alert

When it's `false` nothing will happen, when it's `true` there will an anmation making the user aware of the situation.

By default this value is `false`.

Note: Once the value is set to true, you should set it back to false after some time or after an interaction.

**Example:**

```js
export default class WidgetController {

  static $inject = ['od.data.service', '$timeout'];

  constructor($data, $timeout) {
    let value = $data.get(id).value;

    if (!this.isValueOk(value)) {
      // Value is critical, alert the user:
      this.state.alert = true;

      // Set the state to false after 5 seconds
      $timeout(() => {
        this.state.alert = false;
      }, 5000);
    }

    // ...
  }

  isValueOk(value) {
    // ...
  }
}
```

### widgetTemplate

A template string for the widget [Angular Component](https://docs.angularjs.org/guide/component).

### settingsController

A controller for the settings [Angular Component](https://docs.angularjs.org/guide/component).

### settingsTemplate

A template string for the settings [Angular Component](https://docs.angularjs.org/guide/component).

### presets

An array with presets which looks like this, but it may be an empty array, if you don't need a preset:

```js
[
    {
        name: 'preset name',
        image: 'DATA URL or path/to/image.png',
        description: 'preset description...',
        config: {
            name: 'display name',
            grid: [2,0],
            config: {

            },
        },
    },
]
```
