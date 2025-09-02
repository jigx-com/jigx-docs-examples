# grid-item

The grid-item component serves as the child component whenever any grid component has been configured, as discussed in the [grid](grid.md) section. The component determines how the grid items are displayed, allowing you to customize the UI elements in the grid.

## Configuration options

Some properties are common to all components, see [Common component properties](grid-item.md) for a list and their configuration options.

<table><thead><tr><th width="160.73046875">Core structure</th><th></th></tr></thead><tbody><tr><td><code>size</code></td><td>Select the size that the grid-item will be displayed in, the options are <code>1x1</code>,<code>2x2</code>, <code>2x4</code>, <code>4x2</code>, <code>4x4</code>.</td></tr><tr><td><code>children</code></td><td>The following components can be used in the grid-item: <a href="../image.md">image</a> <a href="https://docs.jigx.com/widgets">widgets</a></td></tr></tbody></table>

<table><thead><tr><th width="170.640625">Other options</th><th></th></tr></thead><tbody><tr><td><code>icon</code></td><td>The icon will be displayed on the of the jig. Start typing the name of the icon to invoke the available list in IntelliSense. See <a href="https://docs.jigx.com/jigx-icons">Jigx icons</a> for information on working with icons. The <code>icon</code> property applies to <code>component.jig-widget</code> without a <code>widgetId</code>. See the considerations below for the rules governing icon behavior.</td></tr><tr><td><code>title</code></td><td>By default, the jig's title is displayed. You can override it by adding the <code>title</code> property to the <code>grid-item</code>, either with a custom <code>title</code> or with <code>''</code> (a blank space) to remove the title entirely.</td></tr></tbody></table>

## Considerations

* When using the `grid-item` with a `component.jig-widget`, note the following:
  * A `widgetId` is required if the referenced jig includes a widget configuration. This value should match the `Widget Name` specified in the referenced jig.
  * If no widget configuration exists, the widget’s icon is inherited from the jig’s `icon` value. If no `icon` is specified there either, a default icon is used. You can override the icon by specifying one in the `component.jig-widget` of the `grid-item`.
* For a `1x1` widget, or a `component.widget` with no widgetId, the following rules apply:
  * If no `icon` is specified, a default icon is displayed.
  * If an `icon` is configured in the linked jig, that icon is used.
  * If an `icon` is specified in the `component.widget` in the `grid-item`, it overrides all other icon settings.
* A jig with inputs in it's `title` will display without a title (blank) as the jig would not have received those inputs.

## Examples and code snippets

### Grid-item with image and widget

{% columns %}
{% column %}
Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-swPsNWBEeUaZR5ulp043w-20250203-103644.png" size="66" position="center" caption="Grid-items" alt="Grid-items" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-swPsNWBEeUaZR5ulp043w-20250203-103644.png" width="800" height="1612" darkWidth="800" darkHeight="1612"}
{% endcolumn %}

{% column %}
In this example, three grid-items are configured, each with a different size and type.

1. Grid-item using an image component with a size specified of 4x2.
2. Grid-item using a list widget with a size specified as 2x2. The grid-item automatically shows the list.
3. Grid-item using a chart widget with a size of 2x2.
{% endcolumn %}
{% endcolumns %}

{% tabs %}
{% tab title="grid-item-sales.jigx" %}
```yaml
children:
    # Add a grid to contain multiple grid-items.  
    - type: component.grid
      options: 
        children:
        # First grid-item adds an image to the grid.
        # Specify the grid-item size to apply to the item.
          - type: component.grid-item
            options:
              size: 4x2
              children: 
                type: component.image
                options:
                  source:
                    uri: https://images.unsplash.com/photo-1488509082528-cefbba5ad692?w=800&auto=format&fit=crop&q=60&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8MjB8fGJvb2tpbmd8ZW58MHx8MHx8fDA%3D 
          # Second grid-item adds a list widget to the grid.
          # Specify the grid-item size to apply to the item.
          - type: component.grid-item
            options:
              size: 2x2
              children: 
                type: component.jig-widget
                options:
                  jigId: list-with-stage-dd
          # Third grid-item adds a chart widget to the grid.
          # Specify the grid-item size to apply to the item.        
          - type: component.grid-item
            options:
              size: "2x2"
              children: 
                type: component.jig-widget
                options:
                  jigId: chart-bar1_2x2
                  widgetId: sales
```
{% endtab %}

