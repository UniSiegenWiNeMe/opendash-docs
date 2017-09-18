# Customize your open.DASH Instance

You can customize your open.DASH instance using the [od.env.service](/services/env.md).

## Official Configs

### OD-EUD-SUPPORTED-SENSORS

Overwrite the list of sensor types supported by the EUD service. You have to supply an array of objects. The objects should have at least a `type` property, which holds the type to check against an [OpenDashDataItem](/classes/data-item.md) and a `label` property, which will be shown in the EUD Editor.

#### Example

```js
// app.js
instance.env('OD-EUD-SUPPORTED-SENSORS', [
  {
    type: 'custom-sensor-type',
    label: 'Custom Sensor',
  },
]);
```