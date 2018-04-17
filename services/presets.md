# Presets Service (opendash/services/presets)

The persets services allows you to open the presets modal.

**Contents:**
<!-- TOC depthFrom:2 depthTo:3 -->

- [Usage](#usage)
- [Properties & Methods](#properties--methods)
    - [$presets.open()](#presetsopen)

<!-- /TOC -->

## Usage

Use the Presets Service by injecting `opendash/services/presets` as an Angular Service. We suggest using `$presets` as a name for the variable.

Example:
```js
class controller {

  static get $inject() { return ['opendash/services/presets']; }

  constructor($presets) {
    // ...
  }
}
```

## Properties & Methods

### $presets.open()

Opens the presets modal.

#### Response

Returns a promise resolving to a widget configuration. The promise might be rejected if the user decides to close the modal.