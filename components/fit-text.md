# fit-text Component

`fit-text` ist ein Angular Component, mit dem man Text auf eine möglichst große Größe skalieren kann, ohne dass overflow entsteht.

## Benutzung

Im Tempalte an ensprechender Stelle den `fit-text` Component einfügen:

```html
<fit-text
  fttext="$ctrl.ft.text"
  ftwidth="$ctrl.ft.width"
  ftheight="$ctrl.ft.height"
  ftgroup="$ctrl.ft.group"
  >
  </fit-text>
```

Im Javascript den folgenden Code einfügen:

```js
this.ft = {
  text: "Der anzuzeigende Text",
  width: "100%", // Die Breite des Elements
  height: "50%", // Die Höhe des Elements
  group: 1000, // Die Gruppe zur Synchronisierung mehrerer fit-text
};
```

`ftgroup` muss auf 1000 initialisiert werden.

### Beispiel für Synchronisierung

Meherere `fit-text` Elemente können mit `ftgroup` auf die gleiche Größe synchronisiert werden, indem die gleiche Variable für zwei oder mehr `fit-text` Elemente verwendet wird.

Template:

```html
<fit-text
  fttext="$ctrl.ft1.text"
  ftwidth="$ctrl.ft1.width"
  ftheight="$ctrl.ft1.height"
  ftgroup="$ctrl.ftgroup"
  >
  </fit-text>

<fit-text
  fttext="$ctrl.ft2.text"
  ftwidth="$ctrl.ft2.width"
  ftheight="$ctrl.ft2.height"
  ftgroup="$ctrl.ftgroup"
  >
  </fit-text>
```

Javascript:

```js
this.ft1 = {
  text: "Text Nr. 1",
  width: "100%",
  height: "50%",
};


this.ft2 = {
  text: "Text Nr. 2",
  width: "100%",
  height: "50%",
};

this.ftgroup = 1000;
```