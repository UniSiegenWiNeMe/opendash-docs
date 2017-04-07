# Widget Entwicklung

<!-- TOC depthFrom:2 depthTo:6 -->

- [Entwicklung](#entwicklung)
  - [Konstruktor Funktion](#konstruktor-funktion)
  - [Widget Objekt](#widget-objekt)
    - [widgetController](#widgetcontroller)
    - [widgetTemplate](#widgettemplate)
    - [settingsController](#settingscontroller)
    - [settingsTemplate](#settingstemplate)
    - [presets](#presets)
- [Entwicklung mit open.DASH CLI](#entwicklung-mit-opendash-cli)
  - [Template herunterladen](#template-herunterladen)
  - [Widget builden](#widget-builden)
  - [Template Datei Struktur](#template-datei-struktur)
  - [Widget/Settings Controller](#widgetsettings-controller)
    - [Ladeanimation](#ladeanimation)
  - [Widget/Settings Template](#widgetsettings-template)
  - [Widget/Settings Styles](#widgetsettings-styles)

<!-- /TOC -->

## Entwicklung

Widgets bestehen aus zwei [Angular Components](https://docs.angularjs.org/guide/component), einen der für das Anzeigen der Widgets benötigt wird und einen für die Einstellungen des Widgets.

Die Components werden allerdings nicht vom Widget Entwickler registiert, statt dessen werden die Controller, die Templates und optional [SCSS](http://sass-lang.com/) in Form einer Konstruktor Funktion bereitgestellt, die ein Widget Objekt zurück gibt, welches an open.DASH übergeben und von open.DASH zusammen gesetzt wird.

### Konstruktor Funktion

Die Konstruktor Funktion ist kein Konstruktor im Sinne eines JS constructors. Es ist eine Funktion an die Optionen übergeben werden, mit deren Hilfe dann ein Widget Objekt erzeugt wird.

Beispiel:

```js
// instance.js
import { bootstrap } from 'opendash-core';
import widget from 'widget.js';

bootstrap({
    // ...
    widgets: {
        'widget-name': widget({
            // ...
        }),
    },
    // ...
});

// widget.js
// ...
export default (options) => {
    
    options = options || {};

    let presets = options.presets || defaultPresets;

    return {
        widgetController,
        widgetTemplate,
        settingsController,
        settingsTemplate,
        presets,
    };
};
```

### Widget Objekt

Das Beispiel von oben gibt das folgdene Widget Objekt zurück:

```js
{
    widgetController,
    widgetTemplate,
    settingsController,
    settingsTemplate,
    presets,
}
```

#### widgetController

Ein Controller für den Widget [Angular Component](https://docs.angularjs.org/guide/component).

#### widgetTemplate

Ein Template String für den Widget [Angular Component](https://docs.angularjs.org/guide/component).

#### settingsController

Ein Controller für den Settings [Angular Component](https://docs.angularjs.org/guide/component).

#### settingsTemplate

Ein Template String für den Settings [Angular Component](https://docs.angularjs.org/guide/component).

#### presets

Ein Array mit Presets, Beispiel:

```js
[
    {
        name: 'Preset Name',
        image: 'DATA URL oder path/to/image.png',
        description: 'Preset Description...',
        config: {
            name: 'Display Name',
            config: {

            },
        },
    },
]
```

## Entwicklung mit open.DASH CLI

> Zuerst muss die [open.DASH CLI installiert werden](CLI-Guide).

Mit hilfe der CLI kann ein Template herunter geladen werden, mit dem man die Entwicklung von Widgets schneller starten kann. Das Template kann dann über die CLI durch Babel und Rollup gebuildet werden.

Mehr Infos zum Template gibt es [hier](https://github.com/UniSiegenWiNeMe/opendash-widget-template).

### Template herunterladen

```
# opendash widget:init <widget-name>

$ opendash widget:init beispiel-widget

username: zlls
password: ****

  Initialize new open.DASH Widget 'beispiel-widget':

    -> Starting login attempt as 'zlls'...
    -> Logged in as Sebastian Zilles (zlls).
    -> Starting download of widget template 'UniSiegenWiNeMe/opendash-widget-template' into './beispiel-widget'...
    -> Download of 'UniSiegenWiNeMe/opendash-widget-template' finished.
    -> Initialization of 'beispiel-widget' finished.

$ cd beispiel-widget
```

### Widget builden

```
$ opendash widget:build

  Build open.DASH Widget.
    -> Finish open.DASH Widget Build.
```

### Template Datei Struktur

Die Datei Struktur sieht wie folgt aus:

```
├── src/
│   ├── widget/
│   │   ├── widget.controller.js
│   │   ├── widget.template.html
│   │   └── widget.scss
│   ├── settings/
│   │   ├── settings.controller.js
│   │   ├── settings.template.html
│   │   └── settings.scss
│   ├── assets/
│   │   └── ...
│   ├── index.js
│   └── presets.js
├── build/
│   └── ...
├── README.md
└── package.json
```

### Widget/Settings Controller

Die Entwickler von Angularjs empfehlen in Components auf das modifizieren des DOMs und den direkten Zugriff auf $scope zu verzichten.

Es ist trotzdem möglich, indem `$element` und `$scope` injected werden, sollte aber unbedingt vermieden werden. 

Ein Beispiel für einen Controller in [ES6 Schreibweise](http://es6-features.org/#ClassDefinition):

```js
export default class WidgetController {

  // ES6 Schreibweise für WidgetController.$inject = [];
  // Siehe: https://docs.angularjs.org/guide/di#-inject-property-annotation
  static $inject = ['od.adapter.service', '$element', '$scope'];

  // Konstruktor der bei Initialisierung eines Widgets aufgerufen wird.
  // Wichtig zu wissen: Wenn ein Widget erstellt wird, wird für jede Instanz
  // eines Widgets eine neue Instanz des Controllers erstellt.
  constructor($adapter, $element, $scope) {

    // Wichtig zu wissen: Bei der ES6 Schreibweise für Klassen müssen Parameter
    // des Konstruktors an this gebunden werden, damit sie in anderen Methoden
    // zur Verfügung stehen.
    this.$adapter = $adapter;

    // Ein gutes Pattern ist es, wenn in einem Konstruktor nicht zu viel Logik
    // steckt und statt dessen eine init() Methode aufgerufen wird.
    this.init();
  }

  init() {
      // ...
  }

  beispielMethode() {
      // ...
  }
}
```
#### Ladeanimation

Bei dem Widget Controller muss das `loading` Attribut auf `false` gesetzt werden, sobald alles geladen ist.

```js
this.loading = false;
```

### Widget/Settings Template


```html
<p>
    In einer Template Datei, kann ganz normales HTML mit Angular Flavor benutzt werden.
</p>
<p>
    Auf den Controller kann wie folgt zugegriffen werden: {{ $ctrl.attribute }}.
</p>
<p>
    $ctrl bietet somit Zugriff auf die Instanz des Controllers.
</p>
```

### Widget/Settings Styles

In Templates sollte aus verschieden Gründen (Minimierung / Wartbarkeit / fehlender Pre-/Postprozessor) auf die Verwendung von `<style>` Tags verzichtet werden.

Inline CSS ist in bestimmten Szenarien ok, ich schließe mich der [Meinung auf StackOverflow](http://stackoverflow.com/questions/2612483/whats-so-bad-about-in-line-css#answers) an.

Die Style Dateien sind [SCSS](http://sass-lang.com/) Dateien, in ihnen kann in den meisten Fällen bedenkenlos normales CSS benutzt werden oder auf Features von [SCSS](http://sass-lang.com/) benutzt werden.

Die Styles werden automatisch mit dem Element Namen über Nesting geprefixt.

Beispiel:

Der Name des Widgets ist `test-widget`. Die Selektoren der Widget Style Datei werden also mit `od-widget-test-widget` geprefixt und die Widget Settings Style Datei wird mit `od-widget-test-widget-settings` geprefixt.