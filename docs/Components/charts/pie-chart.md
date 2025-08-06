# pie-chart

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

Some properties are common to all components, see [Common component properties]() for a list and their configuration options.

<table isTableHeaderOn="true" selectedColumns="" selectedRows="" selectedTable="false">
  <tr>
    <td selected="false" align="left">
      <p><strong>Core structure</strong></p>
    </td>
    <td selected="false" align="left">
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>chart</code></p>
    </td>
    <td selected="false" align="left">
      <p><code>title</code>- Its <code>text</code> and <code>verticalAlign</code>.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>series</code></p>
    </td>
    <td selected="false" align="left">
      <ul>
      <li><code>data</code> - values to be used in the chart.</li>
      <li><code>layout</code> -  <code>Pie</code> or <code>Arch</code> - the availabe types of chart.</li>
      </ul>
    </td>
  </tr>
</table>

<table isTableHeaderOn="true" selectedColumns="" selectedRows="" selectedTable="false">
  <tr>
    <td selected="false" align="left">
      <p><strong>Other options</strong></p>
    </td>
    <td selected="false" align="left">
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>chart</code></p>
    </td>
    <td selected="false" align="left">
      <ul>
      <li><code>title</code> and <code>subtitle</code> - Name and a short description of your chart.</li>
      <li><code>height</code> and <code>width</code> - The parameters of the chart displayed (in pixels).</li>
      </ul>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>legend</code></p>
    </td>
    <td selected="false" align="left">
      <p><code>isHidden</code> -  The setting of a boolean value if the legend (naming of the series) should be displayed under the chart.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>series</code></p>
    </td>
    <td selected="false" align="left">
      <ul>
      <li><code>name</code> - The naming of the actual series.</li>
      <li><code>color</code>- select a color from the color palette.</li>
      </ul>
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
      <p><code>onPress</code></p>
    </td>
    <td selected="false" align="left">
      <p>The ability to add any of the actions (please refer to the list of  Actions). This action(s) will be triggered as a reaction to the press event.</p>
    </td>
  </tr>
</table>

## Examples and code snippets

:::::ExpandableHeading
### Pie chart

::::VerticalSplit{layout="middle"}
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

::::VerticalSplit{layout="middle"}
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
:::
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

