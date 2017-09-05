# Widgets Guide

Once you have setup your user and data adapter, you want your users to access all the information. In open.DASH you do this by providing widgets, which can be used by your users, so they can customize their dashboards.

## instance.registerWidget()

Once you have an instance, you can `import` widgets and register them:

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