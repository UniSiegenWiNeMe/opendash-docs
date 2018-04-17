# Plugins

If you create a collection of widget or you want to use custom components or services, you may want to create an open.DASH plugin.

**Contents:**
<!-- TOC depthFrom:2 depthTo:3 -->

- [Using Plugins](#using-plugins)
- [Official Plugins](#official-plugins)
    - [EUD Editor](#eud-editor)
- [Creating Plugins](#creating-plugins)

<!-- /TOC -->

## Using Plugins

You can register a plugin by calling the `instance.use(plugin: Function [, options: Object]);` method with an plugin. Examples are below.

## Official Plugins

There are some plugins ready to use right now:

### EUD Editor

Install via NPM: `npm i -S @opendash/user-adapter-local`

Make sure to install version `^4.0.0` for opendash version `2.0.0`.

```js
// app.js

import instance from 'opendash';
import eudPlugin from 'opendash/plugins/eud';

instance.use(eudPlugin);
```

## Creating Plugins

Example:

```js
// plugin.js
export default function (options) {
    return function (instance, module, name) {
        instance.registerWidget(myWidget);

        instance.module.service('myServiceName', eudService);
        instance.module.component('myComponentName', eudComponent);
    
        instance.module.run(['opendash/services/notification', ($notification) => {
            $notification.create('Using my plugin');
        }]);
    };
}

// app.js

import instance from 'opendash';
import myPlugin from './plugin.js';

instance.use(myPlugin);
```