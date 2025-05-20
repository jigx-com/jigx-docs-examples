# email-field

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
Email fields in forms provide a user-friendly way to collect email addresses, incorporating validation to ensure data is entered correctly.

The `email-field` component can only be used in a [jig.default](<./../../Jig Types/jig_default.md>) inside of a [form](./../form.md) component for capturing an email address.
:::

:::VerticalSplitItem
![Email Field Preview](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/dSjO63W1F7TwFYsE8SIUK_cc-emailfield.png "Email Field Preview")
:::
::::

:::hint{type="info"}
The `email-field` component can be used independently or within a `form` component, each offering distinct benefits. As a standalone, it provides flexibility for isolated usage without requiring a form structure. When wrapped in a form, it leverages the form’s instanceId, enabling better coordination and usability when managing multiple fields in a jig.
:::

## Configuration options

Some properties are common to all components, see [Common component properties](docId\:LLnTD-rxe8FmH7WpC5cZb) for a list and their configuration options.

| **Core structure** |                                                                                                             |
| ------------------ | ----------------------------------------------------------------------------------------------------------- |
| `instanceId`       | The unique identifier for the email-field.                                                                  |
| `label`            | Provide a label/name for the email-field. 'Label' is displayed as a placeholder when no value is specified. |

| **Other options**                 |                                                                                                                                                                                                                                                                                                                                                                                                                            |
| --------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `color`                           | Sets the color of the email-field property based on conditions by using the `when` property. First evaluated to `true` will be used. Choose a color from the provided color palette. Default color is grey if the property is not specified in the YAML. See the list of available colors in [Jigx color palette](#).                                                                                                      |
| `errorText`                       | Add text, string, or expressions to show text under the email-field indicating an error/invalid value in the field. Text is shown in `isNegative` (red) styling with a red exclamation icon on the right.                                                                                                                                                                                                                  |
| `helperText`                      | Add text, string, or expressions to guide users by showing text under the email-field. Helper text is displayed only when there is no errorText.                                                                                                                                                                                                                                                                           |
| `icon`                            | Add an icon to the email-field. The icon apprears on the far right of the field.  A list of icons is available. See [Jigx icons](#) for more information.                                                                                                                                                                                                                                                                  |
| `initialValue`                    | The `initialValue` is the value that will be displayed in the email-field when the form is initially loaded. You can use this property to preset the field with a default email address so that you do not have to manually select it. Using the `reset-state` action with `initialValues` does not clear the field, it resets the field back to it's `initialValue`.                                                      |
| `isAutoFocused`                   | If `true` the email-field will get focus immediately after the form is displayed.                                                                                                                                                                                                                                                                                                                                          |
| `isHidden`                        | If `true` the email-field will be hidden on the form. If set to `false` the field will be shown.                                                                                                                                                                                                                                                                                                                           |
| `isIgnored`                       | When `true`, the field will be ignored when submitting the form and the content will not be stored.                                                                                                                                                                                                                                                                                                                        |
| `isOptionalLabelHidden`           | If the field is optional you can turn off the "(optional)" label by setting this field to `true`. This property works in combination with `isRequired: false`.                                                                                                                                                                                                                                                             |
| `isRequired`                      | Set to `true` when the field is required. Useful when you use it in form submission. Set to `false` the email-field is optional and will have (optional) in the label.                                                                                                                                                                                                                                                     |
| `isReturnKeyEnabledAutomatically` | When set to `true`, the keyboard disables the return/done key when there is no text and automatically enables it when there is text. The default value is `false`.                                                                                                                                                                                                                                                         |
| `isSensitive`                     | If set to `true`, the text input obscures the text entered so that sensitive email addresses stay secure.                                                                                                                                                                                                                                                                                                                  |
| `isTextClearedOnFocus`            | When set to `true`, the email-field is automatically cleared when editing begins.                                                                                                                                                                                                                                                                                                                                          |
| `KeyboardType`                    | Determines which keyboard to open. Default is email.                                                                                                                                                                                                                                                                                                                                                                       |
| `nextProperty`                    | Name of the property you want to focus next in the form when you use return/next on a keyboard.                                                                                                                                                                                                                                                                                                                            |
| `style`                           | The following property settings are available:&#xA;- `flex` - Flex property if rendered inside row.&#xA;- `isBusy` - Displays spinner on right side of field. It removes any  configured icon.&#xA;- `isDisabled` - disables the email-field preventing any input text.&#xA;- `isPositive` - a green icon displays on the right of the email-field.&#xA;More than one can be true. It will be evaluated based on priority. |
| `value`                           | The value to show in the email-field when the form initially loads. This can be combined with the `isDisable` style to preset the value that cannot be edited on the form.                                                                                                                                                                                                                                                 |

| **Actions** |                                                                                                                                             |
| ----------- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| `onChange`  | The action is triggered when the content in the email-field is changed. Use IntelliSense (ctrl+space) to see the list of available actions. |

| **State Configuration**  | **Key**              | **Notes**                                                          |
| ------------------------ | -------------------- | ------------------------------------------------------------------ |
| `=@ctx.component.state.` | value                | - State is the variable of the component.                          |
| `=@ctx.solution.state.`  | activeItemId&#xA;now | \* Global state variable that can be used throughout the solution. |

## Examples and code snippets

:::::ExpandableHeading
### Email Field on Form

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/dRoZqXtjnoY-wVwNMAaEM_cc-email-fieldsample.PNG" size="80" position="center" caption="Form with an email field" alt="Form with an email field" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/dRoZqXtjnoY-wVwNMAaEM_cc-email-fieldsample.PNG"}
:::

:::VerticalSplitItem
The example below displays a form input for the email address with an `icon` and `initialValue` set.

**Examples:**

See the full example using static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/email-field/static-data/email-field.jigx).
See the full example using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/email-field/dynamic-data/email-field-dynamic.jigx).
:::
::::

:::CodeblockTabs
email-field (static)

```yaml
children:
  - type: component.form
    instanceId: email-form
    options:
      children: 
        - type: component.email-field
          instanceId: email
          options:
            icon: email-action-at
            initialValue: name@example.com
            label: Email
```

email-field (dynamic)

```yaml
title: Email
type: jig.default

actions:
  - children:
    - type: action.execute-entity
      options:
        title: Create Record
        provider: DATA_PROVIDER_DYNAMIC
        entity: default/form
        method: save
        data:
          email: =@ctx.components.email.state.value
        onSuccess: 
          type: action.go-back

header:
  type: component.jig-header
  options:
    height: medium
    children:
      type: component.image
      options:
        title: Email 
        source:
          uri: https://cdn2.webdamdb.com/v1_1280_6enPaxIBt9M3.jpg?1554490336
        
children:
  - type: component.form
    instanceId: emails-form
    options:
      children: 
        - type: component.email-field
          instanceId: email
          options:
            label: Email
            helperText: =@ctx.datasources.field-values.email
```
:::
:::::

## See also

- [State](#)

