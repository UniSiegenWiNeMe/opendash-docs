# Modal Service (od.modal.service)

The modal services allows you to:
- Ask the user for confirmation
- Prompt the user for a string input
- Show a text popup.
- Open a custom component in a modal

**Contents:**
<!-- TOC depthFrom:2 depthTo:3 -->

- [Usage](#usage)
- [Properties & Methods](#properties--methods)
  - [$dashboard.confirm(message: String)](#dashboardconfirmmessage-string)
  - [$dashboard.prompt(message: String)](#dashboardpromptmessage-string)
  - [$dashboard.showModal(options)](#dashboardshowmodaloptions)

<!-- /TOC -->

## Usage

Use the Modal Service by injecting `od.modal.service` as an Angular Service. We suggest using `$modal` as a name for the variable.

Example:
```js
class controller {

  static $inject = ['od.modal.service'];

  constructor($modal) {
    // ...
  }
}
```

## Properties & Methods

### $dashboard.confirm(message: String)

Asks the user to confirm the given message.

#### Response

Returns a promise resolving to `true` or `false`. The promise might be rejected if the user decides to close the modal.

### $dashboard.prompt(message: String)

Asks the user for an input string showing the given message.

#### Response

Returns a promise resolving to the input. The promise might be rejected if the user decides to close the modal.

### $dashboard.showModal(options)

Do not use this method currently, as the api is not final. 