# bar-chart

::::VerticalSplit{layout="middle"} :::VerticalSplitItem The component can display statistics related to data records (categorical variables) represented in a bar chart. This can show a single or multiple data series for comparative purposes and highlight specific regions or ranges on the chart to make it easier for users to interpret and analyze the data. This component is mostly used in [jig.default](<../../Jig Types/jig_default.md>) or [jig.list](<../../Jig Types/jig_list.md>). :::

:::VerticalSplitItem ::Image\[]{alt="Bar Chart Preview" src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/FNwqF58yNsXcKrMxDsANE\_bar-chart.png" size="86" caption="Bar Chart Preview" position="center" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/FNwqF58yNsXcKrMxDsANE\_bar-chart.png" width="800" height="604" darkWidth="800" darkHeight="604"} ::: ::::

### Configuration options

Some properties are common to all components, see [Common component properties](bar-chart.md) for a list and their configuration options.

<table><thead><tr><th width="158.7578125">Core structure</th><th></th></tr></thead><tbody><tr><td><code>series</code></td><td><code>color</code> - defines the color of the bar used in the chart.</td></tr><tr><td><code>data</code></td><td>values to be used in the chart.</td></tr><tr><td><code>yAxis</code></td><td><code>min</code> and <code>max</code> values that display on the y-axis. The <code>max</code> property doesn't have to be defined, in this case, it will automatically be calculated depending on your data.</td></tr><tr><td><code>xAxis</code></td><td><code>categories</code> to display on the x-axis</td></tr></tbody></table>

<table><thead><tr><th width="163.85546875">Other options</th><th></th></tr></thead><tbody><tr><td><code>chart</code></td><td><ul><li><code>title</code>and <code>subtitle</code> - Name and a short description of your chart.</li><li><code>height</code> and <code>width</code> - The parameters of the graph displayed (in pixels).</li></ul></td></tr><tr><td><code>legend</code></td><td><code>isHidden</code> - The setting of a boolean value if the legend (naming of the series) should be displayed under the chart.</td></tr><tr><td><code>plotBands</code></td><td>The <code>from</code> and <code>to</code> properties define the area to be filled with color. Specify the range using the from and to properties with numeric values. <code>color</code> Sets the color of the band for the <code>y-axis</code>, choose a color from the provided color palette. Use <code>plotbands</code> to highlight specific regions or ranges on the chart, making it easier for users to interpret and analyze the data.</td></tr><tr><td><code>plotOptions</code></td><td><code>series</code> - Different properties available to manipulate the data shown in the bar such as width of columns, the interval between two points, option to hide markers.</td></tr><tr><td><code>series</code></td><td><code>name</code> - The naming of the actual series.</td></tr><tr><td><code>xAxis</code></td><td><ul><li><code>isFirstLabelHidden</code> value is either <code>true</code> to hide the first label or <code>false</code> to display the first label. The property doesn't have to be defined, by default the first label is shown.</li><li><code>isFirstTickHidden</code> value is either true/false. Set to <code>true</code> hides the whole axis.</li><li><code>isHidden</code> value is either true/false.</li><li><code>isLastLabelHidden</code> value is either <code>true</code> to hide the last label or <code>false</code> to display the last label. The property doesn't have to be defined, by default the last label are shown.</li><li><code>isLastTickHidden</code> value is either <code>true</code> to hide the last line and label or <code>false</code> to display the last line and label. The property doesn't have to be defined, by default the last label and line are shown.</li><li><code>labels</code> - Label of axis, a selection of different formats such as <code>dateFormat</code>, <code>currency</code>, <code>unit</code>, and <code>signDisplay</code> are available.</li><li><code>min</code> and <code>max</code> - Minimum and maximum values that should be displayed on the x-axis.</li><li><code>minPadding</code> - When no categories set, a 1% space is made on the left and right of the chart so the id doesn't start on the left or ends on the right edge exactly. The default is set to 0.02 (x-axis) and 0.05 (y-axis).</li><li><code>tickAmount</code> - The number of ticks to display on the x-axis. The final amount doesn't have to be exactly the same number as you pass into it. Round up to 6 to give the chart a good set of numbers 0, 20, 40, 60, 80, 100. Set ticks to 3 will be honored and shows 0, 50, and 100.</li></ul></td></tr><tr><td><code>yAxis</code></td><td><ul><li><code>isFirstLabelHidden</code> value is either true/false. Set to <code>true</code> hides the first label. The property doesn't have to be defined, by default the first label is shown.</li><li><code>isFirstTickHidden</code> value is either true/false. Set to <code>true</code> hides the whole axis.</li><li><code>isHidden</code> value is either true/false. Set to <code>true</code> the last label is hidden.</li><li><code>isLastLabelHidden</code> value is either <code>true</code> to hide the last label and line or <code>false</code> to display the last label and line. The property doesn't have to be defined, by default the last label and line are shown.</li><li><code>isLastTickHidden</code> value is either <code>true</code> to hide the last line and label or <code>false</code> to display the last line and label. The property doesn't have to be defined, by default the last label and line are shown.</li><li><code>labels</code> - Label of axis, a selection of different formats such as <code>currency</code>, <code>numberStyle</code>, <code>compactDisplay</code> and <code>notation</code> is available.</li><li><code>minPadding</code> - When no categories set, a 1% space is made on the left and right of the chart so the id doesn't start on the left or ends on the right edge exactly. The default is set to 0.02 (x-axis) and 0.05 (y-axis).</li><li><code>min</code> and <code>max</code> - Minimum and maximum values that should be displayed on the y-axis.</li><li><code>tickAmount</code> - The number of ticks to display on the x-axis. The final amount doesn't have to be exactly the same number as you pass into it. Round up to 6 to give the chart a good set of numbers 0, 20, 40, 60, 80, 100. Set ticks to 3 will be honored and shows 0, 50, and 100</li></ul></td></tr></tbody></table>

