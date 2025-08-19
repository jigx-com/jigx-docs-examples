# email-field

{% columns %}
{% column %}
&#x20;Email fields in forms provide a user-friendly way to collect email addresses, incorporating validation to ensure data is entered correctly.

The `email-field` component can only be used in a [jig.default](<../../Jig Types/jig_default.md>) inside of a [form](../form.md) component for capturing an email address.&#x20;
{% endcolumn %}

{% column %}
&#x20;![Email Field Preview](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/dSjO63W1F7TwFYsE8SIUK_cc-emailfield.png)


{% endcolumn %}
{% endcolumns %}

{% hint style="info" %}
The `email-field` component can be used independently or within a `form` component, each offering distinct benefits. As a standalone, it provides flexibility for isolated usage without requiring a form structure. When wrapped in a form, it leverages the form’s instanceId, enabling better coordination and usability when managing multiple fields in a jig.&#x20;
{% endhint %}

### Configuration options

Some properties are common to all components, see [Common component properties](email-field.md) for a list and their configuration options.

<table><thead><tr><th width="190.49609375">Core structure</th><th></th></tr></thead><tbody><tr><td><code>instanceId</code></td><td>The unique identifier for the email-field.</td></tr><tr><td><code>label</code></td><td>Provide a label/name for the email-field. <em>Label</em> is displayed as a placeholder when no value is specified.</td></tr></tbody></table>

<table><thead><tr><th width="282.984375">Other options</th><th></th></tr></thead><tbody><tr><td><code>color</code></td><td>Sets the color of the email-field property based on conditions by using the <code>when</code> property. First evaluated to <code>true</code> will be used. Choose a color from the provided color palette. Default color is grey if the property is not specified in the YAML. See the list of available colors in .</td></tr><tr><td><code>errorText</code></td><td>Add text, string, or expressions to show text under the email-field indicating an error/invalid value in the field. Text is shown in <code>isNegative</code> (red) styling with a red exclamation icon on the right.</td></tr><tr><td><code>helperText</code></td><td>Add text, string, or expressions to guide users by showing text under the email-field. Helper text is displayed only when there is no errorText.</td></tr><tr><td><code>icon</code></td><td>Add an icon to the email-field. The icon apprears on the far right of the field. A list of icons is available. See for more information.</td></tr><tr><td><code>initialValue</code></td><td>The <code>initialValue</code> is the value that will be displayed in the email-field when the form is initially loaded. You can use this property to preset the field with a default email address so that you do not have to manually select it. Using the <code>reset-state</code> action with <code>initialValues</code> does not clear the field, it resets the field back to it's <code>initialValue</code>.</td></tr><tr><td><code>isAutoFocused</code></td><td>If <code>true</code> the email-field will get focus immediately after the form is displayed.</td></tr><tr><td><code>isHidden</code></td><td>If <code>true</code> the email-field will be hidden on the form. If set to <code>false</code> the field will be shown.</td></tr><tr><td><code>isIgnored</code></td><td>When <code>true</code>, the field will be ignored when submitting the form and the content will not be stored.</td></tr><tr><td><code>isOptionalLabelHidden</code></td><td>If the field is optional you can turn off the "(optional)" label by setting this field to <code>true</code>. This property works in combination with <code>isRequired: false</code>.</td></tr><tr><td><code>isRequired</code></td><td>Set to <code>true</code> when the field is required. Useful when you use it in form submission. Set to <code>false</code> the email-field is optional and will have (optional) in the label.</td></tr><tr><td><code>isReturnKeyEnabledAutomatically</code></td><td>When set to <code>true</code>, the keyboard disables the return/done key when there is no text and automatically enables it when there is text. The default value is <code>false</code>.</td></tr><tr><td><code>isSensitive</code></td><td>If set to <code>true</code>, the text input obscures the text entered so that sensitive email addresses stay secure.</td></tr><tr><td><code>isTextClearedOnFocus</code></td><td>When set to <code>true</code>, the email-field is automatically cleared when editing begins.</td></tr><tr><td><code>KeyboardType</code></td><td>Determines which keyboard to open. Default is email.</td></tr><tr><td><code>nextProperty</code></td><td>Name of the property you want to focus next in the form when you use return/next on a keyboard.</td></tr><tr><td><code>style</code></td><td><p>The following property settings are available:</p><ul><li><code>flex</code> - Flex property if rendered inside row.</li><li><code>isBusy</code> - Displays spinner on right side of field. It removes any configured icon.</li><li><code>isDisabled</code> - disables the email-field preventing any input text.</li><li><code>isPositive</code> - a green icon displays on the right of the email-field.</li></ul><p>More than one can be true. It will be evaluated based on priority.</p></td></tr><tr><td><code>value</code></td><td>The value to show in the email-field when the form initially loads. This can be combined with the <code>isDisable</code> style to preset the value that cannot be edited on the form.</td></tr></tbody></table>

<table><thead><tr><th width="153.12890625">Actions</th><th></th></tr></thead><tbody><tr><td><code>onChange</code></td><td>The action is triggered when the content in the email-field is changed. Use IntelliSense (ctrl+space) to see the list of available actions.</td></tr></tbody></table>

<table><thead><tr><th width="215.35546875">State Configuration</th><th width="134.2109375">Key</th><th>Notes</th></tr></thead><tbody><tr><td><code>=@ctx.component.state.</code></td><td>value</td><td>State is the variable of the component.</td></tr><tr><td><code>=@ctx.solution.state.</code></td><td>activeItemId now</td><td>Global state variable that can be used throughout the solution.</td></tr></tbody></table>

### Examples and code snippets

#### Email Field on Form

{% columns %}
{% column %}
Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/dRoZqXtjnoY-wVwNMAaEM\_cc-email-fieldsample.PNG" size="80" position="center" caption="Form with an email field" alt="Form with an email field" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/dRoZqXtjnoY-wVwNMAaEM\_cc-email-fieldsample.PNG" width="800" height="1613" darkWidth="800" darkHeight="1613"}&#x20;
{% endcolumn %}

{% column %}
The example below displays a form input for the email address with an `icon` and `initialValue` set.

**Examples:**

See the full example using static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/email-field/static-data/email-field.jigx). \
See the full example using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/email-field/dynamic-data/email-field-dynamic.jigx).
{% endcolumn %}
{% endcolumns %}

{% tabs %}
{% tab title="email-field (static)" %}
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
{% endtab %}

{% tab title="email-field (dynamic)" %}
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
{% endtab %}
{% endtabs %}

### See also

* [State](https://docs.jigx.com/state)
