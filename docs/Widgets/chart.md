# chart

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
The chart widget is suitable for displaying the \<[line-chart](https://docs.jigx.com/examples/line-chart), [bar-chart](https://docs.jigx.com/examples/bar-chart), or [pie-chart](https://docs.jigx.com/examples/pie-chart) on the Home Hub .
:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/adjbqUzKWPTPOznhe57WH_wd-charts.PNG" size="64" position="center" caption="Chart widgets" alt="Chart widgets" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/adjbqUzKWPTPOznhe57WH_wd-charts.PNG"}
:::
::::

## Configuration options

| **Core structure** |                                                                                                                                                                                                                                                            |
| ------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `chart`            | The configuration is the same as for the chart components, refer to the [line-chart](https://docs.jigx.com/examples/line-chart), [bar-chart](https://docs.jigx.com/examples/bar-chart), or [pie-chart](https://docs.jigx.com/examples/pie-chart) examples. |

| **Other options** |                                                                                                          |
| ----------------- | -------------------------------------------------------------------------------------------------------- |
| `bottom`          | The [titles](https://docs.jigx.com/examples/titles) component will be added to the bottom of the widget. |
| `footer`          | Add text to the footer of the widget.                                                                    |
| `footerAlign`     | Align the footer text to `left`, `right`, `center`.                                                      |
| `placeholders`    | Specify a placeholder text to display if there is no data, for example - `title: No data to display`.    |
| `top`             | The [titles](https://docs.jigx.com/examples/titles) component will be added to the top of the widget.    |

## Considerations

- It is recommended to set either the `top`, `bottom`, or both properties when configuring a chart widget to ensure it renders correctly and maintains a clear, readable layout within the widget.

## Examples and code snippets

:::::ExpandableHeading

### Chart widget: line-chart component (2x2)

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/J6pNWuARKgPksDAqWwkzK_wd-chartline22.PNG" size="74" position="center" caption="Line-chart 2x2" alt="Line-chart 2x2" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/J6pNWuARKgPksDAqWwkzK_wd-chartline22.PNG"}
:::

:::VerticalSplitItem
In this example select the `chart` widget and add a `component.line-chart` and add a `component.trend` at the `top` to show the positive percentage trend and a `component.titles` at the `bottom`.

**Example:**
See the complete example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/widgets/2x2/chart-line-1_2x2.jigx).
:::
::::

:::CodeblockTabs
chart-line-1\_2x2.jigx

```yaml
widgets:
   line1-2x2: 
   # select chart widget and then add the compoments trend and line-chart
    type: widget.chart
    options:     
      top:
        type: component.trend
        options:
          title: Quarterly Revenue
          style:
            isAlignRight: false
            isValueBottom: true
          value: 0.911111111111      
          format:
            numberStyle: percent
            
      chart:     
        type: component.line-chart
        options:
          legend:
            isHidden: false
          series:
            - data: =@ctx.datasources.static-data
              dataLabels:
                - isEnabled: true
              name: Quarterly Revenue 2020
              layout: area-gradient
          xAxis:
            categories:
              - Q1
              - Q2
              - Q3
              - Q4
          yAxis:
            isFirstLabelHidden: true
            isFirstTickHidden: true
            labels:
              format:
                compactDisplay: long
                notation: compact
                numberStyle: currency
            min: 0
            tickAmount: 3
      bottom: 
        type: component.titles
        options:
          subtitle: Updated 1 min ago
          align: center
```

datasource

```yaml
datasources:
  static-data:
    type: datasource.static
    options:
      data:
        - x: Q1/20
          y: 25000
        - x: Q2/20
          y: 32000
        - x: Q3/20
          y: 45000
        - x: Q4/20
          y: 86000
```

grid-item

```yaml
# Grid-item for the jig.
children:
  - type: component.grid-item
    options:
      size: "2x2"
      children: 
        type: component.jig-widget
        options:
          jigId: chart-line-1_2x2
          widgetId: line1-2x2
```

:::
:::::

:::::ExpandableHeading

### Chart widget: line-chart component (2x4)

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
In this example select the `chart` widget and add a `component.line-chart` and add a `component.title` at the `top`.

**Example:**
See the complete example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/widgets/2x4/chart-line-1_2x4.jigx).
:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/q9x1YJjqI0mnBBDuf9rBh_wd-chartline24.PNG" size="84" position="center" caption signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/q9x1YJjqI0mnBBDuf9rBh_wd-chartline24.PNG"}
:::
::::

