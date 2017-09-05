# Wellcome to the open.DASH Documentation

This page is still under construction.

## About open.DASH
HERE BE INTRO TEXT
open.DASH ist an open source visualization framework written mainly in javascript. 

There are two ways to work with open.DASH:
 - Use our Command Line Interface (CLI) to develop stand alone open.DASH applications 
 - Use our library to generate an Angularjs module to use in your existing Angularjs application.

## Prerequisites 

Either way you want to work with open.DASH, you need to 

- install [nodejs](https://nodejs.org/en/) version  `>=7.6.0` and 
- use [npm](ttps://www.npmjs.com) version `>=5.3.0` (console: `npm i -g npm@latest`).

npm is a JavaScript package manager, that is very popular in Node.js development. It allows you to pull packages, other developers have created. We also use it for open.DASH, which is why you can it from there to start working. 

You can check your node version by using `node -v` and your npm version by running `npm -v` in your console.

This guide further assumes that you know 
 - features of [ES2015 Javascript language](https://babeljs.io/learn-es2015/) like const/let, arrow functions and classes
 - feature of [Angularjs](https://angularjs.org/) `^1.5`, especially components and services
 - build tools like [webpack](https://webpack.js.org/)(IS THIS THE RIGHT LINK?)

### Stand alone apps

If you just want to use the open.DASH Dashboard for now, you might want to use our CLI Tools to generate an instance and then build it. To get started using the CLI, [click here](/guides/using-the-cli.md).

### open.DASH Class API
#### Prerequisites
- Install Node.js Current (not LTS)
- Install npm from here: h



#### Installation

After installation of npm you have everything you need.
Now pull opendash from npm by typing in your command line:

```
npm install --save opendash
```

This should work from every folder, since npm is installed globally on your machine.

Then, get the open.DASH Class by requiring it in the file xou want to use open.DASH in. Secondly, create an instance to be able to use the API (IN WHICH FILE??).


```js
import openDASH from 'opendash';

const instance = new openDASH();
```

#### Usage
Once you have an instance, you can use the following methods

##### instance.registerUserAdapter(adapter)
TODO Description
##### instance.registerDataAdapter(name, adapter)
TODO Description
##### instance.registerWidget(widget)
TODO Description
##### instance.registerWidgets(widgets)
TODO Description
##### instance.env(key, value)
TODO Description
##### instance.config(settings)
TODO Description
##### instance.start()
TODO Description
