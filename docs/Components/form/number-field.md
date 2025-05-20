# number-field

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
Number fields in forms simplify the process of entering numerical information. They feature built-in validation to ensure only valid numbers are input. This optimizes user experience by automatically presenting a numeric keypad, facilitating quicker and more accurate data entry.

The component can only be used in a [jig.default](<./../../Jig Types/jig_default.md>) inside of a [form](./../form.md) component for an input of a numeric value.
:::

:::VerticalSplitItem
::Image[]{alt="Number Field Preview" src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/KwkJpkkJwrkIiXLBfWABo_number.png" size="84" caption="Number Field Preview" position="center" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/KwkJpkkJwrkIiXLBfWABo_number.png"}
:::
::::

:::hint{type="info"}
The `number-field` component can be used independently or within a `form` component, each offering distinct benefits. As a standalone, it provides flexibility for isolated usage without requiring a form structure. When wrapped in a form, it leverages the form’s instanceId, enabling better coordination and usability when managing multiple fields in a jig.
:::

## Configuration options

Some properties are common to all components, see [Common component properties](docId\:LLnTD-rxe8FmH7WpC5cZb) for a list and their configuration options.

| **Core structure** |                                                                                                              |
| ------------------ | ------------------------------------------------------------------------------------------------------------ |
| `instanceId`       | The unique identifier for the number-field.                                                                  |
| `label`            | Provide a label/name for the number-field. 'Label' is displayed as a placeholder when no value is specified. |

| **Other options**                 |                                                                                                                                                                                                                                                                                                                                                                                                                              |
| --------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `color`                           | Sets the color of the number-field property based on conditions by using the `when` property. First evaluated to `true` will be used. Choose a color from the provided color palette. Default color is grey if the property is not specified in the YAML. See the list of available colors in [Jigx color palette](#).                                                                                                       |
| `errorText`                       | Add text, string, or expressions to show text under the number-field indicating an error/invalid value in the field. Text is shown in `isNegative` (red) styling with a red exclamation icon on the right.                                                                                                                                                                                                                   |
| `format`                          | Text Format of the value entered. Format is enabled only if field is configured to disabled.  `style: isDisabled: true`                                                                                                                                                                                                                                                                                                      |
| `helperText`                      | Add text, string, or expressions to guide users by showing text under the number-field. Helper text is displayed only when there is no errorText.                                                                                                                                                                                                                                                                            |
| `icon`                            | Add an icon to the number-field, for example a dollar icon. The icon apprears on the far right of the field.  A list of icons is available. See [Jigx icons](#) for more information.                                                                                                                                                                                                                                        |
| `initialValue`                    | The `initialValue` is the value that will be displayed in the number-field when the form is initially loaded. You can use this property to preset the field with a default number so that you do not have to manually select it. Using the `reset-state` action with `initialValues` does not clear the field, it resets the field back to it's `initialValue`.                                                              |
| `isAutoFocused`                   | If `true` the number-field will get focus immediately after the form is displayed and the number keyboard will be opened automatically.                                                                                                                                                                                                                                                                                      |
| `isHidden`                        | If `true` the number-field will be hidden on the form. If set to `false` the field will be shown.                                                                                                                                                                                                                                                                                                                            |
| `isIgnored`                       | When `true`, the field will be ignored when submitting the form and the content will not be stored.                                                                                                                                                                                                                                                                                                                          |
| `isOptionalLabelHidden`           | If the field is optional you can turn off the "(optional)" label by setting this field to `true`. This property works in combination with `isRequired: false`.                                                                                                                                                                                                                                                               |
| `isRequired`                      | Set to `true` when the field is required. Useful when you use it in form submission as the submit button remains disabled until the number-field has a numeric input. Set to `false` the number-field is optional and will have (optional) in the label.                                                                                                                                                                     |
| `isReturnKeyEnabledAutomatically` | When set to `true`, the keyboard disables the return/done key when there is no number and automatically enables it when there is a number. The default value is `false`.                                                                                                                                                                                                                                                     |
| `isSensitive`                     | If set to `true`, the number input obscures the number entered so that sensitive numbers stay secure. For example, bank card account details or salary details.                                                                                                                                                                                                                                                              |
| `isTextClearedOnFocus`            | When set to `true`, the number-field is automatically cleared when editing begins.                                                                                                                                                                                                                                                                                                                                           |
| `KeyboardType`                    | Determines which keyboard to open. Default is number-pad. You can select one of the following:&#xA;- `decimal-pad`&#xA;- `number-pad`&#xA;- `numeric`                                                                                                                                                                                                                                                                        |
| `minimum`                         | Set the minimum number limit. Used with the `maximum` property allows you to set an available number range.                                                                                                                                                                                                                                                                                                                  |
| `maximum`                         | Set the maximum number limit. Used with the `minimum` property allows you to set an available number range.                                                                                                                                                                                                                                                                                                                  |
| `nextProperty`                    | Name of the property you want to focus next in the form when you use return/next on a keyboard.                                                                                                                                                                                                                                                                                                                              |
| `stepper`                         | When the stepper `isEnabled` property is set to `true` a - and + icon is added to the right of the number field allowing you to add or subtract numbers. Use the `value` property to determine the numerical increments when the icon is pressed. For example, `value: 5` will increase the number-field by 5 each time the + icon is pressed. The stepper property is great for an invoicing or order form.                 |
| `style`                           | The following property settings are available:&#xA;- `flex` - Flex property if rendered inside row.&#xA;- `isBusy` - Displays spinner on right side of field. It removes any  configured icon.&#xA;- `isDisabled` - disables the number-field preventing any input text.&#xA;- `isPositive` - a green icon displays on the right of the number-field.&#xA;More than one can be true. It will be evaluated based on priority. |
| `value`                           | The value to show in the number-field when the form initially loads. This can be combined with the `isDisable` style to preset the value that cannot be edited on the form.                                                                                                                                                                                                                                                  |

| **Actions** |                                                                                                                                              |
| ----------- | -------------------------------------------------------------------------------------------------------------------------------------------- |
| `onChange`  | The action is triggered when the content in the number-field is changed. Use IntelliSense (ctrl+space) to see the list of available actions. |

| **State Configuration**  | **Key**              | **Notes**                                                       |
| ------------------------ | -------------------- | --------------------------------------------------------------- |
| `=@ctx.component.state.` | value                | State is the variable of the component.                         |
| `=@ctx.solution.state.`  | activeItemId&#xA;now | Global state variable that can be used throughout the solution. |

## Examples and code snippets

::::ExpandableHeading
### Number Field on Form

::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/ZehuKgdayEDjBvecia7S7_cc-numberfield.png" size="82" position="center" caption="Form with number field" alt="Form with number fields" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/ZehuKgdayEDjBvecia7S7_cc-numberfield.png"}

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

- [State](#)

