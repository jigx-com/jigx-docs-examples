# trend

The trend component displays an increase or decrease over a period. The increment or decrement number can be formatted as a percentage, currency, or plain value.

Trend is available in the following content widgets:

- [chart](./../chart.md)
- [list](./../list.md)&#x20;
- [value](./../value.md)&#x20;

## Configuration options

<table isTableHeaderOn="true" selectedColumns="" selectedRows="" selectedTable="false" columnWidths="110">
  <tr>
    <td selected="false" align="left">
      <p><strong>Core structure</strong></p>
    </td>
    <td selected="false" align="left">
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>value</code></p>
    </td>
    <td selected="false" align="left">
      <p>Positive or negative numeric value.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>format</code></p>
    </td>
    <td selected="false" align="left">
      <p>A selection of formats is available for the main value of the widget, for example, currency.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>title</code></p>
    </td>
    <td selected="false" align="left">
      <p>Display a <code>title</code> for the trend.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>subtitle</code></p>
    </td>
    <td selected="false" align="left">
      <p>Add a subtitle under the title text. Note: this text won't be displayed if <code>isValueBottom</code> is set to <code>true</code></p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>style</code></p>
    </td>
    <td selected="false" align="left">
      <p>Properties used for component styling.</p>
      <ul>
      <li><code>isValueBottom</code> - By default, the value is on the right of the text.  Set the property to <code>true</code> to move it underneath the text.</li>
      <li><code>isValueHidden</code> - hides the number and only shows an icon indicating an up or down trend.</li>
      <li><code>isAlignRight</code> - aligns everything to the right.</li>
      </ul>
    </td>
  </tr>
</table>

## Examples and code snippets

:::::ExpandableHeading
### Trend on value widget

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/YIaF_yhQk7REdnMJBJB10_trend-valueiphone13blueportrait.png" size="76" position="center" caption="Upward trend" alt="Upward trend" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/YIaF_yhQk7REdnMJBJB10_trend-valueiphone13blueportrait.png" width="800" height="1493" darkWidth="800" darkHeight="1493"}
:::

:::VerticalSplitItem
This example shows an increase in company turnover. The company has a turnover of over 24K USD, and the trend component shows that the increase for the last week is 1250 USD.

**Examples**:
See the full example using static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/trend/static-data/trend-in-value-widget/trend-in-value-widget.jigx).
See the full example using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/trend/dynamic-data/trend-in-value-widget/trend-in-value-dynamic.jigx).
:::
::::

:::CodeblockTabs
trend-value (static)

```yaml
widgets:
  trend-value:
    type: widget.value
    options:
      value: '23850'
      align: right
      format:
        numberStyle: currency
        currency: USD
      bottom: 
        type: component.trend
        options:
          title: 'Last week'
          value: +1250
          format:
            numberStyle: currency
            currency: USD
      top: 
        type: component.titles
        options:
          icon: chart
          iconColor: color6
```

trend-value (dynamic)

```yaml
widgets:
  trend-value-dd:
    type: widget.value
    options:
      value: =@ctx.datasources.trend-dynamic.financevalue
      align: right
      format:
        numberStyle: currency
        currency: USD
      bottom: 
        type: component.trend
        options:
          title: =@ctx.datasources.trend-dynamic.title
          value: =@ctx.datasources.trend-dynamic.value
          format:
            numberStyle: currency
            currency: USD
      top: 
        type: component.titles
        options:
          icon: chart
          iconColor: color6
```

grid-item

```yaml
# Grid-item for the static jig.
children:
  - type: component.grid-item
    options:
      size: "2x2"
      children: 
        type: component.jig-widget
        options:
          jigId: trend-in-value-widget
          widgetId: trend-value
```
:::
:::::

:::::ExpandableHeading
### Trend on chart widget

::::VerticalSplit{layout="left"}
:::VerticalSplitItem
![Percentage trend](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/JMOCUzUBcSOdzFhCFq-Y9_trend-chartiphone13blueportrait.png "Percentage trend")
:::

:::VerticalSplitItem
This example shows finance statistics. The trend component, indicates an increase in percent. Exactly 21% in the last period.

**Examples**:
See the full example using static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/trend/static-data/trend-in-chart-widget/trend-in-chart-widget.jigx).
See the full example using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/trend/dynamic-data/trend-in-chart-widget/trend-in-chart-dynamic.jigx).
:::
::::

:::CodeblockTabs
trend-chart (static)

