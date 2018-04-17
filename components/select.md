# open.DASH Selection Components for Settings

The following components allow you to build settings faster by letting your users select dates and items from your data sources.

**Contents:**
<!-- TOC depthFrom:2 depthTo:3 -->

- [od-select-item](#od-select-item)
    - [Usage](#usage)
    - [Example](#example)

<!-- /TOC -->

## od-select-item

The `od-select-item` component allows your user to select one or more item(s)/container(s) available to the `opendash/services/data`.

### Usage

Create an instance by using the `od-select-item` tag in your template. You have to specify a configuration object and an watch function as attributes.

#### Attributes

**watch**: A `Function` which will be triggered when the selection changes. It takes one parameter, which will be the current selection.
**config**: An `Object` which holds all configuration.

The config Object might have the following properties:

- **root**: `Boolean`: Wether only elements without an parent are available.
- **items**: `Boolean`: Wether only elements of the type `OpenDashDataItem` are available.
- **containers**: `Boolean`: Wether only elements of the type `OpenDashDataContainer` are available.
- **type**: `Boolean`: Wether only elements of the type `OpenDashDataContainer` are available.


### Example

```js

```

## od-select-date



### Usage

### Example

```js

```