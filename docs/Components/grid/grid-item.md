---
title: grid-item
slug: gHh8-g
createdAt: Tue Dec 03 2024 11:44:39 GMT+0000 (Coordinated Universal Time)
updatedAt: Fri Mar 21 2025 09:20:33 GMT+0000 (Coordinated Universal Time)
---

The grid-item component serves as the child component whenever any grid component has been configured, as discussed in the [grid](./../grid.md)  section. The component determines how the grid items are displayed, allowing you to customize the UI elements in the grid.&#x20;

## Configuration options

Some properties are common to all components, see [Common component properties](docId\:LLnTD-rxe8FmH7WpC5cZb) for a list and their configuration options.

| ### Core structure | ****                                                                                                                                                                                       |
| ------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `size`             | Select the size that the grid-item will be displayed in, the options are `1x1`,`2x2`, `2x4`, `4x2`, `4x4`.                                                                                 |
| `children`         | The following components can be used in the grid-item:<br />* [Custom components (Alpha)](<./../../Custom components _Alpha_.md>)&#x20;
* [image](./../image.md)&#x20;
* [widgets]()&#x20; |

## Considerations

- When using the `grid-item` with a `component.jig-widget`, note of the following:
  - A `widgetId` is required if the referenced jig includes a widget configuration. This value should match the `Widget Name` specified in the referenced jig.&#x20;
  - If no widget configuration exists, the widget's icon is derived from the jig's `icon` value. If none is specified, a default icon is assigned.

## Examples and code snippets 

:::::ExpandableHeading
### Grid-item with image and widget&#x20;

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-swPsNWBEeUaZR5ulp043w-20250203-103644.png" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-swPsNWBEeUaZR5ulp043w-20250203-103644.png" size="66" width="1224" height="2466" position="center" caption="Grid-items" alt="Grid-items"}
:::

:::VerticalSplitItem
In this example, three grid items are configured, each with a different size and type.&#x20;

1. Grid-item using an image component with a size specified of 4x2. &#x20;
2. Grid-item using a list component with a size specified as 2x2. The grid-item automatically shows the list.
3. Grid-item using a chart widget with a size of 2x2.&#x20;
:::
::::

:::CodeblockTabs
grid-item-sales.jigx

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

list-with-stage-dd

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

chart-bar1\_2x2

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
:::
:::::