:::CodeblockTabs
chart-line-1\_2x4.jigx

```yaml
widgets:
  line1-2x4: 
    type: widget.chart
    options:
      top: 
        type: component.titles
        options:
          title: Company Perf.
          subtitle: "2022"
        
      chart: 
        type: component.line-chart
        options:
          plotOptions:
            series:
              marker:
                isHidden: true
          series:
            - animation:
                direction: left-to-right
              data: =@ctx.datasources.static-data
              name: Quarterly Revenue 2020
              color: color6
              layout: area-gradient
          xAxis:
            categories:
              - Q1
              - Q2
              - Q3
              - Q4
          yAxis:
            isFirstLabelHidden: true
            isFirstTickHidden: true
            labels:
              format:
                compactDisplay: short
                notation: compact
                numberStyle: currency
            min: 0
            max: 75000
            tickAmount: 6
```

datasource

```yaml
datasources:
  static-data:
    type: datasource.static
    options:
      data:
        - x: Q1/20
          y: 35000
        - x: Q2/20
          y: 32000
        - x: Q3/20
          y: 28000
        - x: Q4/20
          y: 45000
```

grid-item

```yaml
# Grid-item for the jig.
children:
  - type: component.grid-item
    options:
      size: "2x2"
      children: 
        type: component.jig-widget
        options:
          jigId: chart-line-1_2x4
          widgetId: line1-2x4
```

:::
:::::

:::::ExpandableHeading

### Chart widget: line-chart component (4x4)

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
![Line-chart widget 4x4](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/YwBcJsDpeAgYRh0HOhte2_wd-line44.PNG "Line-chart widget 4x4")
:::

:::VerticalSplitItem
In this example select the `chart` widget and add a `component.line-chart` and add a `component.title` at the `top` and at the `bottom`.

**Example:**
See the complete example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/widgets/4x4/chart-line-2_4x4.jigx) for the Sales performance line-chart widget.
See the complete example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/widgets/4x4/chart-line-1_4x4.jigx) for the Quarterly Company Progress.
:::
::::

:::CodeblockTabs
chart-line-2\_4x4.jigx

```yaml
title: Line chart 2 (4x4)
type: jig.default

datasources:
  static-data:
    type: datasource.static
    options:
      data:
        - 41456
        - 40667
        - 50445
        - 57223
  static-data2:
    type: datasource.static
    options:
      data:
        - 43445
        - 48230
        - 37230
        - 89400      
  static-data3:
    type: datasource.static
    options:
      data:
        - 45778
        - 64889
        - 20009
        - 50432   

children:
  - type: component.entity
    options:
      children:
        - type: component.entity-field
          options:
            label: Placeholder
            value: Value
widgets:
  line2-4x4:
    type: widget.chart
    options:
      top:
        type: component.titles
        options:
          title: Sales Performance
      chart:
        type: component.line-chart
        
        options:
          yAxis:
            min: 0
            tickAmount: 7
            labels:
              format:
                notation: compact
                numberStyle: currency  
          xAxis:
            categories:
              - "07/22"
              - "08/22"
              - "09/22"
              - "10/22"
          series:
            - data: =@ctx.datasources.static-data
              layout: area-gradient
              animation:
                direction: bottom-to-top
              color: color7
            - data: =@ctx.datasources.static-data2
              layout: area-gradient
              animation:
                direction: bottom-to-top
              color: color9
            - data: =@ctx.datasources.static-data3
              layout: area-gradient
              animation:
                direction: bottom-to-top
              color: color2
      bottom: 
        type: component.titles
        options: 
          title: 110 New Paying Customers
          subtitle: Goal for 2022
          icon: multiple-neutral-2
          iconColor: color4
          align: center
```

chart-line-1\_4x4.jigx

