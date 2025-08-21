# group

The `group widget` allows widgets to be combined to create a single widget. The `group widget` can be used only on `sizes:` 2x4, 4x2, and 4x4.

## Configuration options

<table><thead><tr><th width="144.4296875">Core structure</th><th></th></tr></thead><tbody><tr><td><code>children</code></td><td>The <code>children</code> property includes all available widgets- combining two widgets is typical for group widgets.</td></tr></tbody></table>

<table data-header-hidden><thead><tr><th width="142.62890625">Other options</th><th></th></tr></thead><tbody><tr><td><code>footer</code></td><td>Add text to the footer of the widget</td></tr><tr><td><code>footerAlign</code></td><td>Align the footer text to <code>left</code>, <code>right</code>, <code>center</code>.</td></tr><tr><td><code>placeholders</code></td><td>Specify a placeholder text to display if there is no data, for example - <code>title: No data to display</code></td></tr><tr><td><code>split</code></td><td>The option to group the widgets vertically or horizontally. By default, widgets are grouped vertically.</td></tr></tbody></table>

## Examples and code snippets

## Group with chart and list (size: 4x4, split: horizontal)

{% columns %}
{% column %}
Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/vZSpwck06Npdts3BCYNB1\_group-wiphone13blueportrait.png" size="82" position="center" caption="Horizontal split widget group " alt="Horizontal split widget group " signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/vZSpwck06Npdts3BCYNB1\_group-wiphone13blueportrait.png" width="800" height="1493" darkWidth="800" darkHeight="1493"}&#x20;
{% endcolumn %}

{% column %}
For the 4x4 widget, we have a split option. In this property, a vertical or horizontal layout is possible for the widget. In this example, a combination of a chart and a list are used in a **horizontal** split.

**Examples**: See the full example using static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/widgets/group/static-data/group-chart-list-horizontal.jigx).
{% endcolumn %}
{% endcolumns %}

{% tabs %}
{% tab title=" group-ChartList (static)" %}
```yaml
widgets:
  list-horizontal-4x4: 
    type: widget.group
    options:
      split: horizontal
      children:
        - type: widget.chart
          options:
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
                  tickAmount: 8
                  isFirstTickHidden: true
                  isFirstLabelHidden: true
                xAxis:
                  categories:
                    - Q1
                    - Q2
                    - Q3
                    - Q4
                series:
                  - data: =[{"x":"Q1/20", "y":25000, "color":"color2"}, {"x":"Q2/20", "y":32000, "color":"color2"}, {"x":"Q3/20", "y":45000, "color":"color2"}, {"x":"Q4/20", "y":86000, "color":"color2"}]
                    name: Year 2019
                    animation:
                        direction: left-to-right
                    layout: area-gradient
                    dataLabels:
                      - isEnabled: true
                  - data: =[{"x":"Q1/20", "y":12000, "color":"color3"}, {"x":"Q2/20", "y":48000, "color":"color3"}, {"x":"Q3/20", "y":36000, "color":"color3"}, {"x":"Q4/20", "y":120000, "color":"color3"}]
                    name: Year 2020
                    animation:
                        direction: left-to-right
                    layout: area-gradient
                    dataLabels:
                      - isEnabled: true      
                legend:
                  isHidden: false
        - type: widget.list
          options:
            data: =@ctx.datasources.transactions
            item: 
              type: component.list-item
              options:
                divider: solid
                title: =@ctx.current.item.company
                subtitle: =@ctx.current.item.description
                description: =$fromMillis($toMillis(@ctx.current.item.date), '[M01]/[D01]/[Y01]')
                label:
                  title: =@ctx.current.item.amount & '$'
                  isHidden: false
                  color:
                    - when: =(@ctx.current.item.positive = true)
                      color: color2
                    - when: =(@ctx.current.item.positive = false)
                      color: color4
                leftElement: 
                  element: icon
                  icon: =@ctx.current.item.positive = true ? 'up' :'down'
                style:
                  isPositive: =@ctx.current.item.positive
                  isError: =@ctx.current.item.positive = false ? "true" :"false"
```
{% endtab %}

{% tab title="grid-item" %}
```yaml
children:
  - type: component.grid-item
    options:
      size: "4x4"
      children: 
        type: component.jig-widget
        options:
          jigId: group-chart-list-horizontal
          widgetId: list-horizontal-4x4
```
{% endtab %}
{% endtabs %}

## Group with chart and list (size: 4x4, split: vertical)

{% columns %}
{% column %}
Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/vblqyuZ8bZ3CsaQOHpbU3\_verticalgroupiphone13blueportrait.png" size="80" position="center" caption="Vertical split widget group " alt="Vertical split widget group " signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/vblqyuZ8bZ3CsaQOHpbU3\_verticalgroupiphone13blueportrait.png" width="800" height="1493" darkWidth="800" darkHeight="1493"}
{% endcolumn %}

{% column %}
In this example, a combination of a chart and list was configured with a **vertical** split.

**Examples**: See the full example using static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/widgets/group/static-data/group-chart-list-vertical.jigx).
{% endcolumn %}
{% endcolumns %}



