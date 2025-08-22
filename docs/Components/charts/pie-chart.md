# pie-chart

{% columns %}
{% column %}
The component can be used to display statistics related to data records. Mostly used in [jig.default](<../../Jig Types/jig_default.md>) or [jig.list](<../../Jig Types/jig_list.md>).
{% endcolumn %}

{% column %}
<figure><img src="../../../.gitbook/assets/CC-pieChart-intro.png" alt="Pie Chart preview"><figcaption><p>Pie Chart preview</p></figcaption></figure>
{% endcolumn %}
{% endcolumns %}

{% hint style="warning" %}
We are currently experiencing issues with the legend of the Pie Chart component. We are working hard to fix this issue.
{% endhint %}

## Configuration options

Some properties are common to all components, see [Common component properties](pie-chart.md) for a list and their configuration options.

<table><thead><tr><th width="162.8046875">Core structure</th><th></th></tr></thead><tbody><tr><td><code>chart</code></td><td><code>title</code>- Its <code>text</code> and <code>verticalAlign</code>.</td></tr><tr><td><code>series</code></td><td><ul><li><code>data</code> - values to be used in the chart.</li><li><code>layout</code> - <code>Pie</code> or <code>Arch</code> - the availabe types of chart.</li></ul></td></tr></tbody></table>

<table><thead><tr><th width="161.16015625">Other options</th><th></th></tr></thead><tbody><tr><td><code>chart</code></td><td><ul><li><code>title</code> and <code>subtitle</code> - Name and a short description of your chart.</li><li><code>height</code> and <code>width</code> - The parameters of the chart displayed (in pixels).</li></ul></td></tr><tr><td><code>legend</code></td><td><code>isHidden</code> - The setting of a boolean value if the legend (naming of the series) should be displayed under the chart.</td></tr><tr><td><code>series</code></td><td><ul><li><code>name</code> - The naming of the actual series.</li><li><code>color</code>- select a color from the color palette.</li></ul></td></tr></tbody></table>

<table><thead><tr><th width="162.4140625">Actions</th><th></th></tr></thead><tbody><tr><td><code>onPress</code></td><td>The ability to add any of the actions (please refer to the list of Actions). This action(s) will be triggered as a reaction to the press event.</td></tr></tbody></table>

## Examples and code snippets

### Pie chart

{% columns %}
{% column %}
<figure><img src="../../../.gitbook/assets/pie-chart.png" alt="Pie chart"><figcaption><p>Pie chart</p></figcaption></figure>
{% endcolumn %}

{% column %}
This jig displays a complete pie chart. In this example, these are issues where green shows resolved issues, yellow issues in progress, and red unresolved issues.

**Examples:**\
See the full code sample using static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/pie-chart/static-data/pie-chart/pie-chart.jigx).\
See the full code sample using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/pie-chart/dynamic-data/pie-chart/pie-chart-dynamic.jigx).

**Datasources:**\
See the full datasource code sample for dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/charts/dynamic/pie-chart-dynamic.jigx).
{% endcolumn %}
{% endcolumns %}

{% tabs %}
{% tab title="pie-chart (static)" %}
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
{% endtab %}

{% tab title="pie-chart (dynamic)" %}
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
{% endtab %}

{% tab title="datasources (dynamic)" %}
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
{% endtab %}
{% endtabs %}

### Pie chart type arch

{% columns %}
{% column %}
<figure><img src="../../../.gitbook/assets/cc-pieChart2.png" alt="Pie chart - arch" width="188"><figcaption><p>Pie chart - arch</p></figcaption></figure>
{% endcolumn %}

{% column %}
This jig displays an arc pie chart. This example shows the occupancy in a warehouse; the green color shows available space and the red color indicates occupied space.

**Examples:** See the full code sample using static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/pie-chart/static-data/pie-chart-arch/pie-chart-arch.jigx). See the full code sample using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/pie-chart/dynamic-data/pie-chart-arch/pie-chart-arch-dynamic.jigx).

**Datasources:** See the full datasource code sample for dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/charts/dynamic/pie-arch-chart-dynamic.jigx).
{% endcolumn %}
{% endcolumns %}

{% tabs %}
{% tab title="arch-chart (static)" %}
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
{% endtab %}

{% tab title="arch-chart (dynamic)" %}
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
{% endtab %}

{% tab title="datasources (dynamic)" %}
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
{% endtab %}
{% endtabs %}
