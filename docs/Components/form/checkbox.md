# checkbox

{% columns %}
{% column %}
Checkboxes on mobile app forms offer a straightforward way to make selections, especially for multiple options, enhancing usability and interaction.

The component is used in a [jig.default](<../../Jig Types/jig_default.md>) inside of a [form](../form.md) component and supports single- and multiple-selection options. The checkbox's initial checkbox status and required checkbox status can be set.&#x20;
{% endcolumn %}

{% column %}
Image\[]{alt="Checkbox preview" src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/C108AXi\_xo5aRgmBnjo\_9\_checkboxes.png" size="90" caption="Checkbox preview" position="center" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/C108AXi\_xo5aRgmBnjo\_9\_checkboxes.png" width="800" height="348" darkWidth="800" darkHeight="348"}
{% endcolumn %}
{% endcolumns %}

{% hint style="info" %}
The `checkbox` component can be used independently or within a `form` component, each offering distinct benefits. As a standalone, it provides flexibility for isolated usage without requiring a form structure. When wrapped in a form, it leverages the form’s instanceId, enabling better coordination and usability when managing multiple fields in a jig.&#x20;
{% endhint %}

### Configuration options

Some properties are common to all components, see [Common component properties](checkbox.md) for a list and their configuration options.

<table><thead><tr><th width="199.234375">Core structure</th><th></th></tr></thead><tbody><tr><td><code>instanceId</code></td><td>The unique identifier for the checkbox component.</td></tr><tr><td><code>label</code></td><td>Provide a label/name for the checkbox. 'Label' is displayed as a placeholder when no value is specified.</td></tr></tbody></table>

<table><thead><tr><th width="197.9609375">Other options</th><th></th></tr></thead><tbody><tr><td><code>color</code></td><td>Sets the color of the checkbox based on conditions by using the <code>when</code> property. First evaluated to true will be used. Choose a color from the provided color palette. Default color is grey if the property is not specified in the YAML. See the list of available colors in .</td></tr><tr><td><code>errorText</code></td><td>Add text, string, or expressions to show text under the checkbox indicating an error/invalid value in the field. Text is shown in <code>isNegative</code> (red) styling.</td></tr><tr><td><code>helperText</code></td><td>Add text, string, or expressions to guide users by showing text under the checkbox. Helper text is displayed only when there is no <code>errorText</code>.</td></tr><tr><td><code>icon</code></td><td>Add an icon to the title. A list of icons is available. See for more information.</td></tr><tr><td><code>initialValue</code></td><td>The <code>initialValue</code> is the value that the checkbox will load with when the form is initially loaded. You can use this property to preset the checkbox value so that the user doesn't have to manually select it. Set to <code>true</code> loads the checkbox as selected, <code>false</code> loads the checkbox as unselected. Using the <code>reset-state</code> action with <code>initialValues</code> does not clear the checkbox, it resets the field back to its <code>initialValue</code>.</td></tr><tr><td><code>isAutoFocused</code></td><td>If <code>true</code> it will get focus immediately after the jig is displayed.</td></tr><tr><td><code>isHidden</code></td><td>If <code>true</code> the checkbox will be hidden on the form. If set to <code>false</code> the field will be shown.</td></tr><tr><td><code>isIgnored</code></td><td>When <code>true</code>, the field will be ignored when submitting the form and the content will not be stored.</td></tr><tr><td><code>isOptionalLabelHidden</code></td><td>If the field is optional you can turn off the "(optional)" label by setting this field to <code>true</code>. This property works in combination with <code>isRequired: false</code>.</td></tr><tr><td><code>isRequired</code></td><td>Set to <code>true</code> when the field is required. Useful when you use it in form submission. Set to <code>false</code> the checkbox is optional and will have an (optional) in the label.</td></tr><tr><td><code>nextProperty</code></td><td>Name of the property you want to focus next in the form when you use return/next on a keyboard.</td></tr><tr><td><code>style</code></td><td><p>The following property settings are available:</p><ul><li><code>flex</code> - Flex property if rendered inside row.</li><li><code>isDanger</code> - when the checkbox is selected the component displays in red.</li><li><code>isDisabled</code> - makes the checkbox field un-selectable.</li><li><code>isPositive</code> - when the checkbox is selected the component displays in green.</li><li><code>isWarning</code> - displays the component in red.</li></ul><p>More than one can be true. It will be evaluated based on priority.</p></td></tr><tr><td><code>value</code></td><td>The value to show for the checkbox. Setting up a checkbox with a <code>value</code> property of <code>true</code> will display the checkbox as selected when the form loads, setting the property to <code>false</code> will display the checkbox as unselected when the form loads.</td></tr></tbody></table>

| **Actions** |                                                                                                                                            |
| ----------- | ------------------------------------------------------------------------------------------------------------------------------------------ |
| `onChange`  | The action is triggered when the content in the `checkbox` is changed. Use IntelliSense (ctrl+space) to see the list of available actions. |
| `onPress`   | `OnPress` action overwrites the main check / uncheck functionality.                                                                        |

<table><thead><tr><th width="211.01953125">State Configuration</th><th width="143.390625">Key</th><th>Notes</th></tr></thead><tbody><tr><td><code>=@ctx.component.state.</code></td><td>value</td><td>State is the variable of the component.</td></tr><tr><td><code>=@ctx.solution.state.</code></td><td>activeItemId now</td><td>Global state variable that can be used throughout the solution.</td></tr></tbody></table>

