---
title: charts
slug: n5MH-charts
createdAt: Wed Oct 12 2022 08:42:41 GMT+0000 (Coordinated Universal Time)
updatedAt: Wed Jan 17 2024 10:18:12 GMT+0000 (Coordinated Universal Time)
description: >-
  Learn how to use the Jigx component to display statistics for categorical
  variables in this informative document. Discover examples of converting data
  formats like Excel, Jigx dynamic data tables, and
---

# charts

The component can display statistics related to data records (categorical variables). This can be used to show a single series or multiple series of data for comparative purposes and highlight specific regions or ranges on the chart to make it easier for users to interpret and analyze the data.This component is mostly used in [jig.default](<../Jig Types/jig_default.md>) or [jig.list](<../Jig Types/jig_list.md>).

::::LinkArray :::LinkArrayItem{headerType="IMAGE" headerImage="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/mYNg-6TNdRQaZMKGrcqsN\_bar-chart.png"} Bar chart

[Show more](charts/bar-chart.md) :::

:::LinkArrayItem{headerType="IMAGE" headerImage="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/3vTze\_ECdOVAFIFGq1LIq\_pie-chart.png"} Pie Chart

[Show more](charts/pie-chart.md) :::

:::LinkArrayItem{headerType="IMAGE" headerImage="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/fAmrDPB1PsqwCbgVNS2Ab\_line-chart.png"} Line chart

[Show more](charts/line-chart.md) :::

:::LinkArrayItem{headerType="IMAGE" headerImage="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/urCrWekO3-jrmGSAbGo2L\_charts-bar-plotbands-s.png"} [Show more](charts/bar-chart.md) :::

:::LinkArrayItem{headerType="IMAGE" headerImage="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/XWHCno5Z1WQ5HDglihnNr\_charts-line-plotbands-s.png"} [Show more](charts/line-chart.md) ::: ::::

### Understanding chart data

Chart data is structured in a way that makes it easy to display. To understand how to create the YAML for a chart in Jigx Builder let's look at the data in various formats and how you can use the data in Jigx.

* Let's start with the financial data per quarter for three years from a **Microsoft Excel** table, as shown below:

::Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/UcOTckXGJkUjlVRuGnuFp\_c-exceldata.png" size="80" position="center" caption="Excel data table" alt="Excel data table"}

* Next we map out the same data in Jigx [Dynamic Data](https://docs.jigx.com/dynamic-data) in[Jigx Management](https://docs.jigx.com/data). Notice that the data is exactly the same as the Excel data.

![Dynamic Data table](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/jZg3JrV65OcMvWRhadDqA_c-dd-data.png)

* The same data can also exist in a **JSON** file. Using the _Download_ button at the top-right of the Data-finance-data table shown above will download the data into a JSON file. The JSON is shown below.

::Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/dz517cISeRt0lkq-Y5v7y\_c-json.png" size="80" position="center" caption="JSON data" alt="JSON data"}

### Using the data in YAML

Now that you have your data you can convert it into the YAML needed for the charts. The data can be used as a static datasource or a dynamic datasource.

#### YAML - Static data

Using the _finance-data.json_ it was easy to convert the data into YAML as shown below.

:::CodeblockTabs static-data

```yaml
datasources:
  finance:
    type: datasource.static
    options:
      data:
        - Q1: 34000
          Q2: 22000
          Q3: 40000
          Q4: 51000
          Year: "2021"
        - Q1: 12000
          Q2: 48000
          Q3: 36000
          Q4: 12000
          Year: "2020"
        - Q1: 25000
          Q2: 32000
          Q3: 45000
          Q4: 86000
          Year: "2019"
```

:::

#### YAML - Dynamic Data

In Jigx you can use the data from the dynamic data table, in this instance _data-Finance-data_, then create a file under datasource folder. Use the Dynamic data provider that references the finance-data table with a query selecting the data you want to use, quarters and year in this example.

:::CodeblockTabs dynamic-data

```yaml
type: datasource.sqlite
options:
  provider: DATA_PROVIDER_DYNAMIC

  entities:
    - default/finance-data

  query: |
    SELECT
      id,
      '$.Q1', 
      '$.Q2', 
      '$.Q3', 
      '$.Q4', 
      '$.Year' 
    FROM [default/finance-data]
```

:::

#### YAML - Chart

In the YAML for charts the following keys are used: - `yAxis` - `xAxis` - `categories` - `series`

In this example the _finance-data_ would show as follows for each key.

::Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/O3Z8Q9pXGBC1kbaz-qH9s\_c-yamlkey.png" size="54" position="center" caption="Chart YAML data described" alt="Chart YAML data described"}

Now it is possible to create charts in YAML with the exact same data, for example a bar and line chart with the finance-data in the above YAML keys is shown below. Notice in the YAML below that the same YAML is used for both the bar and line chart.

:::CodeblockTabs Bar-chart

```yaml
children:
  # select the BAR-CHART component and configure the x-axis and y-axis
  - type: component.bar-chart
    options:
      chart:
        height: 250
      legend:
        isHidden: false

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

      xAxis:
        categories: =@ctx.datasources.finance-data-dd.Year

      series:
        - data: =@ctx.datasources.finance-data-dd.Q1
          name: Q1
          color: color2

        - data: =@ctx.datasources.finance-data-dd.Q2
          name: Q2
          color: color3

        - data: =@ctx.datasources.finance-data-dd.Q3
          name: Q3
          color: color4

        - data: =@ctx.datasources.finance-data-dd.Q4
          name: Q4
          color: color5
```

Line-chart

```yaml
children:
  # select the LINE-CHART component and configure the x-axis and y-axis
  - type: component.line-chart
    options:
      chart:
        height: 250
      legend:
        isHidden: false

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

      xAxis:
        categories: =@ctx.datasources.multi.Year

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

:::

::::VerticalSplit{layout="middle"} :::VerticalSplitItem The `component.bar-chart` in the Jigx App using the finance- data.

::Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/ssjfdQ\_2eC20t8-KJZYKQ\_c-barmultiexplained.png" size="74" position="center" caption="Bar chart in Jigx App" alt="Bar chart in Jigx App"} :::

:::VerticalSplitItem The `component.line-chart` in the Jigx App using the finance- data.

![Line chart in Jigx](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/jm-81Q_XeyBlWOAAY5A4M_c-lineexample.PNG) ::: ::::
