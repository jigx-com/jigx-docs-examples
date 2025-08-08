# avatar-field

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
This component allows you to upload an avatar image. You can choose a picture from your device or use your camera to capture one.
:::

:::VerticalSplitItem
::Image[]{alt="Avatar Field Preview" src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/-_UiZpMFDyAN1buxUcz3m_avatar-field.png" size="72" caption="Avatar Field Preview" position="center" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/-_UiZpMFDyAN1buxUcz3m_avatar-field.png" width="800" height="463" darkWidth="800" darkHeight="463"}
:::
::::

:::hint{type="info"}
The `avatar-field` component can be used independently or within a `form` component, each offering distinct benefits. As a standalone, it provides flexibility for isolated usage without requiring a form structure. When wrapped in a form, it leverages the form’s instanceId, enabling better coordination and usability when managing multiple fields in a jig.
:::

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
      <p>The unique identifier for the avatar-field.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>label</code></p>
    </td>
    <td selected="false" align="left">
      <p>Provide a label/name for the avatar. 'Label' is displayed as a placeholder when no value is specified. <strong>Note</strong> the label is displayed at the top of the popup screen where you select images.</p>
    </td>
  </tr>
</table>

<table isTableHeaderOn="true" selectedColumns="" selectedRows="" selectedTable="false" columnWidths="214">
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
      <p>Sets the color of the avatar-field based on conditions by using the when property. First evaluated to true will be used. Choose a color from the provided color palette. Default color is grey if the property is not specified in the YAML. See the list of available colors in .</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>errorText</code></p>
    </td>
    <td selected="false" align="left">
      <p>Add text, string, or expressions to show text under the avatar-field indicating an error/invalid value in the field. Text is shown in <code>isNegative</code> (red) styling.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>helperText</code></p>
    </td>
    <td selected="false" align="left">
      <p>Add text, string, or expressions to guide users by showing text under the avatar-field. Helper text is displayed only when there is no errorText.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>imageQuality</code></p>
    </td>
    <td selected="false" align="left">
      <p>Image quality after compression (from 0 to 100, where 100 is the best quality). On iOS, values larger than 80 don't produce a noticeable quality increase in most images, while a value of 80 will reduce the file size by about half or less compared to a value of 100. Default: 100 (Android)/ 80 (iOS).</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>icon</code></p>
    </td>
    <td selected="false" align="left">
      <p>Add an icon to the title. A list of icons is available. See for more information.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>imageCropping</code></p>
    </td>
    <td selected="false" align="left">
      <p>You can set the following with <code>imageCropping</code> :</p>
      <ul>
      <li><code>isEnabled</code> - allows you to crop an image if set to <code>true</code>.</li>
      <li><code>isFreeStyleCropEnabled</code> - when set to <code>true</code> it supports custom cropping to change the size or aspect ratio of an image.</li>
      <li><code>height</code> - maximum allowed is 5000px</li>
      <li><code>width</code>- maximum allowed is 5000px</li>
      </ul>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>initialValue</code></p>
    </td>
    <td selected="false" align="left">
      <p>Initial value of the relevant field. You can use this to preset value, so user doesn't need to add anything and use this "default". Using the <code>reset-state</code> action with <code>initialValues</code> does not clear the field, it resets the field back to it's <code>initialValue</code>.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>isAutoFocused</code></p>
    </td>
    <td selected="false" align="left">
      <p>If <code>true</code> it will get focus immediately after it is displayed.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>isHidden</code></p>
    </td>
    <td selected="false" align="left">
      <p>If <code>true</code> the avatar-field will be hidden on the form. If set to <code>false</code> the field will be shown.</p>
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
      <p>If the field is optional you can turn off the "(optional)" label by setting this field to <code>true</code>. <strong>Note</strong> the (optional) text in the label is displayed at the top of the popup screen where you select images. This property works in combination with <code>isRequired: false</code>.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>isRequired</code></p>
    </td>
    <td selected="false" align="left">
      <p>Set to <code>true</code> when the field is required. Useful when you use it in form submission. When set to <code>false</code> the (optional) text in the label is displayed at the top of the popup screen where you select images.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>maximumFileSize</code></p>
    </td>
    <td selected="false" align="left">
      <p>Maximum file size in bytes. Set to 'none' to disable size check. Default value is <code>=6 * 1024 * 1024</code> 6MB.</p>
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
      <li><code>isBusy</code> - Displays a spinner.</li>
      <li><code>isDisabled</code> - disables the avatar-field preventing the image selection popup from displaying.</li>
      <li><code>isPositive</code></li>
      </ul>
      <p>More than one can be true. It will be evaluated based on priority.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>value</code></p>
    </td>
    <td selected="false" align="left">
      <p>The value to show for the field. Text field is a controlled component, which means the internal value will be forced to match this value prop if provided. In most cases, you don't need to use this.</p>
    </td>
  </tr>
</table>

<table isTableHeaderOn="true" selectedColumns="" selectedRows="" selectedTable="false">
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
      <p>The action is triggered when the content in the avatar-field is changed. Use IntelliSense (ctrl+space) to see the list of available actions.</p>
    </td>
  </tr>
</table>

<table isTableHeaderOn="true" selectedColumns="" selectedRows="" selectedTable="false" columnWidths="223,126">
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
      <p>activeItemId now</p>
    </td>
    <td selected="false" align="left">
      <p>Global state variable that can be used throughout the solution.</p>
    </td>
  </tr>
</table>

## Considerations

- The `avatar-field` can only be used in a [jig.default](<./../../Jig Types/jig_default.md>) inside of a [form](./../form.md) component.
- Only Dynamic Data or SQL data can be used to ensure that the image can be saved.

## Examples and code snippets

:::::ExpandableHeading
### Avatar-field example

::::VerticalSplit{layout="left"}
:::VerticalSplitItem
![Avatar ](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/zzGERUU6kEdLrZ3bKcKFy_q75ewfno5lmiohkj-lv9avatarfieldiphone13blueportrait.png "Avatar ")
:::

:::VerticalSplitItem
This component uploads pictures for avatars.  After clicking on the plus next to the avatar, a menu will appear to choose whether to upload an existing image from your device or use the camera to take a new image. After loading and cropping the image, press the Upload picture button at the bottom to call the action to save the image.

**Examples:**

See the full example using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/avatar-field/dynamic-data/avatar-field-example/avatar-field-example.jigx)
:::
::::

:::CodeblockTabs
avatar (dynamic)

```yaml
children:
  - type: component.form
    options:
      children:
        - type: component.avatar-field
          instanceId: avatar-field
          options:
            label: Upload avatar
            color:
              - when: true
                color: color2
            style:
              flex: 1
            imageCropping:
              width: 120
              height: 120
            isHidden: false
            isIgnored: false
```
:::
:::::

