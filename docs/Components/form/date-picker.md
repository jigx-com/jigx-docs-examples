---
title: date-picker
slug: 8ZlB-date-picker
description: Learn how to use the versatile and customizable "Date Picker" component to seamlessly select specific dates or hours. Explore its configuration options like instanceId, label, format, and mode, and discover how to set maximum and minimum ranges for dates 
createdAt: Thu Jun 09 2022 19:28:21 GMT+0000 (Coordinated Universal Time)
updatedAt: Tue Mar 18 2025 11:22:55 GMT+0000 (Coordinated Universal Time)
---

::::VerticalSplit{layout="left"}
:::VerticalSplitItem
The date-picker component provides the functionality to select specific dates, times, or a combination of both. Date/time must be ***input*** in <a href="https://www.iso.org/iso-8601-date-and-time-format.html#:~:text=Therefore%2C%20the%20order%20of%20the,27%2018%3A00%3A00.000." target="_blank">ISO format</a>. You can configure how the date/time is displayed in the form by formatting the ***output***.
:::

:::VerticalSplitItem
![Date Picker ](https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-EMmv_RApEz18txt2YEbDK-20250318-111938.png "Date Picker ")
:::
::::

## Configuration options

Some properties are common to all components, see [Common component properties](docId\:LLnTD-rxe8FmH7WpC5cZb) for a list and their configuration options.

| ### Core structure | ****                                                                                                                                   |
| ------------------ | -------------------------------------------------------------------------------------------------------------------------------------- |
| `instanceId`       | The unique identifier for the date-picker field that can be referenced elsewhere. This is useful when saving the date to a datasource. |
| `label`            | Provide a label to guide people on the what they selecting, for example, date of birth or start date.                                  |

| ### Other options       | ****                                                                                                                                                                                                                                                                                                                     |
| ----------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `color`                 | Select a color from the [Jigx color palette]() to change the color of the field and label based on a `when` condition. First evaluated to `true` will be used.                                                                                                                                                           |
| `errorText`             | Provide text message to display when field's value is not valid. The message is displayed in `isNegative` style (red). Use an expression to determine when to show the field.                                                                                                                                            |
| `format`                | Select the format of the date/time:<br />* LT - 3:28 PM
* LTS - 3:28:57 PM
* LLLL - Thursday, March 3, 2024 3:28 PM
* LLL - March 3, 2024 3:28 PM
* LL - March 3, 2024 (default)
* L - 03/03/2024
* l - 3/3/2024
* ll -  Mar 3, 2024
* lll - Mar 3, 2024 3:28 PM
* llll - Thu, Mar 3, 2024 3:28 PM
* HH\:mm - 15:28      |
| `helperText`            | `helperText` is displayed only when there is no `errorText` property configured as `errorText` takes priorty.                                                                                                                                                                                                            |
| `icon`                  | Add an icon to the field. See [Jigx icons]() for more information on adding icons.                                                                                                                                                                                                                                       |
| `isRequired`            | The default setting is `true` making the field required, useful when used in form submission. Set to `false` the field is not required and the field is marked (optional).                                                                                                                                               |
| `isIgnored`             | Set to `true`, the field is ignored when submitting the form.                                                                                                                                                                                                                                                            |
| `isHidden`              | Set to `true`, hides the field on the form. Use an expression to determine when to hide the field.                                                                                                                                                                                                                       |
| `initialValue`          | Initial value for the field. You can use this to preset the value, so user do not need to change the value and can use this as the default. Using the `reset-state` action with `initialValues` does not clear the field, it resets the date back to it's `initialValue`.                                                |
| `isOptionalLabelHidden` | If the field is optional (by setting `isRequired` to `false`) , setting the `isOptionalLabelHidden` property to `true` turns off/removes the (optional) text in the label.This property works in combination with `isRequired: false`.                                                                                   |
| `isAutoFocused`         | By default this field is set to `false`, use `true` to get focus immediately after it is displayed.                                                                                                                                                                                                                      |
| `maximum`               | Set a maximum time range f date/ time (UTC time). For example, "2022-04-22 14:00" or "2022-04-22" or "20:00" in case of type "time".&#xA;`Maximum` on Android only works with `date` mode because TimePicker does not support this option.                                                                               |
| `minimum`               | Set a minimum time range for date/ time (UTC time). For example. "2022-04-22 05:00" or "2022-04-22" or "08:00" in case of type "time".&#xA;`Minimum` on Android  only works with `date` mode because  the TimePicker does not support this option.                                                                       |
| `mode`                  | By default the mode is set to `date`.  &#xA;Use `dateTime `to show a date and time picker.&#xA;Use `time` to only show a time picker.                                                                                                                                                                                    |
| `nextProperty`          | Name of the next property to receive focus in the form when using submit on a virtual keyboard.                                                                                                                                                                                                                          |
| `style`                 | `isPositive` - field shows a positive icon (green tick)&#xA;`isBusy` - Displays a spinner in the right hand side of the field to show that the field is busy. &#xA;`isDisabled` - Set to `true` disables the date-picker field, preventing the picker screen from popping up.&#xA;`flex` - adjust the size of the field. |
| `value`                 | The value to display in the field. `Text` field is a controlled component, which means the internal value will be forced to match a UTC time, if it cannot an Invalid date error displays.                                                                                                                               |

