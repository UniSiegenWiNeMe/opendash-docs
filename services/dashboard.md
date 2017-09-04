# Dashboard Service (od.dashboard.service)

The Dashboard Service allows you to:
- Get a list of all dashboards.
- Switch between dashboards.
- Modify the current dashboard by creating, deleting and editing widgets.

**Contents:**
<!-- TOC depthFrom:2 depthTo:3 -->

- [Usage](#usage)
  - [$dashboard.dasboards](#dashboarddasboards)
  - [$dashboard.changeDashboard(name: String)](#dashboardchangedashboardname-string)
  - [$dashboard.deleteCurrentDashboard()](#dashboarddeletecurrentdashboard)
  - [$dashboard.addWidget(widget: OpenDashWidget)](#dashboardaddwidgetwidget-opendashwidget)
  - [$dashboard.onWidgetResize(callback: Function)](#dashboardonwidgetresizecallback-function)

<!-- /TOC -->

## Usage

Use the Dashboard Service by injecting `od.dashboard.service` as an Angular Service. We suggest using `$dashboard` as a name for the variable.

Example:
```js
class controller {

  static $inject = ['od.dashboard.service'];

  constructor($dashboard) {
    // ...
  }
}
```

### $dashboard.dasboards

An array listing all existing dashboards.

### $dashboard.changeDashboard(name: String)

Will change the dashboard depending on the given name.

#### Response

Nothing will happen, if you try to change to the current dashboard.

If a dashboard with the given name exists, the existing dashboard will be loaded, otherwise the dashboard will be created. Either way the browser will do a reload.

### $dashboard.deleteCurrentDashboard()

Use this method to delete the current dashboard.

#### Response

The browser will reload.

### $dashboard.addWidget(widget: OpenDashWidget)

Adds a widget to the current dashboard.

#### Parameter

**widget** - Object which looks like this:

```js
{
  name: 'Widget Name', // Display name of the widget
  type: 'widget-type', // Type of the widget
  grid: [0,0,0,0], // Height, Width, Y- und X- coordinate. Should not be set.
  config: {}, // Config which will be used by the widget.
}
```

#### Response

Returns `true` if the widget was added to the dashboard, `false` if not.

### $dashboard.onWidgetResize(callback: Function)

Deprecated - use the `od.event.service` instead.

```js
$event.on('od-widgets-resize', callback);
```