```yaml
title: Line chart 1 (4x4)
type: jig.default

datasources:
  static-data:
    type: datasource.static
    options:
      data:
        - x: Q1/20
          y: 25767
        - x: Q2/20
          y: 45320
        - x: Q3/20
          y: 33100
        - x: Q4/20
          y: 91750

children:
  - type: component.entity
    options:
      children:
        - type: component.entity-field
          options:
            label: Placeholder
            value: Value

widgets:
  line2-4x4: 
    type: widget.chart
    options:
      top: 
        type: component.titles
        options:
          title: $91.750
          icon: chart
      chart: 
        type: component.line-chart
        options:
          legend:
            isHidden: false
          series:
            - animation:
                direction: left-to-right
              data: =@ctx.datasources.static-data
              color: color3
              dataLabels:
                - isEnabled: true
              name: Quarterly Revenue 2022
              layout: area-gradient
          xAxis:
            categories: =@ctx.datasources.static-data.x
          yAxis:
            isFirstLabelHidden: true
            isFirstTickHidden: true
            labels:
              format:
                compactDisplay: short
                notation: compact
                numberStyle: currency
            min: 0
            tickAmount: 5
      bottom: 
        type: component.titles
        options:
          title: Quarterly Company Progress
          subtitle: "2022"
          align: center            
```

grid-item

```yaml
# Grid-item for the jig.
children:
  - type: component.grid-item
    options:
      size: "2x2"
      children: 
        type: component.jig-widget
        options:
          jigId: chart-line-2_4x4
          widgetId: line2-4x4
```

:::
:::::

:::::ExpandableHeading

### Chart widget - line-chart component (4x2)

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/Mqh4r9GH4TOTnBy1_kXtQ_linechartiphone13blueportrait.png" size="80" position="center" caption="line-chart widget" alt="line-chart widget 4" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/Mqh4r9GH4TOTnBy1_kXtQ_linechartiphone13blueportrait.png"}
:::

:::VerticalSplitItem
This example is configured using a line-chart to display in the chart widget.

**Examples**:
See the complete example using static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/widgets/chart/static-data/chart-widget-with-line-chart/chart-widget-line-chart.jigx).
See the complete example using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/widgets/chart/dynamic-data/chart-widget-with-line-chart/chart-widget-line-dynamic.jigx).

**Datasources**:
See the complete datasource for static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/charts/static/series1.jigx).
See the complete datasource for dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/charts/dynamic/series1-dynamic.jigx)
:::
::::

:::CodeblockTabs
line-chart-widget (static)

```yaml
widgets:
  lineChartDD-4x2:
    type: widget.chart
    options:
      chart:
        type: component.line-chart
        options:
          chart:
            height: 150
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

line-chart-widget (dynamic)

```yaml
widgets:
  lineChartStatic-4x2:
    type: widget.chart
    options:
      chart:
        type: component.line-chart
        options:
          chart:
            height: 150
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
      size: "2x2"
      children: 
        type: component.jig-widget
        options:
          jigId: line-chart-widget 
          widgetId: lineChartDD-4x2
```

:::
:::::

:::::ExpandableHeading

### Chart widget: line-chart component in group widget (4x4)

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/klbestBzZ9mIfpOu6q7D__wd-linegroup.PNG" size="80" position="center" caption="Group widget with line-charts" alt="Group widget with line-charts" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/klbestBzZ9mIfpOu6q7D__wd-linegroup.PNG"}
:::

:::VerticalSplitItem
In this example two line-chart widgets are combined in the `group` widget with the `component.titles` to add additional information.

**Example:**
See the complete example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/widgets/4x2/combined-chart-chart-1_4x2.jigx).
:::
::::

:::CodeblockTabs
combined-chart-chart-1\_4x2.jigx

```yaml
title: Chart & Chart 1 (4x2)
type: jig.default