| ### Action | ****                                                                            |
| ---------- | ------------------------------------------------------------------------------- |
| `onChange` | Select an action to execute when the date-picker component's  value is changed. |

| ### State Configuration  | **Key**              | **Notes**                                                         |
| ------------------------ | -------------------- | ----------------------------------------------------------------- |
| `=@ctx.component.state.` | value                | - State is the variable of the component.                         |
| `=@ctx.solution.state.`  | activeItemId&#xA;now | * Global state variable that can be used throughout the solution. |

## Considerations

- The `date-picker` component requires dates to be input in an ISO format when statically specified or from a datasource.
- The `format` property is set to show for the outputs of the field and are ready only.
- For setting the date format taking into account time zones see [Expressions - cheatsheet]() for example expressions.

## Examples and code snippets ****

:::::ExpandableHeading
### Date picker for selecting a specific date

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
![Date picker- input + output](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/lZp4wvPnnYUd7YdOAlSDB_cc-datepicker.png "Date picker- input + output")
:::

:::VerticalSplitItem
In this an example the date-picker allows you to select a specific date in ISO format (input). Using the `mode` property set to `L` ensures the date is displayed in the field (output) as  MM/DD/YYYY.

**Example:**

See the full example using static data in <a href="https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/date-picker/date-picker-date.jigx" target="_blank">GitHub</a>.
:::
::::

:::CodeblockTabs
date-picker (static)

```yaml
children:
  - type: component.form
    options:
      children:
        - type: component.date-picker
          instanceId: date
          options:
            label: Select a date
            format: L
```
:::
:::::

:::::ExpandableHeading
### Date picker for selecting time

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
![Time selector - input + output](https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-WoqqTGRt53R_ymb-bdSGs-20250318-112250.png "Time selector - input + output")
:::

:::VerticalSplitItem
In is example, only time can be selected. This is accomplished by setting the `mode` property to `time` (input). The time is formatted to display (output) as HH\:mm in the field by using the `format: HH:mm` property.

**Example:**

See the full example using static data in <a href="https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/date-picker/date-picker-time.jigx" target="_blank">GitHub</a>.
:::
::::

:::CodeblockTabs
date-picker (static)

```yaml
children:
  - type: component.form
    options:
      children:
        - type: component.date-picker
          instanceId: time
          options:
            label: Select a time
            mode: time
            format: HH:mm
```
:::
:::::

:::::ExpandableHeading
### Date picker with a minimum and maximum date&#x20;

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
This example shows how to set a specific date range using the `minimum` and `maximum` properties.&#x20;
:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/EVYL9aHItYCcYfcSj2J1T_cc-date-min-max.PNG" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/EVYL9aHItYCcYfcSj2J1T_cc-date-min-max.PNG" size="60" width="1240" height="2500" position="center" caption="Date range with minimum & maximum" alt="Date range with minimum & maximum"}
:::
::::

:::CodeblockTabs
date-picker-min-max

```yaml
title: Date picker
type: jig.default
children:
  - type: component.form
    options:
      children:
        - type: component.date-picker
          instanceId: date
          options:
            minimum: 03/20/2024
            maximum: 03/27/2024
            format: L
            label: Select a date
```
:::
:::::

## **See also**

- [State]()

