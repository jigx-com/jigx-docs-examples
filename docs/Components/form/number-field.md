# number-field

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
Number fields in forms simplify the process of entering numerical information. They feature built-in validation to ensure only valid numbers are input. This optimizes user experience by automatically presenting a numeric keypad, facilitating quicker and more accurate data entry.

The component can only be used in a [jig.default](<./../../Jig Types/jig_default.md>) inside of a [form](./../form.md) component for an input of a numeric value.
:::

:::VerticalSplitItem
::Image[]{alt="Number Field Preview" src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/KwkJpkkJwrkIiXLBfWABo_number.png" size="84" caption="Number Field Preview" position="center" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/KwkJpkkJwrkIiXLBfWABo_number.png" width="800" height="495" darkWidth="800" darkHeight="495"}
:::
::::

:::hint{type="info"}
The `number-field` component can be used independently or within a `form` component, each offering distinct benefits. As a standalone, it provides flexibility for isolated usage without requiring a form structure. When wrapped in a form, it leverages the form’s instanceId, enabling better coordination and usability when managing multiple fields in a jig.
:::

## Configuration options

Some properties are common to all components, see [Common component properties]() for a list and their configuration options.

| **Core structure** |                                                                                                              |
| ------------------ | ------------------------------------------------------------------------------------------------------------ |
| `instanceId`       | The unique identifier for the number-field.                                                                  |
| `label`            | Provide a label/name for the number-field. 'Label' is displayed as a placeholder when no value is specified. |

<table isTableHeaderOn="true" selectedColumns="" selectedRows="" selectedTable="false" columnWidths="296">
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
      <p>Sets the color of the number-field property based on conditions by using the <code>when</code> property. First evaluated to <code>true</code> will be used. Choose a color from the provided color palette. Default color is grey if the property is not specified in the YAML. See the list of available colors in .</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>errorText</code></p>
    </td>
    <td selected="false" align="left">
      <p>Add text, string, or expressions to show text under the number-field indicating an error/invalid value in the field. Text is shown in <code>isNegative</code> (red) styling with a red exclamation icon on the right.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>format</code></p>
    </td>
    <td selected="false" align="left">
      <p>Text Format of the value entered. Format is enabled only if field is configured to disabled.  <code>style: isDisabled: true</code></p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>helperText</code></p>
    </td>
    <td selected="false" align="left">
      <p>Add text, string, or expressions to guide users by showing text under the number-field. Helper text is displayed only when there is no errorText.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>icon</code></p>
    </td>
    <td selected="false" align="left">
      <p>Add an icon to the number-field, for example a dollar icon. The icon apprears on the far right of the field.  A list of icons is available. See  for more information.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>initialValue</code></p>
    </td>
    <td selected="false" align="left">
      <p>The <code>initialValue</code> is the value that will be displayed in the number-field when the form is initially loaded. You can use this property to preset the field with a default number so that you do not have to manually select it. Using the <code>reset-state</code> action with <code>initialValues</code> does not clear the field, it resets the field back to it's <code>initialValue</code>.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>isAutoFocused</code></p>
    </td>
    <td selected="false" align="left">
      <p>If <code>true</code> the number-field will get focus immediately after the form is displayed and the number keyboard will be opened automatically.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>isHidden</code></p>
    </td>
    <td selected="false" align="left">
      <p>If <code>true</code> the number-field will be hidden on the form. If set to <code>false</code> the field will be shown.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>isIgnored</code></p>
    </td>
    <td selected="false" align="left">
      <p>When <code>true</code>, the field will be ignored when submitting the form and the content will not be stored.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>isOptionalLabelHidden</code></p>
    </td>
    <td selected="false" align="left">
      <p>If the field is optional you can turn off the "(optional)" label by setting this field to <code>true</code>. This property works in combination with <code>isRequired: false</code>.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>isRequired</code></p>
    </td>
    <td selected="false" align="left">
      <p>Set to <code>true</code> when the field is required. Useful when you use it in form submission as the submit button remains disabled until the number-field has a numeric input. Set to <code>false</code> the number-field is optional and will have (optional) in the label.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>isReturnKeyEnabledAutomatically</code></p>
    </td>
    <td selected="false" align="left">
      <p>When set to <code>true</code>, the keyboard disables the return/done key when there is no number and automatically enables it when there is a number. The default value is <code>false</code>.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>isSensitive</code></p>
    </td>
    <td selected="false" align="left">
      <p>If set to <code>true</code>, the number input obscures the number entered so that sensitive numbers stay secure. For example, bank card account details or salary details.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>isTextClearedOnFocus</code></p>
    </td>
    <td selected="false" align="left">
      <p>When set to <code>true</code>, the number-field is automatically cleared when editing begins.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>KeyboardType</code></p>
    </td>
    <td selected="false" align="left">
      <p>Determines which keyboard to open. Default is number-pad. You can select one of the following:</p>
      <ul>
      <li><code>decimal-pad</code></li>
      <li><code>number-pad</code></li>
      <li><code>numeric</code></li>
      </ul>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>minimum</code></p>
    </td>
    <td selected="false" align="left">
      <p>Set the minimum number limit. Used with the <code>maximum</code> property allows you to set an available number range.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>maximum</code></p>
    </td>
    <td selected="false" align="left">
      <p>Set the maximum number limit. Used with the <code>minimum</code> property allows you to set an available number range.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>nextProperty</code></p>
    </td>
    <td selected="false" align="left">
      <p>Name of the property you want to focus next in the form when you use return/next on a keyboard.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>stepper</code></p>
    </td>
    <td selected="false" align="left">
      <p>When the stepper <code>isEnabled</code> property is set to <code>true</code> a - and + icon is added to the right of the number field allowing you to add or subtract numbers. Use the <code>value</code> property to determine the numerical increments when the icon is pressed. For example, <code>value: 5</code> will increase the number-field by 5 each time the + icon is pressed. The stepper property is great for an invoicing or order form.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>style</code></p>
    </td>
    <td selected="false" align="left">
      <p>The following property settings are available:</p>
      <ul>
      <li><code>flex</code> - Flex property if rendered inside row.</li>
      <li><code>isBusy</code> - Displays spinner on right side of field. It removes any  configured icon.</li>
      <li><code>isDisabled</code> - disables the number-field preventing any input text.</li>
      <li><code>isPositive</code> - a green icon displays on the right of the number-field.</li>
      </ul>
      <p>More than one can be true. It will be evaluated based on priority.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>value</code></p>
    </td>
    <td selected="false" align="left">
      <p>The value to show in the number-field when the form initially loads. This can be combined with the <code>isDisable</code> style to preset the value that cannot be edited on the form.</p>
    </td>
  </tr>