datasources:
  bitcoin:
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_REST
      entities:
        - entity: coin-history
          function: coin-history
          functionParameters:
            symbol: BTC-EUR
      query: |
        WITH cte AS (
          SELECT
            '$.ms' AS ms,
            '$.close' AS close
          FROM [coin-history]
          ORDER BY 1 DESC
        )
        SELECT
          1 - ROW_NUMBER() OVER (ORDER BY ms DESC) AS x,
          close AS y
        FROM cte
        ORDER BY
          ms DESC
        LIMIT 1 + 1 * 7

  etherum:
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_REST
      entities:
        - entity: coin-history-etherum
          function: coin-history-etherum
          functionParameters:
            symbol: ETH-EUR
      query: |
        WITH cte AS (
          SELECT
            '$.ms' AS ms,
            '$.close' AS close
          FROM [coin-history-etherum]
          ORDER BY 1 DESC
        )
        SELECT
          1 - ROW_NUMBER() OVER (ORDER BY ms DESC) AS x,
          close AS y
        FROM cte
        ORDER BY
          ms DESC
        LIMIT 1 + 1 * 7

children:
  - type: component.line-chart
    options:
      chart:
        height: 300
      legend:
        isHidden: false
      yAxis:
        labels:
          format:
            numberStyle: currency
            currency: EUR
        tickAmount: 6
      series:
        # - data: =@ctx.datasources.bitcoin.{'x':x,'y':y}
        - data: =@ctx.datasources.bitcoin
          color: color4
          name: Bitcoin EUR (last 7 days)
          layout: area-gradient

  - type: component.line-chart
    options:
      chart:
        height: 300
      legend:
        isHidden: false
      yAxis:
        labels:
          format:
            numberStyle: currency
            compactDisplay: short
            notation: compact
            currency: EUR
            maximumSignificantDigits: 5
            maximumFractionDigits: 5                      
        tickAmount: 3
      series:
        - data: =@ctx.datasources.etherum
          color: color4
          name: Etherum EUR (last 14 days)
          layout: area-gradient
# Add the widgets group, then the chart widget with the two line-chart components 
widgets:
  combined-chart1-4x2:
    type: widget.group
    options:
      children:
        - type: widget.chart
          
          options:
            top: 
              type: component.titles
              options:
                title: Bitcoin
                subtitle: BTC to EUR
            chart:
              type: component.line-chart
              options:
                plotOptions:
                  series:
                    marker:
                      isHidden: true
                legend:
                  isHidden: false
                xAxis:
                  isHidden: true
                yAxis:
                  labels:
                    format:
                      numberStyle: currency
                      compactDisplay: long
                      notation: standard
                      currency: EUR
                      maximumSignificantDigits: 5
                      maximumFractionDigits: 5
                  tickAmount: 3
                series:
                  - data: =@ctx.datasources.bitcoin
                    color: color4
                    name: Bitocin EUR (last 14 days)
                    layout: area-gradient

        - type: widget.chart
          options:
            top:
              type: component.titles
              options:
                title: Etherum
                subtitle: BTC to EUR
            chart:
              type: component.line-chart
              options:
                plotOptions:
                  series:
                    marker:
                      isHidden: true
                legend:
                  isHidden: false
                xAxis:
                  isHidden: true
                yAxis:
                  labels:
                    format:
                      numberStyle: currency
                      compactDisplay: short
                      notation: compact
                      currency: EUR
                      maximumSignificantDigits: 5
                      maximumFractionDigits: 5                      
                  tickAmount: 3
                series:
                  - data: =@ctx.datasources.etherum
                    color: color4
                    name: Etherum EUR (last 14 days)
                    layout: area-gradient

```

coin-history.jigx (function)

```yaml
method: GET
provider: DATA_PROVIDER_REST
parameters:
  symbol:
    value: BTC-EUR
    location: path
    type: string
    required: true
url: 'https://api.exchange.coinbase.com/products/BTC-EUR/candles'
outputTransform: >-
  $.{ "ms": $[0] * 1000, "close": $formatNumber($number($[4]), '#.00000000') }
```

coin-history-etherum.jigx (function)

```yaml
method: GET
provider: DATA_PROVIDER_REST
parameters:
  symbol:
    value: ETH-EUR
    location: path
    type: string
    required: true
url: 'https://api.exchange.coinbase.com/products/ETH-EUR/candles'
outputTransform: >-
  $.{ "ms": $[0] * 1000, "close": $formatNumber($number($[4]), '#.00000000') }
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
          jigId: combined-chart-chart-1_4x2
          widgetId: combined-chart1-4x2
