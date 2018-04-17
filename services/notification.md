# Notification Service (opendash/services/notification)

The notification services allows you to:
- Ask the user for confirmation
- Prompt the user for a string input
- Show a text popup.
- Open a custom component in a modal

**Contents:**
<!-- TOC depthFrom:2 depthTo:3 -->

- [Usage](#usage)
- [Properties & Methods](#properties--methods)
    - [$notification.create(options: Object)](#notificationcreateoptions-object)
    - [$notification.\[success|info|warning|danger](message: String)](#notification\successinfowarningdangermessage-string)

<!-- /TOC -->

## Usage

Use the Modal Service by injecting `opendash/services/modal` as an Angular Service. We suggest using `$notification` as a name for the variable.

Example:
```js
class controller {

  static get $inject() { return ['opendash/services/notification']; }

  constructor($notification) {
    // ...
  }
}
```

## Properties & Methods

### $notification.create(options: Object)

Creats a notification, using the options object.

The options object might have the following properties:

* `message: String` - Message that will be shown.
* `class: String` - Aditional classes which will be applied to the notification element.
* `focus: Boolean` (default: false) - If true, an overlay will be created to make the user focus on the notification.
* `time: Boolean` (default: 5000) - Time in milliseconds after which the notification will be closed. Might be false, so the notification will stay until the user closes the notification.

#### Response

No response.

### $notification.\[success|info|warning|danger](message: String)

Creates a simple notification showing the message in one of the following styles:

* success
* info
* warning
* danger

#### Response

No response.