</table>

<table isTableHeaderOn="true" selectedColumns="" selectedRows="" selectedTable="false" columnWidths="207">
  <tr>
    <td selected="false" align="left">
      <p><strong>Actions</strong></p>
    </td>
    <td selected="false" align="left">
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>onChange</code></p>
    </td>
    <td selected="false" align="left">
      <p>The action is triggered when the content in the number-field is changed. Use IntelliSense (ctrl+space) to see the list of available actions.</p>
    </td>
  </tr>
</table>

<table isTableHeaderOn="true" selectedColumns="" selectedRows="" selectedTable="false" columnWidths="218,115">
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

## Examples and code snippets

::::ExpandableHeading
### Number Field on Form

::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/ZehuKgdayEDjBvecia7S7_cc-numberfield.png" size="82" position="center" caption="Form with number field" alt="Form with number fields" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/ZehuKgdayEDjBvecia7S7_cc-numberfield.png" width="800" height="805" darkWidth="800" darkHeight="805"}

The form use multiple `number-fields` property for numeric values with the following optional properties set:

1. `stepper` property to increase or decrease the number.
2. `color` property to color the label and number field purple.
3. `icon` property to show the number represents a currency in dollars.
4. `IntialValue` property preloads with a number when the form loads. The number is set using an expression.
5. `isSensitive` property obsecures the numbers when entered in the field.
6. A combination of `minimum`, `maximum` and `errorText` are used to set limits with validation on the field.

**Examples:**

See the full example using static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/number-field/static-data/number-field.jigx).
See the full example using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/components/number-field/dynamic-data/number-field-dynamic.jigx).

:::CodeblockTabs
number-field (static)

```yaml
title: Number-field
type: jig.default

header:
  type: component.jig-header
  options:
    height: small
    children:
      type: component.image
      options:
        source:
          uri: https://images.unsplash.com/photo-1529078155058-5d716f45d604?q=80&w=1469&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D

children:
  - type: component.form
    instanceId: NumberForm
    options:
      children:
        - type: component.number-field
          instanceId: numberStepper
          options:
            label: Number with stepper
            stepper:
              isEnabled: true
              value: 1
        - type: component.number-field
          instanceId: numberColor
          options:
            color:
              - when: true
                color: color5
            label: Number with color
        - type: component.number-field
          instanceId: numberIcon
          options:
            icon: currency-dollar
            label: Number with icon
        - type: component.number-field
          instanceId: numberIntValue
          options:
            initialValue: =$number(5 * 2)
            label: Number with inital value from expression
        - type: component.number-field
          instanceId: numberSensitive
          options:
            isSensitive: true
            label: sensitive Number
        - type: component.number-field
          instanceId: numberLimits
          options:
            helperText: Minimum of 5 and maximum of 10 allowed
            minimum: 5
            maximum: 10
            label: Number with min, max and help text                        
```

number-field (dynamic)

```yaml
children:
  - type: component.form
    instanceId: number-form
    options:
      children: 
        - type: component.number-field
          instanceId: number
          options:
            label: Number 
            helperText: =@ctx.datasources.field-values.number
```
:::
::::

## See also

- [State](https://docs.jigx.com/state)