```

:::
:::::

:::::ExpandableHeading

### Chart widget: bar-chart component (2x2)

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
In this example select the `chart` widget and add a `component.bar-chart` and add a `component.trend` at the `top`.

**Example:**
See the complete example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/widgets/2x2/chart-line-1_2x2.jigx).
:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/fp7s1B__h9Bjo1bbuR9-k_wd-bar22.PNG" size="80" position="center" caption="Bar-chart widget 2x2" alt="Bar-chart widget 2x2" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/fp7s1B__h9Bjo1bbuR9-k_wd-bar22.PNG"}
:::
::::

:::CodeblockTabs
chart-bar-1\_2x2.jigx

```yaml
widgets:
  line1-2x2:
    type: widget.chart
    options:
      top:
        type: component.trend
        options:
          title: "This Month"
          value: +11.81818181818
          
          format:
            numberStyle: unit
            unit: percent
             
          style:
            isAlignRight: true
            isValueHidden: false
            isValueBottom: true
      chart:
        type: component.bar-chart
        options:
          plotOptions:
            series:
              pointWidth: 12
          yAxis:
            max: 80
            min: 0
            tickAmount: 3
            labels:
              format:
                compactDisplay: short
                notation: compact
                numberStyle: currency
          xAxis:
            categories:
              - Aug
              - Sep
              - Oct
              - Nov
          series:
            - data: =@ctx.datasources.static-data-1
              color: color3
            - data: =@ctx.datasources.static-data-2
              color: positive
```

datasource

```yaml
datasources:
  static-data-1:
    type: datasource.static
    options:
      data:
        - 10
        - 25
        - 17
        - 10
  static-data-2:
    type: datasource.static
    options:
      data:
        - 15
        - 45
        - 55
        - 65
```

grid-item

```yaml
# Grid-item for the jig.
children:
  - type: component.grid-item
    options:
      size: "2x2"
      children: 
        type: component.jig-widget
        options:
          jigId: chart-bar-1_2x2
          widgetId: line1-2x2
```

:::
:::::

:::::ExpandableHeading

### Chart widget: bar-chart component (4x2)

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/Y3CKSyi1KM2u5eeo3bFHz_wd-bar42.PNG" size="80" position="center" caption="Bar-chart widget 4x2" alt="Bar-chart widget 4x2" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/Y3CKSyi1KM2u5eeo3bFHz_wd-bar42.PNG"}
:::

:::VerticalSplitItem
In this example a chart widget is used with the `component.bar-chart` and `component.titles` at the `top` to add a `title` and `subtitle`.

**Example:**
See the complete example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/widgets/4x2/chart-bar-1_4x2.jigx).
:::
::::

:::CodeblockTabs
chart-bar-1\_4x2.jigx

```yaml
widgets:
  bar1-4x2:
    type: widget.chart
    options:
      top:
        type: component.titles
        options:
         title: New Employees
         subtitle: "2021 vs. 2022"
         icon: multiple-neutral-2
         iconColor: color4
      chart:
        type: component.bar-chart
        options:
          plotOptions:
            series:
              pointWidth: 8
          yAxis:
            max: 100
          xAxis:
            categories: =@ctx.datasources.static-data-1.x
          series:
            - data: =@ctx.datasources.static-data-1
              color: color4
            - data: =@ctx.datasources.static-data-2
              color: color6                  
```

datasource

```yaml
datasources:
  static-data-1:
    type: datasource.static
    options:
      data:
        - y: 10
          x: Jun
        - y: 52
          x: Jul
        - y: 49
          x: Aug
        - y: 48
          x: Sep
  static-data-2:
    type: datasource.static
    options:
      data:
        - 20
        - 52
        - 52
        - 60
```

grid-item

```yaml
# Grid-item for the jig.
children:
  - type: component.grid-item
    options:
      size: "2x2"
      children: 
        type: component.jig-widget
        options:
          jigId: chart-bar-1_4x2
          widgetId: bar1-4x2
