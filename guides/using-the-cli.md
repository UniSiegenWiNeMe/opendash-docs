# Using the CLI to create a stand alone open.DASH instance

This guide will show you how to create and build a stand alone open.DASH instance by using the CLI.

If you allready have a build process up and running and just want to use the open.DASH Library, you might want to read the [Using the API](/guides/using-the-api.md) guide.

All following commands are to be entered into console.

<!-- TOC depthFrom:2 depthTo:6 -->

- [Prerequisites](#prerequisites)
- [Installing the CLI](#installing-the-cli)
- [Creating an instance](#creating-an-instance)
- [Building the instance](#building-the-instance)
- [Next steps](#next-steps)

<!-- /TOC -->

## Prerequisites 

To use the CLI you need to install

- [nodejs](https://nodejs.org/en/) version  `>=7.6.0` 
- [npm](https://www.npmjs.com/get-npm) version `>=5.3.0` (console: `npm i -g npm@latest`).

The CLI is written in Node.js. Node.js is a JavaScript runtime, which works outside of browsers.

Both the CLI and open.DASH are published on npm. npm is a JavaScript package manager, that became popular for hosting JavaScript modules. It allows you to publish and pull packages, other developers have created. It also allows you to save dependencies for your project, so you don't need to bundle all third party libraries with your application, instead you will simply run `npm install`.

You can check your node version by using `node -v` and your npm version by running `npm -v` in your console.

This guide further assumes that you know 
 - features of [ES2015 Javascript language](https://babeljs.io/learn-es2015/) like const/let, arrow functions and classes
 - features of [Angularjs](https://angularjs.org/) `^1.5`, especially dependency injection, components and services are important 
 - build tools like [webpack](https://webpack.js.org/)
 - JS preprocessors like [babel](https://babeljs.io/)
 - CSS preprocessors like [scss](http://sass-lang.com/)

## Installing the CLI

First thing you need to do, is to install the open.DASH CLI globaly by using NPM.

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

  - [Authenticate with the User Adapter](/guides/user-adapter.md)
  - [Learn about Data Adapters](/guides/data-adapter.md)
  - [Extend with custom Widgets](/guides/using-the-cli/widgets.md)
  - [Create your own Style](/guides/using-the-cli/style.md)
  - [Configurate by using the $env Service](/services/env.md)