### Examples and code snippets

#### Bar-chart finance static

::::VerticalSplit{layout="middle"} :::VerticalSplitItem ![Finance bar-chart](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/8Z28MLwf3pqS_7EEZqmRC_weml0oui8khi-mqiu-dbbbar-chart-singleiphone13blueportrait.png) :::

:::VerticalSplitItem The jig displays a bar chart with an annual overview of finances. The x-axis shows the months and the y-axis the monetary amount. Using number formatting, we can have any currency displayed.

**Examples:** See the full code sample using static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/bar-chart/static-data/bar-chart-finance-statistic/bar-chart-finance-statistic.jigx). See the full code sample using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/bar-chart/dynamic-data/bar-chart-finance-dynamic/bar-chart-finance-dynamic.jigx).

**Datasources:** See the full datasource code sample for dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/tree/main/quickstart/jigx-samples/jigs/jigx-components/bar-chart/dynamic-data/bar-chart-finance-dynamic).&#x20;

:::CodeblockTabs bar-chart (static)

```yaml
title: Current account overview
type: jig.default

datasources:
  finance: 
    type: datasource.static
    options:
      data:
        - date: Jun
          amount: 1851
        - date: Jul
          amount: 1483
        - date: Aug
          amount: 1250  
        - date: Sep
          amount: 2067
        - date: Oct
          amount: 1650
        - date: Nov
          amount: 1280
        - date: Dec
          amount: 1430
        - date: Jan
          amount: 1398
        - date: Feb
          amount: 1763
        - date: Mar
          amount: 2151
        - date: Apr
          amount: 1543
        - date: May
          amount: 1475    
                  
children:
  - type: component.bar-chart
    options:
      chart:
        title:
          text: 12 months overview
        height: 260
# Define the format and labels for and their values to display on the y axis
      yAxis:
        min: 0
        max: 2500
        labels: 
          format:
            numberStyle: currency
            currency: USD
            compactDisplay: short
            notation: compact
        tickAmount: 5
      # Define the data categories to display on the x axis
      xAxis:
        categories: =@ctx.datasources.finance.date       
      # Define the data to show in the bars on the chart known as the series. 
      series:
        - data: =@ctx.datasources.finance.amount
          name: 2021/2022
          color: color1 
      legend:
        isHidden: false
```

bar-chart (dynamic)

```yaml
children:
  - type: component.bar-chart
    options:
      chart:
        title:
          text: "12 months overview"
        height: 260
        isAnimated: false
      legend:
        isHidden: true
      yAxis:
        min: 0
        labels:
          format:
            numberStyle: currency
            currency: USD
            compactDisplay: short
            notation: compact
        tickAmount: 5
        isFirstTickHidden: false
        isFirstLabelHidden: false
      series:
        - data: =@ctx.datasources.finance-dynamic
          name: "2021/2022"
          color: color2
```

datasources (dynamic)

```yaml
datasources:
  finance-dynamic:
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_DYNAMIC
      entities:
        - entity: default/finances
      query: |
        SELECT 
          id, 
          json_extract(data, '$.date') as x, 
          json_extract(data, '$.amount') as y, 
          '$.financeid', 
          '$.category' 
        FROM [default/finances] WHERE '$.category' = "finance-month" ORDER BY '$.financeid' ASC
```