```

:::
:::::

:::::ExpandableHeading

### Chart widget: bar-chart component (4x2)

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/2aOyKeqQJOsjZiJRMpoIO_barchartiphone13blueportrait.png" size="80" position="center" caption="Bar-chart widget" alt="Bar-chart widget" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/2aOyKeqQJOsjZiJRMpoIO_barchartiphone13blueportrait.png"}
:::

:::VerticalSplitItem
This example is configured using a bar-chart to display in the chart widget.

**Examples**:
See the complete example using static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/widgets/chart/static-data/chart-widget-with-bar-chart/chart-widget-bar-chart.jigx).
See the complete example using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/widgets/chart/dynamic-data/chart-widget-with-bar-chart/chart-widget-bar-dynamic.jigx).

**Datasources**:
See the complete datasource for static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/charts/static/series1.jigx).
See the complete datasource for dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/charts/dynamic/series1-dynamic.jigx).
:::
::::

:::CodeblockTabs
bar-chart-widget (static)

```yaml
widgets:
  barChartStatic-4x2:
    type: widget.chart
    options:
      chart:
        type: component.bar-chart
        options:
          chart:
            height: 150
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
              dataLabels:
                - isEnabled: false
          legend:
            isHidden: false
```

bar-chart-widget (dynamic)

```yaml
widgets:
  barChartDD-4x2:
    type: widget.chart
    options:
      chart:
        type: component.bar-chart
        options:
          chart:
            height: 150
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
              dataLabels:
                - isEnabled: false
          legend:
            isHidden: false
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
          jigId: bar-chart-widget
          widgetId: barChartStatic-4x2
```

:::
:::::

:::::ExpandableHeading

### Chart widget: pie-chart component (2x2)

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/9aLZHIlMWl2SxoD9rn2V9_piechartiphone13blueportrait.png" size="80" position="center" caption="Pie-chart widget 2x" alt="Pie-chart widget 2x2" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/9aLZHIlMWl2SxoD9rn2V9_piechartiphone13blueportrait.png"}
:::

:::VerticalSplitItem
This example is configured using a pie-chart to display in the chart widget.

**Examples**:
See the complete example using static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/widgets/chart/static-data/chart-widget-with-pie-chart/chart-widget-pie-chart.jigx).
See the complete example using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/widgets/chart/dynamic-data/chart-widget-with-pie-chart/chart-widget-pie-dynamic.jigx).

**Datasources**:
See the complete datasource for static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/charts/static/pie-chart-data.jigx).
See the complete datasource for dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/charts/dynamic/pie-chart-dynamic.jigx).
:::
::::

:::CodeblockTabs
pie-chart-widget (static)

```yaml
widgets:
  pieChartDD-2x2:
    type: widget.chart
    options:
      chart:
        type: component.pie-chart
        options:
          chart:
            title:
              text: Issues
              verticalAlign: center
            width: 120
            height: 120
          legend:
            isHidden: true
          series:
              - data: =@ctx.datasources.pie-chart-data
                dataLabels:
                  - isEnabled: true
                layout: pie
```

pie-chart-widget (dynamic)

```yaml
widgets:
  pieChartStatic-2x2:
    type: widget.chart
    options:
      chart:
        type: component.pie-chart
        options:
          chart:
            title:
              text: Issues
              verticalAlign: center
            width: 120
            height: 120
          legend:
            isHidden: true
          series:
              - data: =@ctx.datasources.pie-chart-dynamic
                dataLabels:
                  - isEnabled: true
                layout: pie
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
          jigId: pie-chart-widget
          widgetId: pieChartDD-2x2