{% tabs %}
{% tab title="group-ChartListVertical (static)" %}
```yaml
widgets:
  listVertical-4x4: 
    type: widget.group
    options:
      split: vertical
      children:
        - type: widget.chart
          options:
            chart: 
              type: component.line-chart
              options:
                xAxis:
                  isHidden: true
                yAxis:
                  max: 6
                  min: 3
                series:
                  - data: =@ctx.datasources.chart
                    color: color1
                    layout: area-gradient
            top: 
              type: component.titles
              options:
                title: Solana
                subtitle: USDT
                align: left
                icon: currency-dollar
                iconColor: color2
            bottom: 
              type: component.trend
              options:
                title: 92,40 USDT / SOL          
                style:
                  isAlignRight: false
                  isValueBottom: true
                value: +21.2
                format:
                  numberStyle: unit
                  unit: percent
        - type: widget.list
          options:
            data: =@ctx.datasources.list
            item: 
              type: component.list-item
              options:
                title: =@ctx.current.item.title
                subtitle: =@ctx.current.item.subtitle
                label:
                  title: =@ctx.current.item.change > 0 ? '+' & @ctx.current.item.change :@ctx.current.item.change
                  color:
                    - when: =@ctx.current.item.change > 0
                      color: color2
                    - when: =@ctx.current.item.change < 0
                      color: color4
```
{% endtab %}

{% tab title="grid-item" %}
```yaml
children:
  - type: component.grid-item
    options:
      size: "4x4"
      children: 
        type: component.jig-widget
        options:
          jigId: group-chart-list-vertical
          widgetId: listVertical-4x4
```
{% endtab %}
{% endtabs %}

## Group with avatar and list (size: 4x2)

{% columns %}
{% column %}
Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/Ku31Kug--owZX3VQ\_NC2G\_4x2iphone13blueportrait.png" size="80" position="center" caption="Group widget with avatar and list" alt="Group widget with avatar and list" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/Ku31Kug--owZX3VQ\_NC2G\_4x2iphone13blueportrait.png" width="800" height="1493" darkWidth="800" darkHeight="1493"}
{% endcolumn %}

{% column %}
&#x20;This group widget represents a combination of the avatar with a list. After clicking on the widget, the list component is shown.

**Examples**: See the full example using static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/widgets/group/static-data/group-avatar-list.jigx). See the full example using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/widgets/group/dynamic-data/group-avatar-list-dynamic.jigx).

**Datasources**: See the full datasource for static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/employees/employees-static.jigx). See the full datasource for dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/employees/employees-dynamic.jigx).
{% endcolumn %}
{% endcolumns %}

{% tabs %}
{% tab title="group-avatar-list (static)" %}
```yaml
widgets:
  groupAvatar-4x2: 
    type: widget.group
    options:
      children:
        - type: widget.avatar
          options:
            text: ''
            uri: https://images.unsplash.com/photo-1591084728795-1149f32d9866?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=928&q=80
        - type: widget.list
          options:
            data: =@ctx.datasources.group-list
            item:
              type: component.list-item
              options:
                title: =@ctx.current.item.name
                leftElement: 
                  element: avatar
                  text: '' 
                  uri: =@ctx.current.item.img
```
{% endtab %}

{% tab title="group-avatar-list (Dynamic)" %}
```yaml
widgets:
  groupAvatarDD-4x2: 
    type: widget.group
    options:
      children:
        - type: widget.avatar
          options:
            text: ''
            uri: =@ctx.datasources.avatar-dynamic.photo
        - type: widget.list
          options:
            data: =@ctx.datasources.employees-dynamic
            item:
              type: component.list-item
              options:
                title: =@ctx.current.item.firstname
                subtitle: =@ctx.current.item.lastname
                leftElement: 
                  element: avatar
                  text: '' 
                  uri: =@ctx.current.item.photo
```
{% endtab %}

{% tab title="grid-item" %}
```yaml
# grid-item for the static jigx
children:
  - type: component.grid-item
    options:
      size: "4x2"
      children: 
        type: component.jig-widget
        options:
          jigId: group-avatar-list
          widgetId: groupAvatar-4x2
```
{% endtab %}
{% endtabs %}

## Group with value and bar-chart (size: 2x4)

{% columns %}
{% column %}
Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/\_nW2If-8vWWmlEVdp0SmL\_2x4iphone13blueportrait.png" size="80" position="center" caption="Group with value and bar-chart" alt="Group with value and bar-chart" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/\_nW2If-8vWWmlEVdp0SmL\_2x4iphone13blueportrait.png" width="800" height="1493" darkWidth="800" darkHeight="1493"}
{% endcolumn %}

{% column %}
This group widget represents a combination of the value and bar-chart. After clicking on the widget, the bar- chart is shown.

**Examples**: See the full example using static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/widgets/group/static-data/group-value-chart.jigx). See the full example using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/widgets/group/dynamic-data/group-value-chart-dynamic.jigx).

**Datasources**: See the full datasource for static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/charts/static/series1.jigx). See the full datasource for dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/charts/dynamic/series1-dynamic.jigx).
{% endcolumn %}
{% endcolumns %}

{% tabs %}
{% tab title="group-value-bar-chart (static)" %}
```yaml
widgets:
  groupValue-2x4: 
    type: widget.group
    options:
      children:
        - type: widget.value
          options:
            value: 7500
            top: 
              type: component.titles
              options:
                title: Daily revenue
        - type: widget.chart
          options:
            chart: 
              type: component.bar-chart
              options:
                series:
                  - data: =@ctx.datasources.series1
```
{% endtab %}

{% tab title="group-value-chart (dynamic)" %}
```yaml
widgets:
  groupValueDD-2x4: 
    type: widget.group
    options:
      children:
        - type: widget.value
          options:
            value: =@ctx.datasources.value-dynamic.value
            top: 
              type: component.titles
              options:
                title: Daily revenue
        - type: widget.chart
          options:
            chart: 
              type: component.bar-chart
              options:
                series:
                  - data: =@ctx.datasources.series1-dynamic
```
{% endtab %}

{% tab title="grid-item" %}
```yaml
# grid-item for the static jigx
children:
  - type: component.grid-item
    options:
      size: "2x4"
      children: 
        type: component.jig-widget
        options:
          jigId: group-value-chart
          widgetId: groupValue-2x4
```
{% endtab %}
{% endtabs %}