#### Bar-chart multiple series

::::VerticalSplit{layout="middle"} :::VerticalSplitItem ::Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/Y0mOpU1tdF-6Q5inYOHBx\_c-barmultiseries.PNG" size="80" position="center" caption="Multiple series" alt="Multiple series" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/Y0mOpU1tdF-6Q5inYOHBx\_c-barmultiseries.PNG" width="800" height="1613" darkWidth="800" darkHeight="1613"} :::

:::VerticalSplitItem The jig displays a bar chart with four series that compares amounts for three years per quarter. In this example the `Legend` is shown.

**Examples:** See the full code sample using static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/bar-chart/static-data/bar-chart-multiple-series/bar-chart-multiple-series.jigx). See the full code sample using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/bar-chart/dynamic-data/bar-chart-multiple-series-dynamic/bar-chart-multiple-dynamic.jigx).

**Datasources in order series1 and series2:** See the full datasource code sample for dynamic data [series 1](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/charts/dynamic/series1-dynamic.jigx) and [series 2](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/charts/dynamic/series2-dynamic.jigx) in GitHub.&#x20;

:::CodeblockTabs bar-chart-multiple (static)

```yaml
title: Multiple series
type: jig.default
# Define the data to be used in the chart
datasources:
  multi:
    type: datasource.static
    options:
      data:
        - Q1: 12000
          Q2: 48000
          Q3: 36000
          Q4: 12000
          Year: "2020"
        - Q1: 34000
          Q2: 22000
          Q3: 40000
          Q4: 51000
          Year: "2021"
        - Q1: 25000
          Q2: 32000
          Q3: 45000
          Q4: 86000
          Year: "2019"              

children:
  - type: component.bar-chart
    options:
      chart:
        height: 250
      legend:
        isHidden: false
        # Define the format, labels to display on the y axis
      yAxis: 
        max: 90000
        min: 0
        labels:  
          format:
            currency: USD
            numberStyle: currency
            compactDisplay: short
            notation: compact
        tickAmount: 8
      # Define the data categories to display on the x axis   
      xAxis:   
        categories: =@ctx.datasources.multi.Year
        # Define the data to show in the bars on the chart known as the series. 
      series: 
        - data: =@ctx.datasources.multi.Q1
          name: Q1
          color: color2
          
        - data: =@ctx.datasources.multi.Q2
          name: Q2
          color: color3
         
        - data: =@ctx.datasources.multi.Q3
          name: Q3
          color: color4
          
        - data: =@ctx.datasources.multi.Q4
          name: Q4
          color: color5
```

bar-chart-multiple (dynamic)

```yaml
children:
  - type: component.bar-chart
    options:
      chart:
        height: 250
      yAxis:
        max: 25
      xAxis:
        categories:
          - 'Sample Data'
      series:
        - data: =@ctx.datasources.series1-dynamic.data
        - data: =@ctx.datasources.series2-dynamic.data
```

datasources (dynamic)

```yaml
datasources:
  series1-dynamic:
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_DYNAMIC
      entities:
        - entity: default/charts
      query: | 
        SELECT 
          id, 
          json_extract(data, '$.seriesy') as y, 
          '$.color', 
          '$.category', 
          json_extract(data, '$.seriesx') as x, 
          '$.subtitle', 
          '$.title' 
        FROM [default/charts] WHERE '$.category' = "chart1" ORDER BY x
  
  series2-dynamic:
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_DYNAMIC
      entities:
        - entity: default/charts
      query: |
        SELECT 
          id, 
          json_extract(data, '$.seriesy') as y, 
          '$.color', 
          '$.category', 
          json_extract(data, '$.seriesx') as x, 
          '$.subtitle', 
          '$.title' 
        FROM [default/charts] WHERE '$.category' = "chart2" ORDER BY x
    
```

#### Bar-chart with plot bands

::::VerticalSplit{layout="middle"} :::VerticalSplitItem The jig displays a bar chart with an annual overview of finances. The x-axis shows the months and the y-axis the monetary amount. The data points are easy to see as we used the `plotBands` property to add color. In this example multiple bands are defined by adding the form, to and color properties.

**Examples:** See the full code sample in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/bar-chart/dynamic-data/bar-chart-finance-dynamic/bar-charts-plotBands.jigx).

:::VerticalSplitItem ::Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/EP5F4QeY\_kyU4tfa\_QRG-\_charts-bar-plotbands.PNG" size="80" position="center" caption="Bar chart with plot bands" alt="Bar chart with plot bands" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/EP5F4QeY\_kyU4tfa\_QRG-\_charts-bar-plotbands.PNG" width="800" height="1613" darkWidth="800" darkHeight="1613"} ::: ::::

