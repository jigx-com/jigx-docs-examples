# grid

The grid component enables you to create grid layouts in your app, organizing content into rows and columns for a visually consistent and flexible interface. It helps align elements proportionally, ensuring a structured design. The grid is ideal for creating galleries to display photos or product images, dashboards, menus, and product lists. This component is very similar to the [jig.grid](<../../Jig Types/jig_grid.md>) the only exception is that this component can be used in a [jig.default](<../../Jig Types/jig_default.md>) with other components.

## Configuration options

The grid component has two available configuration options:

1. **Auto Grid** - used to create a grid layout from a datasource. This is similar in configuration to a [jig.list](<../../Jig Types/jig_list.md>) where a single `grid-item` is configured and iterates through the datasource.
2. **Custom Grid** - used to create a custom grid layout using widgets, images, or custom components in various sizes.

<table><thead><tr><th width="153.90234375">Core structure</th><th></th></tr></thead><tbody><tr><td><code>type</code></td><td>Within a grid component, the component is used to define each of the elements in the grid layout. Within the <code>grid-item</code> a select set of components can be configured.</td></tr><tr><td><code>data</code></td><td>Configure a datasource to call the data in the grid layout. The data property is required for the Auto Grid, but is optional for the Custom Grid selection.</td></tr></tbody></table>

## Examples and code snippets

### Auto grid

{% columns %}
{% column %}
Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-fJilLcZQaseZ0gjR18gfb-20250107-084107.png" size="60" position="center" caption="Auto grid" alt="Auto grid" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-fJilLcZQaseZ0gjR18gfb-20250107-084107.png" width="800" height="1612" darkWidth="800" darkHeight="1612"}
{% endcolumn %}

{% column %}
In this example, a gallery of images is created to showcase the services a company offers. The `jig.default` type, grid component and datasource is used, enabling a simple configuration based on the records in the datasource. The `component.grid-item` only needs to be configured once using the expression `=@ctx.current.item.` followed by the desired data field. Using `current` loops through the datasource, creating a grid item for each data record. Note that the specified `size` will apply to all returned records.;
{% endcolumn %}
{% endcolumns %}

{% tabs %}
{% tab title="grid-cleaning-service.jigx" %}
```yaml
title: Cleaning services
description: Available services in your area.
type: jig.default
# Define the datasource used to list the images and services.
children:
  - type: component.grid
    options:
      # Select the configured data source where the data will originate. 
      data: =@ctx.datasources.cleaning
      item:
        # One grid-item component generates the entire grid using current data. 
        type: component.grid-item
        options:
           # Select the size that all the items will display as, 
           # all items use the same size.        
           size: "2x2"
           children: 
             # Choose the component to show in the grid.            
              type: component.image
              options:
                # Use the expression =@ctx.current.item.x with the data field
                # name. Use current loops through the datasource creating
                # grid-items for each data record.             
                title: =@ctx.current.item.service
                source:
                  uri: =@ctx.current.item.image
```
{% endtab %}

{% tab title="datasource (Dynamic Data)" %}
```yaml
datasources:
  cleaning: 
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_DYNAMIC
      entities:
        - entity: default/cleaning-services

      query: |
        SELECT 
          id, 
          '$.id' as sqlid, 
          '$.area', 
          '$.description', 
          '$.hourlyrate', 
          '$.image', 
          '$.service'  
        FROM [default/cleaning-services]
        WHERE '$.hourlyrate' IS NOT NULL ORDER BY id DESC
```
{% endtab %}
{% endtabs %}

### Custom grid

{% columns %}
{% column %}
This example demonstrates combining the grid component with other components (entity and form) in a default jig. The grid is customized to show an image component (4x2), a list widget (2x2) and chart widget (2x2).
{% endcolumn %}

{% column %}
Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-U\_hOcdAx5wOjx7J-NL2gi-20250203-100429.png" size="66" position="center" caption="Custom grid " alt="Custom grid " signedSrc="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-U\_hOcdAx5wOjx7J-NL2gi-20250203-100429.png" width="800" height="1612" darkWidth="800" darkHeight="1612"}
{% endcolumn %}
{% endcolumns %}

{% tabs %}
{% tab title="grid-custom-component" %}
```yaml
title: Global Sales 
type: jig.default

children:
    - type: component.entity
      options:
        isCompact: true
        children:
         -  type: component.entity-field
            options:
              label: Region Sales Schedule
              value: My Schedule
    - type: component.divider 
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
                    uri: https://images.unsplash.com/photo-1516738901171-8eb4fc13bd20?w=800&auto=format&fit=crop&q=60&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8MTJ8fGJvb2tpbmd8ZW58MHx8MHx8fDA%3D 
         # Second grid-item adds a list widget to the grid.
          # Specify the grid-item size to apply to the item.
          - type: component.grid-item
            options:
              size: 2x2
              children: 
                type: component.jig-widget
                options:
                  jigId: list-with-stage-dd
                  widgetId: "2x2"
          # Third grid-item adds a chart widget to the grid.
          # Specify the grid-item size to apply to the item.        
          - type: component.grid-item
            options:
              size: "2x2"
              children: 
                type: component.jig-widget
                options:
                  jigId: chart-bar1_2x2
                  widgetId: "2x2"
    # The grid and grid-item components can be combined with other components.
    - type: component.form
      instanceId: flightCheck-in
      options:
        isDiscardChangesAlertEnabled: false
        children:
          - type: component.field-row
            options:
              children:
                - type: component.text-field
                  instanceId: fullname
                  options:
                    label: Name
                - type: component.text-field
                  instanceId: mobile-phone
                  options:
                    label: Contact
                    icon: phone
          - type: component.text-field
            instanceId: flightNumber
            options:
              label: Flight number        
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
