# checkbox

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
Checkboxes on mobile app forms offer a straightforward way to make selections, especially for multiple options, enhancing usability and interaction.

The component is used in a [jig.default](<./../../Jig Types/jig_default.md>) inside of a [form](./../form.md) component and supports single- and multiple-selection options. The checkbox's initial checkbox status and required checkbox status can be set.
:::

:::VerticalSplitItem
::Image[]{alt="Checkbox preview" src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/C108AXi_xo5aRgmBnjo_9_checkboxes.png" size="90" caption="Checkbox preview" position="center" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/C108AXi_xo5aRgmBnjo_9_checkboxes.png" width="800" height="348" darkWidth="800" darkHeight="348"}
:::
::::

:::hint{type="info"}
The `checkbox` component can be used independently or within a `form` component, each offering distinct benefits. As a standalone, it provides flexibility for isolated usage without requiring a form structure. When wrapped in a form, it leverages the form’s instanceId, enabling better coordination and usability when managing multiple fields in a jig.
:::

## Configuration options

Some properties are common to all components, see [Common component properties]() for a list and their configuration options.

| **Core structure** |                                                                                                              |
| ------------------ | ------------------------------------------------------------------------------------------------------------ |
| `instanceId`       | The unique identifier for the checkbox component.                                                            |
| `label`            | Provide a label/name for the checkbox.&#xA;'Label' is displayed as a placeholder when no value is specified. |

<table isTableHeaderOn="true" selectedColumns="" selectedRows="" selectedTable="false" columnWidths="218">
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
      <p>Sets the color of the checkbox based on conditions by using the <code>when</code> property. First evaluated to true will be used.
      Choose a color from the provided color palette. Default color is grey if the property is not specified in the YAML.
      See the list of available colors in .</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>errorText</code></p>
    </td>
    <td selected="false" align="left">
      <p>Add text, string, or expressions to show text under the checkbox indicating an error/invalid value in the field.
      Text is shown in <code>isNegative</code> (red) styling.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>helperText</code></p>
    </td>
    <td selected="false" align="left">
      <p>Add text, string, or expressions to guide users by showing text under the checkbox.
      Helper text is displayed only when there is no <code>errorText</code>.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>icon</code></p>
    </td>
    <td selected="false" align="left">
      <p>Add an icon to the title.
      A list of icons is available. See  for more information.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>initialValue</code></p>
    </td>
    <td selected="false" align="left">
      <p>The <code>initialValue</code> is the value that the checkbox will load with when the form is initially loaded.
      You can use this property to preset the checkbox value so that the user doesn't have to manually select it.
      Set to <code>true</code> loads the checkbox as selected, <code>false</code> loads the checkbox as unselected.
      Using the <code>reset-state</code> action with <code>initialValues</code> does not clear the checkbox, it resets the field back to its <code>initialValue</code>.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>isAutoFocused</code></p>
    </td>
    <td selected="false" align="left">
      <p>If <code>true</code> it will get focus immediately after the jig is displayed.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>isHidden</code></p>
    </td>
    <td selected="false" align="left">
      <p>If <code>true</code> the checkbox will be hidden on the form.
      If set to <code>false</code> the field will be shown.</p>
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
      <p>If the field is optional you can turn off the "(optional)" label by setting this field to <code>true</code>.
      This property works in combination with <code>isRequired: false</code>.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>isRequired</code></p>
    </td>
    <td selected="false" align="left">
      <p>Set to <code>true</code> when the field is required.
      Useful when you use it in form submission.
      Set to <code>false</code> the checkbox is optional and will have an (optional) in the label.</p>
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
      <li><code>isDanger</code> - when the checkbox is selected the component displays in red.</li>
      <li><code>isDisabled</code> - makes the checkbox field un-selectable.</li>
      <li><code>isPositive</code> - when the checkbox is selected the component displays in green.</li>
      <li><code>isWarning</code> - displays the component in red.</li>
      </ul>
      <p>More than one can be true. It will be evaluated based on priority.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>value</code></p>
    </td>
    <td selected="false" align="left">
      <p>The value to show for the checkbox.
      Setting up a checkbox with a <code>value</code> property of <code>true</code> will display the checkbox as selected when the form loads,
      setting the property to <code>false</code> will display the checkbox as unselected when the form loads.</p>
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
      <p>The action is triggered when the content in the <code>checkbox</code> is changed. Use IntelliSense (ctrl+space) to see the list of available actions.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>onPress</code></p>
    </td>
    <td selected="false" align="left">
      <p><code>OnPress</code> action overwrites the main check / uncheck functionality.</p>
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

:::hint{type="info"}
There's also the option to configure checkboxes as part of [entity-field](./../entity/entity-field.md) or [list-item](./../list/list-item.md).
:::

## Examples and code snippets

:::::ExpandableHeading
### Checkbox on Form - Single Selection (Yes/No Question)

::::VerticalSplit{layout="left"}
:::VerticalSplitItem
![Checkbox on a form](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/IJK_lSaGyt3T1vku2VDAY_mdjjmgfkxmndvtxfd8ru5checkbox-yes-no.png "Checkbox on a form")
:::

:::VerticalSplitItem
The component displays a yes/no question about the agreement to the Terms and Conditions. The option is preselected as the agreement is in our case required.

**Examples:**
See the full example using static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/checkbox/static-data/yes-no-question/checkbox-yes-no-question.jigx).
See the full example using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/checkbox/dynamic-data/yes-no-question/checkbox-yes-no-dynamic.jigx).
:::
::::

:::CodeblockTabs
check-box (static)

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

check-box (dynamic)

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

datasources (dynamic)

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
:::
:::::

:::::ExpandableHeading
### Checkbox on Form - Multiple Selection

::::VerticalSplit{layout="left"}
:::VerticalSplitItem
![Multiple checkbox selection](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/MCeJFm_9bW3uwfB47U1Uk_ikqrb22eirxfob4os15bcheckbox-multi.PNG "Multiple checkbox selection")
:::

:::VerticalSplitItem
This example displays a question you can answer by selecting multiple checkboxes. The most common answers are already checked for better user experience, but the selection can always be changed.

**Examples:**

See the full example using static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/checkbox/static-data/multiple-selection/checkbox-multiple-selection.jigx).
See the full example using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/checkbox/dynamic-data/multiple-selection/checkbox-multiple-dynamic.jigx)
:::
::::

:::CodeblockTabs
checkbox-multiple (static)

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

checkbox-multiple (dynamic)

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

datasources (dynamic)

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
:::
:::::