{% hint style="info" %}
There's also the option to configure checkboxes as part of [entity-field](../entity/entity-field.md) or [list-item](../list/list-item.md).&#x20;
{% endhint %}

### Examples and code snippets

#### Checkbox on Form - Single Selection (Yes/No Question)

{% columns %}
{% column %}
&#x20;![Checkbox on a form](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/IJK_lSaGyt3T1vku2VDAY_mdjjmgfkxmndvtxfd8ru5checkbox-yes-no.png)&#x20;
{% endcolumn %}

{% column %}
The component displays a yes/no question about the agreement to the Terms and Conditions. The option is preselected as the agreement is in our case required.

**Examples:** \
See the full example using static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/checkbox/static-data/yes-no-question/checkbox-yes-no-question.jigx). \
See the full example using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/checkbox/dynamic-data/yes-no-question/checkbox-yes-no-dynamic.jigx).
{% endcolumn %}
{% endcolumns %}

{% tabs %}
{% tab title="check-box (static)" %}
```yaml
children:
  - type: component.form
    instanceId: agreement-form
    options:
      children:
        - type: component.checkbox
          instanceId: agreement
          options:
            label: I agree
            isRequired: true
            initialValue: true
```
{% endtab %}

{% tab title="check-box (dynamic)" %}
```yaml
children:
  - type: component.form
    instanceId: agreement-form
    options:
      children:
        - type: component.checkbox
          instanceId: agreement
          options:
            label: =@ctx.datasources.checkbox-options[0].agreement
            isRequired: true
            initialValue: true
```
{% endtab %}

{% tab title="datasources (dynamic)" %}
```yaml
datasources:
  checkbox-options:
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_DYNAMIC
      entities:
        - entity: default/checkbox
      query: |
        SELECT
          id,
          '$.order',
          '$.day',
          '$.agreement'
        FROM [default/checkbox] ORDER by '$.order'
```
{% endtab %}
{% endtabs %}

#### Checkbox on Form - Multiple Selection

{% columns %}
{% column %}
&#x20;![Multiple checkbox selection](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/MCeJFm_9bW3uwfB47U1Uk_ikqrb22eirxfob4os15bcheckbox-multi.PNG)&#x20;
{% endcolumn %}

{% column %}
This example displays a question you can answer by selecting multiple checkboxes. The most common answers are already checked for better user experience, but the selection can always be changed.

**Examples:**

See the full example using static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/checkbox/static-data/multiple-selection/checkbox-multiple-selection.jigx). See the full example using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/checkbox/dynamic-data/multiple-selection/checkbox-multiple-dynamic.jigx)&#x20;
{% endcolumn %}
{% endcolumns %}

{% tabs %}
{% tab title="checkbox-multiple (static)" %}
```yaml
children:
  - type: component.form
    instanceId: work-engagement-form
    options:
      children:
        - type: component.checkbox
          instanceId: sunday
          options:
            label: Sunday
            isRequired: false
        - type: component.checkbox
          instanceId: monday
          options:
            label: Monday
            initialValue: true
            isRequired: false
        - type: component.checkbox
          instanceId: tuesday
          options:
            label: Tuesday
            initialValue: true
            isRequired: false
        - type: component.checkbox
          instanceId: wednesday
          options:
            label: Wednesday
            initialValue: true
            isRequired: false
        - type: component.checkbox
          instanceId: thursday
          options:
            label: Thursday
            initialValue: true
            isRequired: false
        - type: component.checkbox
          instanceId: friday
          options:
            label: Friday
            initialValue: true
            isRequired: false
        - type: component.checkbox
          instanceId: saturday
          options:
            label: Saturday
            isRequired: false
```
{% endtab %}

{% tab title="checkbox-multiple (dynamic)" %}
```yaml
children:
  - type: component.form
    instanceId: work-engagement-form
    options:
      children: 
         - type: component.checkbox
           instanceId: sunday
           options:
             label: =@ctx.datasources.checkbox-options[0].day
             isRequired: false
         - type: component.checkbox
           instanceId: monday
           options:
             label: =@ctx.datasources.checkbox-options[1].day
             initialValue: true
             isRequired: false
         - type: component.checkbox
           instanceId: tuesday
           options:
             label: =@ctx.datasources.checkbox-options[2].day
             initialValue: true
             isRequired: false
         - type: component.checkbox
           instanceId: wednesday
           options:
             label: =@ctx.datasources.checkbox-options[3].day
             initialValue: true
             isRequired: false
         - type: component.checkbox
           instanceId: thursday
           options:
             label: =@ctx.datasources.checkbox-options[4].day
             initialValue: true
             isRequired: false
         - type: component.checkbox
           instanceId: friday
           options:
             label: =@ctx.datasources.checkbox-options[5].day
             initialValue: true
             isRequired: false
         - type: component.checkbox
           instanceId: saturday
           options:
             label: =@ctx.datasources.checkbox-options[6].day
             isRequired: false
```
{% endtab %}

{% tab title="datasources (dynamic)" %}
```yaml
datasources:
  checkbox-options:
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_DYNAMIC
      entities:
        - entity: default/checkbox
      query: |
        SELECT
          id,
          '$.order',
          '$.day',
          '$.agreement'
        FROM [default/checkbox] ORDER by '$.order'
```
{% endtab %}
{% endtabs %}
