---
title: pie-chart
slug: P04R-pie-chart
description: This document provides information about a component for displaying statistics related to data records. Learn about the features and options for the Pie Chart component, along with its configuration and actions. Find code snippets, examples, and sample da
createdAt: Thu Jun 09 2022 19:43:04 GMT+0000 (Coordinated Universal Time)
updatedAt: Wed Jul 24 2024 09:50:15 GMT+0000 (Coordinated Universal Time)
---

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
The component can be used to display statistics related to data records. Mostly used in [jig.default](<./../../Jig Types/jig_default.md>) or [jig.list](<./../../Jig Types/jig_list.md>).
:::

:::VerticalSplitItem
![Pie Chart Preview](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/CEsXqKXctc_APbWr9-1G9_pie-chart.png "Pie Chart Preview")
:::
::::

:::hint{type="warning"}
We are currently experiencing issues with the legend of the Pie Chart component. We are working hard to fix this issue.
:::

## Configuration options

Some properties are common to all components, see [Common component properties](docId\:LLnTD-rxe8FmH7WpC5cZb) for a list and their configuration options.

| **Core structure** |                                                                                                    |
| ------------------ | ------------------------------------------------------------------------------------------------------------ |
| `chart`            | `title`- Its `text` and `verticalAlign`.                                                                     |
| `series`           | `data` - values to be used in the chart.&#xA;`layout` -  `Pie` or `Arch` - the availabe types of chart.  |

|**Other options** |                                                                                         |
| ----------------- | -------------------------------------------------------------------------------------------------------------------------------------------------- |
| `chart`           | `title `and `subtitle` - Name and a short description of your chart.&#xA;`height` and `width` - The parameters of the chart displayed (in pixels). |
| `legend`          | `isHidden` -  The setting of a boolean value if the legend (naming of the series) should be displayed under the chart.                             |
| `series`          | `name` - The naming of the actual series.&#xA;`color`- select a color from the color palette.                                                      |

| **Actions** |  |
| ----------- | ------------------------------------------------------------------------------------------------------------------------------------------------ |
| `onPress`   | The ability to add any of the actions (please refer to the list of  Actions). This action(s) will be triggered as a reaction to the press event. |

## Examples and code snippets

:::::ExpandableHeading
### Pie chart

::::VerticalSplit{layout}
:::VerticalSplitItem
![Pie Chart](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/CAWSPzutiCMFmb4gxIrya_w40z-dj51d0ecr9n92ccvpiechartiphone13blueportrait.png "Pie Chart")
:::

:::VerticalSplitItem
This jig displays a complete pie chart. In this example, these are issues where green shows resolved issues, yellow issues in progress, and red unresolved issues.

**Examples:**
See the full code sample using static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/pie-chart/static-data/pie-chart/pie-chart.jigx).
See the full code sample using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/pie-chart/dynamic-data/pie-chart/pie-chart-dynamic.jigx).

**Datasources:**
See the full datasource code sample for dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/charts/dynamic/pie-chart-dynamic.jigx).
:::
::::

:::CodeblockTabs
pie-chart (static)

```yaml
children:
  - type: component.pie-chart
    options:
      chart:
        title:
          text: Issues
          verticalAlign: center
        width: 180
        height: 180
      legend:
          isHidden: true
      series:
          - data: =[{"y":1, "color":"color4"}, {"y":2, "color":"color2"}, {"y":3, "color":"color3"}]
            dataLabels:
              - isEnabled: true
            layout: pie
```

pie-chart (dynamic)

```yaml
children:
  - type: component.pie-chart
    options:
      chart:
        title:
          text: Issues
          verticalAlign: center
        width: 180
        height: 180
      legend:
          isHidden: true
      series:
          - data: =@ctx.datasources.pie-chart-dynamic
            dataLabels:
              - isEnabled: true
            layout: pie
```

datasources (dynamic)

```yaml
datasources:
  pie-chart-dynamic:
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
        FROM [default/charts] WHERE '$.category' = "pie-chart"
    
```
:::
:::::

:::::ExpandableHeading
### Pie chart type arch

::::VerticalSplit{layout}
:::VerticalSplitItem
![Pie chart - arch](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/4-g91a_Saz9YXCiIcWHcR_bco9qdkyaolqvlk3xgf8gpie-chart-archchartiphone13blueportrait.png "Pie chart - arch")
:::

:::VerticalSplitItem
This jig displays an arc pie chart. This example shows the occupancy in a warehouse; the green color shows available space and the red color indicates occupied space.

**Examples:**
See the full code sample using static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/pie-chart/static-data/pie-chart-arch/pie-chart-arch.jigx).
See the full code sample using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/pie-chart/dynamic-data/pie-chart-arch/pie-chart-arch-dynamic.jigx).

**Datasources:**
See the full datasource code sample for dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/charts/dynamic/pie-arch-chart-dynamic.jigx).
::::

:::CodeblockTabs
arch-chart (static)

```yaml
children:
  - type: component.pie-chart
    options:
      chart:
        title:
          text: Stock
          verticalAlign: center
        width: 180
        height: 180
      legend:
          isHidden: true
      series:
          - data: =[{"y":1, "color":"color4"}, {"y":2, "color":"color2"}]
            dataLabels:
              - isEnabled: true
            layout: arch
```

arch-chart (dynamic)

```yaml
title: Arch pie chart
type: jig.default

children:
  - type: component.pie-chart
    options:
      chart:
        title:
          text: Stock
          verticalAlign: center
        width: 180
        height: 180
      legend:
          isHidden: true
      series:
          - data: =@ctx.datasources.pie-arch-chart-dynamic
            dataLabels:
              - isEnabled: true
            layout: arch
```

datasources (dynamic)

```yaml
datasources:
  pie-arch-chart-dynamic:
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
        FROM [default/charts] WHERE '$.category' = "arch-chart"
```
:::
:::::

