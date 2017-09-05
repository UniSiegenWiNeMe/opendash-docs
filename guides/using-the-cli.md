# Using the CLI to create a stand alone open.DASH instance

When you have been following the [Prerequisites](../README.md#prerequisites), you are good to go!

All following commands are to be entered into console.

<!-- TOC depthFrom:2 depthTo:6 -->
- [Installing the CLI](#installing-the-cli)
- [Creating an instance](#creating-an-instance)
- [Building the instance](#building-the-instance)
- [Next steps](#next-steps)
- [Files](#files)
  - [package.json](#packagejson)
  - [index.html](#indexhtml)
  - [app.js](#appjs)

<!-- /TOC -->


## Installing the CLI

First thing you need to do is to install the open.DASH CLI globaly by using NPM.

```
> npm install -g opendash-cli
```

## Creating an instance

Once this is done, change in a directory where you want to build your app and run the `opendash init` command to create a new open.DASH instance.
Note: open.DASH will create a folder of the instance during installation, so no need to create a folder yourself.

A few questions will be asked and the output will look something like this:

```
> opendash init instance
  open.DASH CLI v1.0.4
  ? Pick a name: example
  ? Author Name: My Name
  ? Author Email: my.name@example.com
  Starting download of template 'instance' into './opendash-instance-example'...
  Download of 'instance' finished.
  Initialization of 'example' finished.
```

In this case a directory called `opendash-instance-example` was created, the next step is to change in this directory and open it with your preferred editor (We like VS Code).

You will see a folder structure like this:

```
├── app/
│   ├── js/
│   │   ├── app.js
│   │   ├── data-adapter.js
│   │   └── user-adapter.js
│   ├── scss/
│   │   ├── _config.scss (optional)
│   │   ├── _widgets.scss (optional)
│   │   └── style.scss
│   └── index.html
├── dist/
│   └── ...
└── package.json
```

## Building the instance

In Console, navigate into the folder of your open.DASH instance.

Before building your instance you have to run `npm install` to load all the dependencies in the instance folder.

To test your build, run `opendash build` or `npm run build`.

To test the behaviour of your build, you can start a simple web server for your open.DASH instance adding the `--serve` flag (short: `-s`) to your build statement.
Additionally, you can automatically open your browser by adding `-o` and specify the port by adding `--port 8080`.

If you want the build tool to watch for changes you make and build every time a change is detected, use the `--watch` flag (short: `-w`).
This way, you do not have to rebuild once you change the widgets or the instance intsself.

For your convenience, we added a npm script running `opendash build -ws`: Its called `npm run watch`.

## Next steps

Check the following links, to learn how to feed your instance with data and how to extend open.DASH with custom widgets.

  - [Authenticate with the User Adapter](/guides/using-the-cli/user-adapter.md)
  - [Learn about Data Adapters](/guides/using-the-cli/data-adapter.md)
  - [Extend with custom Widgets](/guides/using-the-cli/widgets.md)
  - [Create your own Style](/guides/using-the-cli/style.md)
  - [Configurate by using the $env Service](/services/env.md)

## Files

### package.json

```json
{
  "name": "opendash-instance-name",
  "version": "1.0.0",
  "license": "PRIVATE",
  "private": true
}
```

### index.html

```html
<!DOCTYPE html>
<html lang="de" ng-app="app">
  <head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1">

    <title>open.DASH</title>
    <link rel="shortcut icon" href="assets/vendor/opendash/favicon.ico" type="image/x-icon" />
  </head>
  <body>
    <!-- Quick Start Component -->
    <opendash></opendash>

    <script src="http://code.highcharts.com/highcharts.src.js"></script>
  </body>
</html>
```

### app.js

```js
import openDASH from 'opendash';

// Adapter:
import userAdapter from './user-adapter.js';
import smartliveDataAdapter from './smartlive.data-adapter.js';

// Custom Components:
import heroMap from './components/map.component';

const instance = new openDASH();

instance.registerUserAdapter(userAdapter);
instance.registerDataAdapter('smartlive', smartliveDataAdapter);

instance.registerWidget('strom-ubersicht', require('./widgets/electricity-overview/src/index.js').default());
instance.registerWidget('temperatur-ubersicht', require('./widgets/temperature-overview/src/index.js').default());
instance.registerWidget('sicherheit-ubersicht', require('./widgets/security-overview/src/index.js').default());
instance.registerWidget('luftqualitaet-ubersicht', require('./widgets/airquality-overview/src/index.js').default());

// App initialisieren:
const app = angular.module('app', [instance.name]);
```
