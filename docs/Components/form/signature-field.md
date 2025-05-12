# signature-field

Simply draw your signature on your mobile screen to approve and proceed. This component can only be used in a [jig.default](<./../../Jig Types/jig_default.md>) inside of a [form](./../form.md) component for the input of a signature. It provides the experience of creating, uploading, and saving your eSignature in a few easy steps.

![Signature Field Preview](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/xFXGhidiImIpwwIhQy4kU_signature.png "Signature Field Preview")

## Configuration options

Some properties are common to all components, see [Common component properties](docId\:LLnTD-rxe8FmH7WpC5cZb) for a list and their configuration options.

| **Core structure** |                                                                                                                 |
| ------------------ | --------------------------------------------------------------------------------------------------------------- |
| `instanceId`       | The unique identifier for the signature-field component.                                                        |
| `label`            | Provide a label/name for the signature field. 'Label' is displayed as a placeholder when no value is specified. |

| **Other options**       |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| ----------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `color`                 | Sets the color of the signature field-based on conditions by using the `when` property. First evaluated to `true` will be used. Choose a color from the provided color palette. Default color is grey if the property is not specified in the YAML. See the list of available colors in [Jigx color palette](#).                                                                                                                                                                                                                                                   |
| `errorText`             | Add text, string, or expressions to show text under the signature-field  indicating an error/invalid value in the field. Text is shown in `isNegative` (red) styling with a red exclamation icon on the right.                                                                                                                                                                                                                                                                                                                                                     |
| `helperText`            | Add text, string, or expressions to guide users by showing text under the signature-field. Helper text is displayed only when there is no errorText.                                                                                                                                                                                                                                                                                                                                                                                                               |
| `icon`                  | Add an icon to the signature-field, for example a pen icon. The icon apprears on the far right of the field.  A list of icons is available. See [Jigx icons](#) for more information.                                                                                                                                                                                                                                                                                                                                                                              |
| `initialValue`          | The `initialValue` is the value that will be displayed in the signature-field when the form is initially loaded. You can use this property to preset the field with a default signature so that you do not have to manually select it or if you already have the person signature in a datasource you can use anexpresssion to return the intial signature. Tapping on the field allows the person to re-sign the form if required. Using the `reset-state` action with `initialValues` does not clear the field, it resets the field back to it's `initialValue`. |
| `isAutoFocused`         | If `true` the signature-field will get focus immediately after the form is displayed and the number keyboard will be opened automatically.                                                                                                                                                                                                                                                                                                                                                                                                                         |
| `isHidden`              | If `true` the signature-field will be hidden on the form. If set to `false` the field will be shown.                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| `isIgnored`             | When `true`, the field will be ignored when submitting the form and the content will not be stored.                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| `isOptionalLabelHidden` | If the field is optional you can turn off the "(optional)" label by setting this field to `true`. This property works in combination with `isRequired: false`.                                                                                                                                                                                                                                                                                                                                                                                                     |
| `isRequired`            | Set to `true` when the field is required. Useful when you use it in form submission as the submit button remains disabled until the signature has been applied. Set to `false` the signature-field is optional and will have (optional) in the label.                                                                                                                                                                                                                                                                                                              |
| `nextProperty`          | Name of the property you want to focus next in the form when you use return/next on a keyboard.                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| `style`                 | The following property settings are available:&#xA;- `flex` - Flex property if rendered inside row.&#xA;- `isBusy` - Displays spinner on right side of field. It removes any  configured icon.&#xA;- `isDisabled` - disables the signature property preventing any input.&#xA;- `isPositive` - a green icon displays on the right of the signature.&#xA;More than one can be true. It will be evaluated based on priority.                                                                                                                                         |
| `value`                 | The value to show in the signature-field when the form initially loads. This can be combined with the `isDisable` style to preset the value that cannot be edited on the form.                                                                                                                                                                                                                                                                                                                                                                                     |

| **Actions** |                                                                                                                                                 |
| ----------- | ----------------------------------------------------------------------------------------------------------------------------------------------- |
| `onChange`  | The action is triggered when the content in the signature-field is changed. Use IntelliSense (ctrl+space) to see the list of available actions. |

| **State Configuration**  | **Key**              | **Notes**                                                       |
| ------------------------ | -------------------- | --------------------------------------------------------------- |
| `=@ctx.component.state.` | value                | State is the variable of the component.                         |
| `=@ctx.solution.state.`  | activeItemId&#xA;now | Global state variable that can be used throughout the solution. |

## Examples and code snippets

:::::ExpandableHeading
### Signature Field on Form

::::VerticalSplit{layout="left"}
:::VerticalSplitItem
![Form signature](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/tCKu2RtpBmPBLyNyCEbL1_ofk8slzh8-djfwqstadycsignature-field.png "Form signature")
:::

:::VerticalSplitItem
The widget displays the signature input. After clicking on it, the user can create his/her eSignature.

**Example:**

See the full example in [GitHub]("https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/signature-field/signature-field.jigx).
:::
::::

:::CodeblockTabs
signature

```yaml
children:
  - type: component.form
    instanceId: new-customer-form
    options:
      children:
        - type: component.signature-field
          instanceId: signature
          options:
            label: Signature required
```
:::
:::::

## See also

- [State](#)

