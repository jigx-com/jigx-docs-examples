# stepper

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
This component displays the progress status of a task. Useful when tracking deliveries or claims. This component can only be used in a [jig.default](<./../Jig Types/jig_default.md>).
:::

:::VerticalSplitItem
![Stepper Preview](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/lRGV6B3arl4EitmWCT0SE_stepper.png "Stepper Preview")
:::
::::

## Configuration options

Some properties are common to all components, see [Common component properties]() for a list and their configuration options.

<table isTableHeaderOn="true" selectedColumns="" selectedRows="" selectedTable="false" columnWidths="202">
  <tr>
    <td selected="false" align="left">
      <p><strong>Core structure</strong></p>
    </td>
    <td selected="false" align="left">
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>data</code></p>
    </td>
    <td selected="false" align="left">
      <p>Define the data to be used in the step items, you can use expressions to reference a datasource.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>item</code></p>
    </td>
    <td selected="false" align="left">
      <p>There is only one available option, which is . The <code>item</code> property is core for the stepper component, so even if you are creating a non-expandable stepper you must configure the step component's <code>title</code> and <code>value</code> properties with an empty string: ""</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>completedPercentage</code></p>
    </td>
    <td selected="false" align="left">
      <p>Define the percentage to be displayed on the chart. Example "0.24" => 24 %. 1 represents 100% complete.</p>
    </td>
  </tr>
</table>

<table isTableHeaderOn="true" selectedColumns="" selectedRows="" selectedTable="false" columnWidths="197">
  <tr>
    <td selected="false" align="left">
      <p><strong>Other options</strong></p>
    </td>
    <td selected="false" align="left">
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>isExpandable</code></p>
    </td>
    <td selected="false" align="left">
      <p>Set to <code>true</code> the stepper will be expandable into steps. Set to <code>false</code> the stepper is not expandable.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>style</code></p>
    </td>
    <td selected="false" align="left">
      <p>The styling determines the color of the chart. There are three colors options, determined by the standard colors or by your branding color configuration. For example if the status is complete use <code>isPositive</code> to show the chart in green (standard). If no style is specified the chart shows in blue (standard).
      Available options:</p>
      <ul>
      <li><code>isNegative</code> - red (standard)</li>
      <li><code>isPositive</code> -  green (standard)</li>
      <li><code>isWarning</code> - orange (standard)</li>
      </ul>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>subtitle</code></p>
    </td>
    <td selected="false" align="left">
      <p>The subtitle/short description of the stepper to display under the title. You can use an expression to set the subtitle.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>title</code></p>
    </td>
    <td selected="false" align="left">
      <p>The title for the stepper, you can use an expression to set the title.</p>
    </td>
  </tr>
</table>

## Examples and code snippets

:::::ExpandableHeading
### Stepper example

::::VerticalSplit{layout="left"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/3q5XYI9fcgYMnxTTSMBaa_xqldilpo0dsaonqcdwm8ostepperiphone13blueportrait.png" size="88" position="center" caption="Stepper for shipment status" alt="Stepper for shipment status" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/3q5XYI9fcgYMnxTTSMBaa_xqldilpo0dsaonqcdwm8ostepperiphone13blueportrait.png" width="800" height="1494" darkWidth="800" darkHeight="1494"}
:::

:::VerticalSplitItem
In this example, a stepper component shows that the task is half done. For completeness, use it together with the step component. After expanding the stepper, the individual steps will be shown.

**Examples**:
See the full example using static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/stepper/static-data/stepper-example/stepper-example.jigx).
See the full example using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/stepper/dynamic-data/stepper-example/stepper-example-dynamic.jigx).

**Datasource**:
See the full datasource for static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/adhoc-components/steps.jigx).
See the full datasource for dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/adhoc-components/steps-dynamic.jigx).
:::
::::

:::CodeblockTabs
stepper (static)

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
      style:  
        isPositive: false
        isWarning: false
        isNegative: false
```

stepper (dynamic)

```yaml
tchildren:
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
      style:  
        isPositive: false
        isWarning: false
        isNegative: false
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

