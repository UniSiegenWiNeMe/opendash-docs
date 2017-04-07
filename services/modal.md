# Modal Service (od.modal.service)

<!-- TOC -->

- [Modal Service (od.modal.service)](#modal-service-odmodalservice)
  - [Nutzung](#nutzung)
    - [$dashboard.showModal(options)](#dashboardshowmodaloptions)

<!-- /TOC -->

Mit dem Modal Service kann ein neues Modal erzeugt werden.

## Nutzung

Der Modal Service kann benutzt werden indem `od.modal.service` über Angular injected wird. Es empfiehlt sich diesen dann mit dem Parameter Namen `$modal` zu benutzen.

Beispiel:

```js
class controller {

  static $inject = ['od.modal.service'];

  constructor($modal) {
    // ...
  }
}
```

### $dashboard.showModal(options)

(TODO) Dokumentation fehlt.