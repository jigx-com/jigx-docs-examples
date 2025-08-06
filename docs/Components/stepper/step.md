# step

This component displays consecutive steps in a stepper component. You can divide the task into steps, mark them as completed, and gradually get closer to completing the entire task.

::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/pHqn9aSU9OrBRvwBxvDw1_cc-step.png" size="66" position="center" caption="Step component" alt="Step component" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/pHqn9aSU9OrBRvwBxvDw1_cc-step.png" width="800" height="800" darkWidth="800" darkHeight="800"}

## Configuration options

Some properties are common to all components, see [Common component properties]() for a list and their configuration options.

<table isTableHeaderOn="true" selectedColumns="" selectedRows="" selectedTable="false" columnWidths="127">
  <tr>
    <td selected="false" align="left">
      <p><strong>Core structure</strong></p>
    </td>
    <td selected="false" align="left">
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>title</code></p>
    </td>
    <td selected="false" align="left">
      <p>Provide a title for the step item. You can use an expression to set the title.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>value</code></p>
    </td>
    <td selected="false" align="left">
      <p>The value of the step item. The value is exposed in the jig's state, making it available for use anywhere inside the jig.</p>
    </td>
  </tr>
</table>

<table isTableHeaderOn="true" selectedColumns="" selectedRows="" selectedTable="false" columnWidths="131">
  <tr>
    <td selected="false" align="left">
      <p><strong>Other options</strong></p>
    </td>
    <td selected="false" align="left">
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>description</code></p>
    </td>
    <td selected="false" align="left">
      <p>Describe the step item that is displayed as the subtitle.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>leftElement</code></p>
    </td>
    <td selected="false" align="left">
      <p>The only available element for the step is an <code>icon</code> displayed on the left of the value. A list of icons is available. See  for more information. If no icon is specified a checkbox is used on the left.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>style</code></p>
    </td>
    <td selected="false" align="left">
      <p>The following styling options are available:</p>
      <ul>
      <li><code>isActive</code> - Shows the step as active.</li>
      <li><code>isDisabled</code> - Shows the step <code>value</code>, <code>description</code>, and <code>icon</code> as disabled (greyed out).</li>
      <li><code>isNegative</code> - The step <code>description</code> and <code>icon</code> are shown in red.</li>
      <li><code>isPositive</code> - The <code>description</code> and <code>icon</code> are shown in green.</li>
      <li><code>isStrikeThrough</code> - The step's <code>value</code> and <code>description</code> are shown with a line through it.</li>
      <li><code>isWarning</code> - The <code>description</code> and <code>icon</code> are shown in orange.</li>
      </ul>
    </td>
  </tr>
</table>

<table isTableHeaderOn="true" selectedColumns="" selectedRows="" selectedTable="false" columnWidths="133">
  <tr>
    <td selected="false" align="left">
      <p><strong>Actions</strong></p>
    </td>
    <td selected="false" align="left">
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>onPress</code></p>
    </td>
    <td selected="false" align="left">
      <p>The action is triggered when pressing on the step item. Use IntelliSense  to see the list of available actions.</p>
    </td>
  </tr>
</table>

## Consideration

- The step component can only be used inside the [stepper](https://docs.jigx.com/examples/stepper) component.

## Examples and code snippets

:::::ExpandableHeading
### Step Example

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
\::Image\[]\{src="[https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/hSkErBLejyQpuODS8-\_4p\_xukzynxiz0pfnomjm8eyostepiphone13blueportrait.png](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/hSkErBLejyQpuODS8-_4p_xukzynxiz0pfnomjm8eyostepiphone13blueportrait.png)" size="80" "position="center" caption="Step inside a stepper component" alt="Step inside a stepper component"}
:::

:::VerticalSplitItem
This example shows the steps of delivering a shipment. In this case, the goods have already been ordered, and the shipment is in transit.

**Examples:**
See the full example using static data on [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/stepper/static-data/stepper-example/stepper-example.jigx).
See the full example using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/stepper/dynamic-data/stepper-example/stepper-example-dynamic.jigx).

**Datasource:**
See the full datasource for static data on [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/adhoc-components/steps.jigx).
See the full datasource for dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/adhoc-components/steps-dynamic.jigx).
:::
::::

:::CodeblockTabs
step (static)

```yaml
children:
  - type: component.stepper
    options:
      data: =@ctx.datasources.steps
      isExpandable: true
      title: Shipment in transit
      item:
        type: component.step
        options:
          title: =@ctx.current.item.title
          description: =@ctx.current.item.description
          value: =@ctx.current.item.value 
          leftElement:
            element: icon
            icon: =@ctx.current.item.icon
          style:
            isPositive: =@ctx.current.item.isCompleted
            isActive: =@ctx.current.item.isActive
            isStrikeThrough: =@ctx.current.item.isCompleted
            isDisabled: =@ctx.current.item.isWaiting
      completedPercentage: 0.5
```

step (dynamic)

```yaml
children:
  - type: component.stepper
    options:
      data: =@ctx.datasources.steps-dynamic
      isExpandable: true
      title: Shipment in transit
      item:
        type: component.step
        options:
          title: =@ctx.current.item.title
          description: =@ctx.current.item.description
          value: =@ctx.current.item.value 
          leftElement:
            element: icon
            icon: =@ctx.current.item.icon
          style:
            isPositive: =@ctx.current.item.iscompleted
            isActive: =@ctx.current.item.isactive
            isStrikeThrough: =@ctx.current.item.iscompleted
            isDisabled: =@ctx.current.item.iswaiting
      completedPercentage: 0.5
```

datasources (static)

```yaml
datasources:
  steps:
    type: datasource.static
    options:
      data:
        - title: Order
          value: step1
          icon: checkbox-checked
          isActive: false
          isCompleted: true
          isWaiting: false
        - description: The shipment is in transit.
          title: Shipment in transit
          value: step2
          icon: time-clock-circle
          isActive: true
          isCompleted: false
          isWaiting: false
        - title: On the way to you
          value: step3
          isActive: false
          isCompleted: false
          isWaiting: true
        - title: Delivered to the recipient
          value: step4
          isActive: false
          isCompleted: false
          isWaiting: true
```

datasources (dynamic)

```yaml
datasources:
  steps-dynamic:
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_DYNAMIC
      entities:
        - entity: default/steps
      query: |
        SELECT
          '$.title',
          '$.description',
          '$.value',
          '$.icon',
          '$.isactive',
          '$.iscompleted',
          '$.iswaiting'
        FROM [default/steps]
        ORDER BY value
```
:::
:::::

