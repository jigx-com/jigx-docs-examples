# avatar-field

{% columns %}
{% column %}
This component allows you to upload an avatar image. You can choose a picture from your device or use your camera to capture one.
{% endcolumn %}

{% column %}
<figure><img src="../../../.gitbook/assets/cc-avatar-field-intro.png" alt="Avatar Field" width="206"><figcaption><p>Avatar Field</p></figcaption></figure>
{% endcolumn %}
{% endcolumns %}

{% hint style="info" %}
The `avatar-field` component can be used independently or within a `form` component, each offering distinct benefits. As a standalone, it provides flexibility for isolated usage without requiring a form structure. When wrapped in a form, it leverages the form’s instanceId, enabling better coordination and usability when managing multiple fields in a jig.
{% endhint %}

## Configuration options

Some properties are common to all components, see [Common component properties](avatar-field.md) for a list and their configuration options.

<table><thead><tr><th width="198.54296875">Core structure</th><th></th></tr></thead><tbody><tr><td><code>instanceId</code></td><td>The unique identifier for the avatar-field.</td></tr><tr><td><code>label</code></td><td>Provide a label/name for the avatar. 'Label' is displayed as a placeholder when no value is specified. <strong>Note</strong> the label is displayed at the top of the popup screen where you select images.</td></tr></tbody></table>

<table><thead><tr><th width="202.02734375">Other options</th><th></th></tr></thead><tbody><tr><td><code>color</code></td><td>Sets the color of the avatar-field based on conditions by using the when property. First evaluated to true will be used. Choose a color from the provided color palette. Default color is grey if the property is not specified in the YAML. See the list of available colors in .</td></tr><tr><td><code>errorText</code></td><td>Add text, string, or expressions to show text under the avatar-field indicating an error/invalid value in the field. Text is shown in <code>isNegative</code> (red) styling.</td></tr><tr><td><code>helperText</code></td><td>Add text, string, or expressions to guide users by showing text under the avatar-field. Helper text is displayed only when there is no errorText.</td></tr><tr><td><code>imageQuality</code></td><td>Image quality after compression (from 0 to 100, where 100 is the best quality). On iOS, values larger than 80 don't produce a noticeable quality increase in most images, while a value of 80 will reduce the file size by about half or less compared to a value of 100. Default: 100 (Android)/ 80 (iOS).</td></tr><tr><td><code>icon</code></td><td>Add an icon to the title. A list of icons is available. See for more information.</td></tr><tr><td><code>imageCropping</code></td><td><p>You can set the following with <code>imageCropping</code> :</p><ul><li><code>isEnabled</code> - allows you to crop an image if set to <code>true</code>.</li><li><code>isFreeStyleCropEnabled</code> - when set to <code>true</code> it supports custom cropping to change the size or aspect ratio of an image.</li><li><code>height</code> - maximum allowed is 5000px</li><li><code>width</code>- maximum allowed is 5000px</li></ul></td></tr><tr><td><code>initialValue</code></td><td>Initial value of the relevant field. You can use this to preset value, so user doesn't need to add anything and use this "default". Using the <code>reset-state</code> action with <code>initialValues</code> does not clear the field, it resets the field back to it's <code>initialValue</code>.</td></tr><tr><td><code>isAutoFocused</code></td><td>If <code>true</code> it will get focus immediately after it is displayed.</td></tr><tr><td><code>isHidden</code></td><td>If <code>true</code> the avatar-field will be hidden on the form. If set to <code>false</code> the field will be shown.</td></tr><tr><td><code>isIgnored</code></td><td>When <code>true</code>, the field will be ignored when submitting the form and the content will not be stored.</td></tr><tr><td><code>isOptionalLabelHidden</code></td><td>If the field is optional you can turn off the "(optional)" label by setting this field to <code>true</code>. <strong>Note</strong> the (optional) text in the label is displayed at the top of the popup screen where you select images. This property works in combination with <code>isRequired: false</code>.</td></tr><tr><td><code>isRequired</code></td><td>Set to <code>true</code> when the field is required. Useful when you use it in form submission. When set to <code>false</code> the (optional) text in the label is displayed at the top of the popup screen where you select images.</td></tr><tr><td><code>maximumFileSize</code></td><td>Maximum file size in bytes. Set to 'none' to disable size check. Default value is <code>=6 * 1024 * 1024</code> 6MB.</td></tr><tr><td><code>nextProperty</code></td><td>Name of the property you want to focus next in the form when you use return/next on a keyboard.</td></tr><tr><td><code>style</code></td><td><p>The following property settings are available:</p><ul><li><code>flex</code> - Flex property if rendered inside row.</li><li><code>isBusy</code> - Displays a spinner.</li><li><code>isDisabled</code> - disables the avatar-field preventing the image selection popup from displaying.</li><li><code>isPositive</code></li></ul><p>More than one can be true. It will be evaluated based on priority.</p></td></tr><tr><td><code>value</code></td><td>The value to show for the field. Text field is a controlled component, which means the internal value will be forced to match this value prop if provided. In most cases, you don't need to use this.</td></tr></tbody></table>

<table><thead><tr><th width="203.7734375">Actions</th><th></th></tr></thead><tbody><tr><td><code>onChange</code></td><td>The action is triggered when the content in the avatar-field is changed. Use IntelliSense (ctrl+space) to see the list of available actions.</td></tr></tbody></table>

<table><thead><tr><th width="206.37109375">State Configuration</th><th width="156.9296875">Key</th><th>Notes</th></tr></thead><tbody><tr><td><code>=@ctx.component.state.</code></td><td>value</td><td>State is the variable of the component.</td></tr><tr><td><code>=@ctx.solution.state.</code></td><td>activeItemId now</td><td>Global state variable that can be used throughout the solution.</td></tr></tbody></table>

## Considerations

* The `avatar-field` can only be used in a [jig.default](<../../Jig Types/jig_default.md>) inside of a [form](form.md) component.
* Only Dynamic Data or SQL data can be used to ensure that the image can be saved.

## Examples and code snippets

### Avatar-field example

{% columns %}
{% column %}
![Avatar](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/zzGERUU6kEdLrZ3bKcKFy_q75ewfno5lmiohkj-lv9avatarfieldiphone13blueportrait.png)
{% endcolumn %}

{% column %}
This component uploads pictures for avatars. After clicking on the plus next to the avatar, a menu will appear to choose whether to upload an existing image from your device or use the camera to take a new image. After loading and cropping the image, press the Upload picture button at the bottom to call the action to save the image.

**Examples:**

See the full example using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/avatar-field/dynamic-data/avatar-field-example/avatar-field-example.jigx)
{% endcolumn %}
{% endcolumns %}

{% code title="avatar (dynamic)" %}
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
{% endcode %}