```yaml
widgets:
  trendStatic-4x4:
    type: widget.chart
    options:
      top:
        type: component.trend
        options:
          title: "$ 39,559.36"
          value: 0.21
          format:
            numberStyle: percent
          style:
            isAlignRight: true
            isValueBottom: true
      chart:
        type: component.line-chart
        options:
          chart:
            isAnimated: true
          yAxis:
            min: 0
            labels:
              format:
                numberStyle: currency
                compactDisplay: short
                notation: compact
            tickAmount: 4
            isFirstTickHidden: true
            isFirstLabelHidden: true
          xAxis:
            categories:
              - Q1
              - Q2
              - Q3
              - Q4
          series:
            - data: =@ctx.datasources.series1
              name: Year 2019
              animation:
                  direction: left-to-right
              layout: area-gradient
              dataLabels:
                - isEnabled: true   
          legend:
            isHidden: false
```

trend-chart (dynamic)

```yaml
widgets:
  trendDD-4x4:
    type: widget.chart
    options:
      top:
        type: component.trend
        options:
          title: "$ 39,559.36"
          value: 0.21
          format:
            numberStyle: percent
          style:
            isAlignRight: true
            isValueBottom: true
      chart:
        type: component.line-chart
        options:
          chart:
            isAnimated: true
          yAxis:
            min: 0
            labels:
              format:
                numberStyle: currency
                compactDisplay: short
                notation: compact
            tickAmount: 4
            isFirstTickHidden: true
            isFirstLabelHidden: true
          xAxis:
            categories:
              - Q1
              - Q2
              - Q3
              - Q4
          series:
            - data: =@ctx.datasources.series1-dynamic
              name: Year 2019
              animation:
                  direction: left-to-right
              layout: area-gradient
              dataLabels:
                - isEnabled: true   
          legend:
            isHidden: false
```

grid-item

```yaml
# Grid-item for the static jig.
children:
  - type: component.grid-item
    options:
      size: "4x4"
      children: 
        type: component.jig-widget
        options:
          jigId: trend-in-chart-widget
          widgetId: trendStatic-4x4
```
:::
:::::

:::::ExpandableHeading
### Trend on list widget

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/D7VqLAmAop15HaURF_Dlk_trend-listiphone13blueportrait.png" size="84" position="center" caption="Patient trend over a period" alt="Patient trend over a period" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/D7VqLAmAop15HaURF_Dlk_trend-listiphone13blueportrait.png" width="800" height="1493" darkWidth="800" darkHeight="1493"}
:::

:::VerticalSplitItem
In this example, the widget-list shows a list of patients. There are a total of 569 patients and the trend component shows that 12 more patients were added in the last period.

**Examples**:
See the full example using static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/trend/static-data/trend-in-list-widget/trend-in-list-widget.jigx).
See the full example using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/trend/dynamic-data/trend-in-list-widget/trend-in-list-dynamic.jigx).
:::
::::

:::CodeblockTabs
trend-list (static)

```yaml
widgets:
  trendList-2x2:
    type: widget.list
    options:
      data: =@ctx.datasources.static-global-multiple
      top:
        type: component.trend
        options:
          title: "569 Patients"
          subtitle: "Patients"
          value: 12
          style:
            isAlignRight: false
            isValueBottom: true
            isValueHidden: false
      item:
        type: component.list-item
        options:
          title: =@ctx.current.item.name
          leftElement: 
            element: avatar
            text: NA
            uri: =@ctx.current.item.picture
```

trend-list (dynamic)

```yaml
widgets:
  trendListDD-2x2:
    type: widget.list
    options:
      data: =@ctx.datasources.employees-dynamic
      top:
        type: component.trend
        options:
          title: "569 Patients"
          subtitle: "Patients"
          value: 12
          style:
            isAlignRight: false
            isValueBottom: true
            isValueHidden: false
      item:
        type: component.list-item
        options:
          title: =@ctx.current.item.firstname & ' ' & @ctx.current.item.lastname
          leftElement: 
            element: avatar
            text: =$substring(@ctx.current.item.firstname, 0, 1) & $substring(@ctx.current.item.lastname, 0, 1)
            uri: =@ctx.current.item.photo
```

grid-item

```yaml
# Grid-item for the static jig.
children:
  - type: component.grid-item
    options:
      size: "2x2"
      children: 
        type: component.jig-widget
        options:
          jigId: trend-in-list-widget
          widgetId: trendList-2x2
```
:::
:::::

