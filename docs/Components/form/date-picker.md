# date-picker

:::::VerticalSplit{layout="middle"}
::::VerticalSplitItem
The date-picker component provides the functionality to select specific dates, times, or a combination of both. Date/time must be ***input*** in [ISO Format](https://www.iso.org/iso-8601-date-and-time-format.html#:~\:text=Therefore%2C%20the%20order%20of%20the,27%2018%3A00%3A00.000.). You can configure how the date/time is displayed in the form by formatting the ***output***.

:::hint{type="info"}
The `date-picker` component can be used independently or within a `form` component, each offering distinct benefits. As a standalone, it provides flexibility for isolated usage without requiring a form structure. When wrapped in a form, it leverages the form’s instanceId, enabling better coordination and usability when managing multiple fields in a jig.
:::
::::

:::VerticalSplitItem
![Date Picker ](https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-EMmv_RApEz18txt2YEbDK-20250318-111938.png "Date Picker ")
:::
:::::

## Configuration options

Some properties are common to all components, see [Common component properties]() for a list and their configuration options.

<table isTableHeaderOn="true" selectedColumns="" selectedRows="" selectedTable="false" columnWidths="132">
  <tr>
    <td selected="false" align="left">
      <p><strong>Core structure</strong></p>
    </td>
    <td selected="false" align="left">
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>instanceId</code></p>
    </td>
    <td selected="false" align="left">
      <p>The unique identifier for the date-picker field that can be referenced elsewhere. This is useful when saving the date to a datasource.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>label</code></p>
    </td>
    <td selected="false" align="left">
      <p>Provide a label to guide people on the what they selecting, for example, date of birth or start date.</p>
    </td>
  </tr>
</table>

<table isTableHeaderOn="true" selectedColumns="" selectedRows="" selectedTable="false" columnWidths="213">
  <tr>
    <td selected="false" align="left">
      <p><strong>Other options</strong></p>
    </td>
    <td selected="false" align="left">
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>color</code></p>
    </td>
    <td selected="false" align="left">
      <p>Select a color from the  to change the color of the field and label based on a <code>when</code> condition. First evaluated to <code>true</code> will be used.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>errorText</code></p>
    </td>
    <td selected="false" align="left">
      <p>Provide text message to display when field's value is not valid. The message is displayed in <code>isNegative</code> style (red). Use an expression to determine when to show the field.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>format</code></p>
    </td>
    <td selected="false" align="left">
      <p>Select the format of the date/time:
      LT - 3:28 PM
      LTS - 3:28:57 PM
      LLLL - Thursday, March 3, 2024 3:28 PM
      LLL - March 3, 2024 3:28 PM
      LL - March 3, 2024 (default)
      L - 03/03/2024
      l - 3/3/2024
      ll -  Mar 3, 2024
      lll - Mar 3, 2024 3:28 PM
      llll - Thu, Mar 3, 2024 3:28 PM
      HH:mm - 15:28</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>helperText</code></p>
    </td>
    <td selected="false" align="left">
      <p><code>helperText</code> is displayed only when there is no <code>errorText</code> property configured as <code>errorText</code> takes priorty.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>icon</code></p>
    </td>
    <td selected="false" align="left">
      <p>Add an icon to the field. See  for more information on adding icons.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>isRequired</code></p>
    </td>
    <td selected="false" align="left">
      <p>The default setting is <code>true</code> making the field required, useful when used in form submission. Set to <code>false</code> the field is not required and the field is marked (optional).</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>isIgnored</code></p>
    </td>
    <td selected="false" align="left">
      <p>Set to <code>true</code>, the field is ignored when submitting the form.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>isHidden</code></p>
    </td>
    <td selected="false" align="left">
      <p>Set to <code>true</code>, hides the field on the form. Use an expression to determine when to hide the field.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>initialValue</code></p>
    </td>
    <td selected="false" align="left">
      <p>Initial value for the field. You can use this to preset the value, so user do not need to change the value and can use this as the default. Using the <code>reset-state</code> action with <code>initialValues</code> does not clear the field, it resets the date back to it's <code>initialValue</code>.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>isOptionalLabelHidden</code></p>
    </td>
    <td selected="false" align="left">
      <p>If the field is optional (by setting <code>isRequired</code> to <code>false</code>) , setting the <code>isOptionalLabelHidden</code> property to <code>true</code> turns off/removes the (optional) text in the label.This property works in combination with <code>isRequired: false</code>.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>isAutoFocused</code></p>
    </td>
    <td selected="false" align="left">
      <p>By default this field is set to <code>false</code>, use <code>true</code> to get focus immediately after it is displayed.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>maximum</code></p>
    </td>
    <td selected="false" align="left">
      <p>Set a maximum time range f date/ time (UTC time). For example, "2022-04-22 14:00" or "2022-04-22" or "20:00" in case of type "time".
      <code>Maximum</code> on Android only works with <code>date</code> mode because TimePicker does not support this option.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>minimum</code></p>
    </td>
    <td selected="false" align="left">
      <p>Set a minimum time range for date/ time (UTC time). For example. "2022-04-22 05:00" or "2022-04-22" or "08:00" in case of type "time".
      <code>Minimum</code> on Android  only works with <code>date</code> mode because  the TimePicker does not support this option.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>mode</code></p>
    </td>
    <td selected="false" align="left">
      <p>By default the mode is set to <code>date</code>.
      Use <code>dateTime</code> to show a date and time picker.
      Use <code>time</code> to only show a time picker.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>nextProperty</code></p>
    </td>
    <td selected="false" align="left">
      <p>Name of the next property to receive focus in the form when using submit on a virtual keyboard.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>style</code></p>
    </td>
    <td selected="false" align="left">
      <p><code>isPositive</code> - field shows a positive icon (green tick)
      <code>isBusy</code> - Displays a spinner in the right hand side of the field to show that the field is busy.
      <code>isDisabled</code> - Set to <code>true</code> disables the date-picker field, preventing the picker screen from popping up.
      <code>flex</code> - adjust the size of the field.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>value</code></p>
    </td>
    <td selected="false" align="left">
      <p>The value to display in the field. <code>Text</code> field is a controlled component, which means the internal value will be forced to match a UTC time, if it cannot an Invalid date error displays.</p>
    </td>
  </tr>
</table>

<table isTableHeaderOn="true" selectedColumns="" selectedRows="" selectedTable="false">
  <tr>
    <td selected="false" align="left">
      <p><strong>Action</strong></p>
    </td>
    <td selected="false" align="left">
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>onChange</code></p>
    </td>
    <td selected="false" align="left">
      <p>Select an action to execute when the date-picker component's  value is changed.</p>
    </td>
  </tr>
</table>

<table isTableHeaderOn="true" selectedColumns="" selectedRows="" selectedTable="false" columnWidths="218,120">
  <tr>
    <td selected="false" align="left">
      <p><strong>State Configuration</strong></p>
    </td>
    <td selected="false" align="left">
      <p><strong>Key</strong></p>
    </td>
    <td selected="false" align="left">
      <p><strong>Notes</strong></p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>=@ctx.component.state.</code></p>
    </td>
    <td selected="false" align="left">
      <p>value</p>
    </td>
    <td selected="false" align="left">
      <p>State is the variable of the component.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>=@ctx.solution.state.</code></p>
    </td>
    <td selected="false" align="left">
      <p>activeItemId
      now</p>
    </td>
    <td selected="false" align="left">
      <p>Global state variable that can be used throughout the solution.</p>
    </td>
  </tr>
</table>

## Considerations

- The `date-picker` component requires dates to be input in an ISO format when statically specified or from a datasource.
- The `format` property is set to show for the outputs of the field and are ready only.
- For setting the date format taking into account time zones see [Expressions - cheatsheet](https://docs.jigx.com/expressions-cheatsheet) for example expressions.

## Examples and code snippets

:::::ExpandableHeading
### Date picker for selecting a specific date

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
![Date picker- input + output](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/lZp4wvPnnYUd7YdOAlSDB_cc-datepicker.png "Date picker- input + output")
:::

:::VerticalSplitItem
In this an example the date-picker allows you to select a specific date in ISO format (input). Using the `mode` property set to `L` ensures the date is displayed in the field (output) as  MM/DD/YYYY.

**Example:**

See the full example using static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/date-picker/date-picker-date.jigx).
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

See the full example using static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/date-picker/date-picker-time.jigx).
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
### Date picker with a minimum and maximum date

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
This example shows how to set a specific date range using the `minimum` and `maximum` properties.
:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/EVYL9aHItYCcYfcSj2J1T_cc-date-min-max.PNG" size="60" position="center" caption="Date range with minimum & maximum" alt="Date range with minimum & maximum" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/EVYL9aHItYCcYfcSj2J1T_cc-date-min-max.PNG" width="800" height="1613" darkWidth="800" darkHeight="1613"}
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

## See also

- [State](https://docs.jigx.com/state)

