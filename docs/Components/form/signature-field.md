# signature-field

:::::VerticalSplit{layout="middle"}
::::VerticalSplitItem
Simply draw your signature on your mobile screen to approve and proceed. This component can only be used in a [jig.default](<./../../Jig Types/jig_default.md>) inside of a [form](./../form.md) component for the input of a signature. It provides the experience of creating, uploading, and saving your eSignature in a few easy steps.

:::hint{type="info"}
The `signature-field` component can be used independently or within a `form` component, each offering distinct benefits. As a standalone, it provides flexibility for isolated usage without requiring a form structure. When wrapped in a form, it leverages the form’s instanceId, enabling better coordination and usability when managing multiple fields in a jig.
:::
::::

:::VerticalSplitItem
![Signature Field Preview](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/xFXGhidiImIpwwIhQy4kU_signature.png "Signature Field Preview")
:::
:::::

## Configuration options

Some properties are common to all components, see [Common component properties]() for a list and their configuration options.

<table isTableHeaderOn="true" selectedColumns="" selectedRows="" selectedTable="false" columnWidths="146">
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
      <p>The unique identifier for the signature-field component.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>label</code></p>
    </td>
    <td selected="false" align="left">
      <p>Provide a label/name for the signature field. 'Label' is displayed as a placeholder when no value is specified.</p>
    </td>
  </tr>
</table>

<table isTableHeaderOn="true" selectedColumns="" selectedRows="" selectedTable="false" columnWidths="209">
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
      <p>Sets the color of the signature field-based on conditions by using the <code>when</code> property. First evaluated to <code>true</code> will be used. Choose a color from the provided color palette. Default color is grey if the property is not specified in the YAML. See the list of available colors in .</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>errorText</code></p>
    </td>
    <td selected="false" align="left">
      <p>Add text, string, or expressions to show text under the signature-field  indicating an error/invalid value in the field. Text is shown in <code>isNegative</code> (red) styling with a red exclamation icon on the right.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>helperText</code></p>
    </td>
    <td selected="false" align="left">
      <p>Add text, string, or expressions to guide users by showing text under the signature-field. Helper text is displayed only when there is no errorText.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>icon</code></p>
    </td>
    <td selected="false" align="left">
      <p>Add an icon to the signature-field, for example a pen icon. The icon apprears on the far right of the field.  A list of icons is available. See  for more information.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>initialValue</code></p>
    </td>
    <td selected="false" align="left">
      <p>The <code>initialValue</code> is the value that will be displayed in the signature-field when the form is initially loaded. You can use this property to preset the field with a default signature so that you do not have to manually select it or if you already have the person signature in a datasource you can use anexpresssion to return the intial signature. Tapping on the field allows the person to re-sign the form if required. Using the <code>reset-state</code> action with <code>initialValues</code> does not clear the field, it resets the field back to it's <code>initialValue</code>.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>isAutoFocused</code></p>
    </td>
    <td selected="false" align="left">
      <p>If <code>true</code> the signature-field will get focus immediately after the form is displayed and the number keyboard will be opened automatically.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>isHidden</code></p>
    </td>
    <td selected="false" align="left">
      <p>If <code>true</code> the signature-field will be hidden on the form. If set to <code>false</code> the field will be shown.</p>
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
      <p>Set to <code>true</code> when the field is required. Useful when you use it in form submission as the submit button remains disabled until the signature has been applied. Set to <code>false</code> the signature-field is optional and will have (optional) in the label.</p>
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
      <p><code>style</code></p>
    </td>
    <td selected="false" align="left">
      <p>The following property settings are available:</p>
      <ul>
      <li><code>flex</code> - Flex property if rendered inside row.</li>
      <li><code>isBusy</code> - Displays spinner on right side of field. It removes any  configured icon.</li>
      <li><code>isDisabled</code> - disables the signature property preventing any input.</li>
      <li><code>isPositive</code> - a green icon displays on the right of the signature.</li>
      </ul>
      <p>More than one can be true. It will be evaluated based on priority.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>value</code></p>
    </td>
    <td selected="false" align="left">
      <p>The value to show in the signature-field when the form initially loads. This can be combined with the <code>isDisable</code> style to preset the value that cannot be edited on the form.</p>
    </td>
  </tr>
</table>

<table isTableHeaderOn="true" selectedColumns="" selectedRows="" selectedTable="false" columnWidths="218">
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
      <p>The action is triggered when the content in the signature-field is changed. Use IntelliSense (ctrl+space) to see the list of available actions.</p>
    </td>
  </tr>
</table>

<table isTableHeaderOn="true" selectedColumns="" selectedRows="" selectedTable="false" columnWidths="218,117">
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

:::::ExpandableHeading
### Signature Field on Form

::::VerticalSplit{layout="left"}
:::VerticalSplitItem
![Form signature](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/tCKu2RtpBmPBLyNyCEbL1_ofk8slzh8-djfwqstadycsignature-field.png "Form signature")
:::

:::VerticalSplitItem
The widget displays the signature input. After clicking on it, the user can create his/her eSignature.

**Example:**

See the full example in [GitHub]().
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

- [State](https://docs.jigx.com/state)

