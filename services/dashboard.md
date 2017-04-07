# Dashboard Service (od.dashboard.service)

Der Dashboard Service ist dazu da das Dashboard zu modifizieren, über diesen Service können Widgets hinzugefügt, gelöscht und bearbeitet werden. Außerdem ist es möglich zwischen verschiedenen Dashboards hin und her zu wechseln und die Daten des momentan ausgewählten Dashboards, sowie aller Dashboards einzusehen.

<!-- TOC -->

- [Dashboard Service (od.dashboard.service)](#dashboard-service-oddashboardservice)
  - [Nutzung](#nutzung)
    - [$dashboard.addWidget(widget)](#dashboardaddwidgetwidget)
      - [Parameter](#parameter)
      - [Rückgabe](#rückgabe)
    - [$dashboard.onWidgetResize(callback: Function)](#dashboardonwidgetresizecallback-function)
      - [Parameter](#parameter-1)
      - [Rückgabe](#rückgabe-1)

<!-- /TOC -->

## Nutzung

Der Dashboard Service kann benutzt werden indem `od.dashboard.service` über Angular injected wird. Es empfiehlt sich diesen dann mit dem Parameter Namen `$dashboard` zu benutzen.

Beispiel:

```js
class controller {

  static $inject = ['od.dashboard.service'];

  constructor($dashboard) {
    // ...
  }
}
```

### $dashboard.addWidget(widget)

Fügt ein Widget zum moment aktiven Dashboard hinzu.

#### Parameter

**widget** - Objekt das die Daten zum erstellen des Widgets speichert.

```js
{
  name: 'Widget Name', // Name der im Dashboard angezeigt wird.
  type: 'widget-type', // Typ von dem ein Widget erzeugt wird.
  grid: [0,0,0,0], // Höhe, Breite, Y- und X- Koordinate. Sollte nicht manuell gesetzt werden.
  config: {}, // Konfigurations Objekt, das an das Widget übergeben wird.
}
```

#### Rückgabe

Gibt `true` zurück.

### $dashboard.onWidgetResize(callback: Function)

Event Listener: Wenn ein Widget seine Größe ändert wird die übergebene Funktion ausgeführt

#### Parameter

**callback** - Funktion die ausgeführt wird, wenn sich die Größe eines Widgets ändert.

```js
$dashboard.onWidgetResize(() => {
  // Mache etwas..
});
```

#### Rückgabe

Gibt nichts zurück.