{% tab title="list-with-stage-dd" %}
```yaml
# Supporting file for the first widget jig in the grid-item.
# Using jig.list ensures the widget automatically displays,
# without configuring a widget property. 
title: Flight Schedule
description: List with Stage
type: jig.list
icon: plane-1

header:
  type: component.jig-header
  options:
    height: medium
    children: 
      type: component.image
      options:
        source:
          uri: https://images.unsplash.com/photo-1490430657723-4d607c1503fc?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxzZWFyY2h8OHx8ZmxpZ2h0c3xlbnwwfHwwfHw%3D&auto=format&fit=crop&w=500&q=60

data: =@ctx.datasources.flight-schedule-dynamic
item:
  type: component.stage
  options:
    icon: plane-1
    right:
      title: =@ctx.current.item.toabrv
      subtitle: =@ctx.current.item.disembark
    left:
      title: =@ctx.current.item.fromabrv
      subtitle: =@ctx.current.item.board
         
```
{% endtab %}

{% tab title="chart-bar1_2x2" %}
```yaml
# Supporting file for the second widget jig in the grid-item.
title: Sales to date
type: jig.default

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

children:
  - type: component.entity
    options:
      children:
        - type: component.entity-field
          options:
            label: Placeholder
            value: Value

widgets:
  sales: 
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
{% endtab %}
{% endtabs %}

### Grid-item options

{% columns %}
{% column %}
This example shows the various configurations available to customize a `grid-item`, making it a versatile widget component. Options include:

* Default `icon`.
* Customized `icons`.
* Overridden or hidden titles using the `title` property.
* `onPress` actions for interactive behavior.

**Examples:** See the full code example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/grid-item/grid-item-auto.jigx).
{% endcolumn %}

{% column %}
Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-eWxJs3no2ja7nEJdJ1LMG-20250605-104403.png" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-eWxJs3no2ja7nEJdJ1LMG-20250605-104403.png" size="66" width="1313" height="2676" position="center" caption}
{% endcolumn %}
{% endcolumns %}

{% tabs %}
{% tab title=" default-icon" %}
```yaml
- type: component.grid
  options:
    children:
      - type: component.grid-item
        options:
          # Widget with 1x1 with default icon.
          size: 1x1
          children:
            type: component.jig-widget
            options:
              jigId: placeholder                                                                           
```
{% endtab %}

{% tab title="custom-icon" %}
```yaml
- type: component.grid
  options:
    children:
      - type: component.grid-item
        options:
          size: "1x1"
          children:
            type: component.jig-widget
            options:
              jigId: placeholder
              # Configure a custom icon to display on the widget
              icon: delivery-truck-2
              # Configuring the title with (' ') removes the title entirely.
              title: ' '
```
{% endtab %}

{% tab title="custom-title" %}
```yaml
- type: component.grid
  options:
    children:
      - type: component.grid-item
        options:
          size: "1x1"
          children:
            type: component.jig-widget
            options:
              jigId: time-log
              # Configure a custom icon to display on the widget.
              icon: time-clock-file-add
              # Configure a custom title to display below the widget. 
              # Configuring the title with (' ') removes the title entirely.
              title: Log
```
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="onPress-event" %}
```yaml
- type: component.grid-item
  options:
    size: "1x1"
    children:
      type: component.jig-widget
      options:
        jigId: placeholder
        # Configure a custom icon to display on the widget.
        icon: air-quality-check-magnifying-glass
        # Configure a custom title to display below the widget.
        title: Checklist
        # Configure an action that will execute when the widget is pressed.
        onPress:
          type: action.info-modal
          options:
            modal:
              title: Inspection checklist
              description: Complete the manual inspection checklist
              element:
                type: icon
                icon: checklist-alternate
                color: warning
              buttonText: Exit
```
{% endtab %}

{% tab title="placeholder.jigx" %}
```yaml
title: Default icon
type: jig.default

placeholders:
  - title: jig placeholder

children:
  - type: component.entity
    options:
      children:
        - type: component.entity-field
          options:
            label: Placeholder
            value: Placeholder
```
{% endtab %}

{% tab title="time-log.jigx" %}
```yaml
title: Time log
type: jig.default
icon: time-monthly-1

header:
  type: component.jig-header
  options:
    height: medium
    children:
      type: component.image
      options:
        source:
          uri: https://images.unsplash.com/37/tEREUy1vSfuSu8LzTop3_IMG_2538.jpg?w=500&auto=format&fit=crop&q=60&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8MTV8fHRpbWUlMjBsb2d8ZW58MHx8MHx8fDA%3D

placeholders:
  - title: No data to display
children:
  - type: component.entity
    options:
      children:
        - type: component.entity-field
          options:
            label: Placeholder
            value: Placeholder
```
{% endtab %}
{% endtabs %}