:::CodeblockTabs bar-chart-plotbands

```yaml
title: Current account overview
type: jig.default

datasources:
  finance: 
    type: datasource.static
    options:
      data:
        - date: Jun
          amount: 1851
        - date: Jul
          amount: 1483
        - date: Aug
          amount: 1250  
        - date: Sep
          amount: 2067
        - date: Oct
          amount: 1650
        - date: Nov
          amount: 1280
        - date: Dec
          amount: 1430
        - date: Jan
          amount: 1398
        - date: Feb
          amount: 1763
        - date: Mar
          amount: 2151
        - date: Apr
          amount: 1543
        - date: May
          amount: 1475    
                  
children:
  - type: component.bar-chart
    options:
      chart:
        title:
          text: 12 months overview
        height: 260
# Define the format and labels for and their values to display on the y axis
      yAxis:
        min: 0
        max: 2500
        labels: 
          format:
            numberStyle: currency
            currency: USD
            compactDisplay: short
            notation: compact
        tickAmount: 5
    # add four bands of different color to the bar chart     
        plotBands:
          - from: 0
            to: 500
            color: color4
          - from: 500
            to: 1000
            color: color5
          - from: 1000
            to: 1500
            color: color6
          - from: 1500
            to: 2000
            color: color7
      # Define the data categories to display on the x axis
      xAxis:
        categories: =@ctx.datasources.finance.date       
      # Define the data to show in the bars on the chart known as the series. 
      series:
        - data: =@ctx.datasources.finance.amount
          name: 2021/2022
          color: color1 
      legend:
        isHidden: false
```

#### Bar-chart using expressions

::::VerticalSplit{layout="middle"} :::VerticalSplitItem ::Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/QoIeM\_NRC-TWN5R079CYy\_cc-barchartexpression.PNG" size="74" position="center" caption="Bar-chart using expressions" alt="Bar-chart using expressions" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/QoIeM\_NRC-TWN5R079CYy\_cc-barchartexpression.PNG" width="800" height="1613" darkWidth="800" darkHeight="1613"} :::

:::VerticalSplitItem In this example expressions are used to dertermine the `series`, `categories`, `min`, `max`, and `tickAmount` of a bar chart . The x-axis shows the quarters and the y-axis the monetary amount using the `format` property to display the currency.

**Examples:** See the full code sample in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/bar-chart/dynamic-data/bar-chart-multiple-series-dynamic/bar-chart-multiple-dynamic.jigx).

**Datasources** See the full datasource code sample for [series 1](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/charts/dynamic/series1-dynamic.jigx) and [series 2](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/charts/dynamic/series2-dynamic.jigx) in GitHub.

:::CodeblockTabs bar-chart-multiple-dynamic

```yaml
#Add file to the jigs folder
title: Multiple series dynamic
type: jig.default
children:
  - type: component.bar-chart
    options:
      chart:
        height: 250
      series:
        - data: =@ctx.datasources.series1.y
        - data: =@ctx.datasources.series2.y
      xAxis:
        categories: 
          - =@ctx.datasources.series1[0].x
          - =@ctx.datasources.series1[1].x
          - =@ctx.datasources.series1[2].x
          - =@ctx.datasources.series1[3].x
      yAxis: 
        labels:
          format:
            compactDisplay: short
            currency: USD
            notation: compact
            numberStyle: currency
        min: =@ctx.datasources.series2[0].min
        tickAmount: =@ctx.datasources.series2[0].tickAmount
        max: =@ctx.datasources.series2[0].max 
```

series1

```yaml
#Add file to the datasource folder
type: datasource.static
options:
  data:
    - x: Q1/20
      y: 25000
      color: color2
    - x: Q2/20
      y: 32000
      color: color2
    - x: Q3/20
      y: 45000
      color: color2
    - x: Q4/20
      y: 86000
      color: color2
```

series2

```yaml
#Add file to the datasource folder
type: datasource.static
options:
  data:
    - x: Q1/20
      y: 12000
      color: color3
      min: 0
      max: 127000
      tickAmount: 6
    - x: Q2/20
      y: 48000
      color: color3
      min: 0
      max: 127000
      tickAmount: 6
    - x: Q3/20
      y: 36000
      min: 0
      max: 127000
      tickAmount: 6
      color: color3
    - x: Q4/20
      y: 120000
      color: color3
      min: 0
      max: 127000
      tickAmount: 6 
```
