# Whats a widget in open.DASH
being a dashboard, open.DASH allows you to visualize data in most different ways, just according to your needs and allows you to add new ways of displaying information. For this, we use widgets. Widgets are like tiles on your dashboard and can be programmed to both use the items and data provided by the adapter, and rely on external information, libraries etc. from the web.

# Creating widgets using the CLI

Creating a widget is as easy as creating an instance. To create a widget use the same opendash init command but as the template select widget: `opendash init widget` 

```
> opendash init widget
  open.DASH CLI v1.0.4
  ? Pick a name: example
  ? Author Name: My Name
  ? Author Email: my.name@example.com
  Starting download of template 'widget' into './opendash-widget-example'...
  Download of 'widget' finished.
  Initialization of 'example' finished.
```

Go ahead and customize the widget the way you want. If you want to learn more about widgets, check out the [Widget Guide](/guides/widgets.md).

## About the template

This template is meant to be an easy way to start a new widget with an opinionated approach. It's written in ES6 Javascript, uses [ES6 classes](http://es6-features.org/#ClassDefinition) and template strings will be loaded from files. The widget uses two [SCSS](http://sass-lang.com/) files for styling, which will also be loaded automatically. The widget is build to be a `node_module`, so the widget name is taken from the `package.json` file.

### Directory structure

```
├── src/
│   ├── widget/
│   │   ├── widget.controller.js
│   │   ├── widget.template.html
│   │   └── widget.scss
│   ├── settings/
│   │   ├── settings.controller.js
│   │   ├── settings.template.html
│   │   └── settings.scss
│   ├── assets/
│   │   └── ...
│   ├── index.js
│   └── presets.js
├── README.md
└── package.json
```

## Linking widgets for development.

For development, use the [npm link](https://docs.npmjs.com/cli/link) command:
(EXPAND THIS SECTION: which folder in?)
`npm run link` 