```

:::
:::::

:::::ExpandableHeading

### Chart widget: pie-chart component (2x4)

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
In this example a chart widget is used with the `component.pie-chart` and `component.titles` at the `top` and `bottom` to add additional information.

**Example:**
See the complete example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/widgets/2x4/chart-pie-1_2x4.jigx).
:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/FA-eiRkpMZ-BpHy1o-b6s_wd-pie2x4.PNG" size="80" position="center" caption="Pie-chart widget 2x4" alt="Pie-chart widget 2x4" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/FA-eiRkpMZ-BpHy1o-b6s_wd-pie2x4.PNG"}
:::
::::

:::CodeblockTabs
chart-pie-1\_2x4.jigx

```yaml
widgets:
  pie1-2x4: 
    type: widget.chart
    options:        
      chart: 
        type: component.pie-chart
        options:
          chart:
            title:
              text: "67%"
              verticalAlign: center
            subtitle:
              text: "Battery"
              verticalAlign: center              
          series:
            - data: =@ctx.datasources.static-data
              layout: arch
              color: positive
      top:
        type: component.titles
        options:
          title: Vojta iPhone
          subtitle: iPhone 14 Pro
          align: center
          icon: mobile-phone-1
          iconColor: color14
      bottom:
        type: component.titles
        options:
          title: 10,75 GB (of 256 GB)          
          subtitle: Available
          align: center
          icon: database-2
```

datasource

```yaml
datasources:
  static-data:
    type: datasource.static
    options:
      data:
        - y: 67
        - y: 23
          color: transparent
```

grid-item

```yaml
# Grid-item for the jig.
children:
  - type: component.grid-item
    options:
      size: "2x2"
      children: 
        type: component.jig-widget
        options:
          jigId: chart-pie-1_2x4
          widgetId: pie1-2x4
```

:::
:::::

:::::ExpandableHeading

### Chart widget: pie-chart component in group widget (4x4)

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
In this example a `group` widget is used to combine a `chart` and `list` widget  with `component.pie-chart` and  `component.titles` at the `top` to add additional information.

**Example:**
See the complete example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/widgets/4x2/combined-chart-list-1_4x2.jigx).
:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/zS66aUyNJyNwAzzhSZ1pP_wd-combinedpie.PNG" size="80" position="center" caption="Group widget 4x" alt signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/zS66aUyNJyNwAzzhSZ1pP_wd-combinedpie.PNG"}
:::
::::

:::CodeblockTabs
combined-chart-list-1\_4x2.jigx

```yaml
widgets:
  chart-list1-4x2: 
    type: widget.group
    options:
      children:
        - type: widget.chart
          options:        
            chart: 
              type: component.pie-chart
              options:
                chart:
                  title: 
                    text: "3 of 5"
                    verticalAlign: center
                  subtitle: 
                    text: Done
                    verticalAlign: center
            
                series:
                  - data: =@ctx.datasources.chart
                    layout: pie
                    color: color3
            top:
              type: component.titles
              options:
                title: Onboarding
                subtitle: Jigx, Inc.
                align: center   

        - type: widget.list
          options:
            data: =@ctx.datasources.list
            item: 
              type: component.list-item
              options:
                color:
                  - when: =(@ctx.current.item.status = 'done' ? true :false)
                    color: color14
                  - when: =(@ctx.current.item.status = 'waiting' ? true :false)
                    color: color1
                title: =@ctx.current.item.task-number
                subtitle: =@ctx.current.item.name
                leftElement: 
                  element: checkbox
                  value: =(@ctx.current.item.status = 'done' ? true :false)
                style:
                  isStrikeThrough: =(@ctx.current.item.status = 'done' ? true :false)
                  isDisabled: =(@ctx.current.item.status = 'done' ? true :false)
 
```

datasource

```yaml
datasources:
  chart:
    type: datasource.static
    options:
      data:
        - y: 3
        - y: 2
          color: transparent
  list:
    type: datasource.static
    options:
      data:
        - icon: person
          task-number: Task 4
          name: Meet With Colleagues
          status: waiting     
        - icon: checklist
          task-number: Task 5
          name: Use Jigx App
          status: waiting
        - icon: synchronize-arrows-1
          task-number: Task 3
          name: Meet Your Manager
          status: done       
        - icon: synchronize-arrows-1
          task-number: Task 2
          name: Set Email & Calendar
          status: done       
        - icon: play
          task-number: Task 1
          name: Watch Jigx Intro Video
          status: done
```

grid-item

```yaml
# Grid-item for the jig.
children:
  - type: component.grid-item
    options:
      size: "2x2"
      children: 
        type: component.jig-widget
        options:
          jigId: combined-chart-list-1_4x2
          widgetId: chart-list1-4x2
```

:::
:::::
