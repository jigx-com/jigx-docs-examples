---
title: jig.grid
slug: 8LCm-jig
createdAt: Tue Dec 03 2024 11:39:30 GMT+0000 (Coordinated Universal Time)
updatedAt: Thu May 01 2025 10:33:53 GMT+0000 (Coordinated Universal Time)
---

The `jig.grid` enables you to create grid layouts in your app, organizing content into rows and columns for a visually consistent and flexible interface. It helps align elements proportionally, ensuring a structured design. The grid is ideal for creating galleries to display photos or product images, as well as dashboards, menus, and product lists.

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-w5fDciaaOqvoKxuVxeQJQ-20250430-101252.png" size="52" position="center" caption="Custom Grid " alt="Custom Grid "}
:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-AA7qAcJ34IJsD36GlpeAm-20241205-080912.png" size="52" position="center" caption="Auto Grid " alt="Auto Grid "}
:::
::::

## Configuration options

The `jig.grid` has two available configuration options:

1. **Auto Grid** - used to create a grid layout from a datasource. This is similar in configuration to a [jig.list](./jig_list.md) where a single `grid-item` is configured and iterates through the datasource.
2. **Custom Grid** - used to create a custom grid layout using widgets, images, or custom components in various sizes.
Some properties are common to all jig types, see [Common jig type properties](docId\:AvbKAkPpRDHkZ8I8iSTkF) for a list and their configuration options.

| ### Core structure | ****                                                                                                                                                                                                                   |
| ------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `title`            | Give the jig a title that is displayed at the top of the screen. If you do not want to show a title in a jig use `title: ' '`.                                                                                         |
| `type`             | Select `jig.grid` for a grid layout configuration.                                                                                                                                                                     |
| `component`        | Within a grid jig type, the [grid-item](./../Components/grid/grid-item.md) component is used to define each of the elements in the grid layout. Within the `grid-item` a select set of components can be configured.   |
| `datasources`      | Configure a datasource to call the data to display in the grid layout. The datasource property is required for the Auto Grid, but is optional for the Custom Grid selection.                                           |

| ### Other options      | ****                                          |
| ---------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `actions`              | Choose from the provided list of available actions, for example, use the `go-to` action to open a different jig.                                  |
| `badge`                | Enhance your tabs with a badge, for instance show the number of grid-items. Add the `badge` property to the jig YAML with an expression.           |
| `description`          | Give the jig a description that is displayed under the `title`.                                                                                    |
| `data`                 | Reference a global datasource to use in the jig .                                                                                                  |
| `grid-item`            | `size` - Select either `1x1`,` 2x2`, `2x4`, `4x2`, `4x4`&#xA;`children` - Select a component from the predefined list to display in the grid. The components for selection are:&#xA;- [Custom components (Alpha)](<./../Custom components _Alpha_.md>) &#xA;- [image](./../Components/image.md)&#xA;- [widgets]()  &#xA;- Use Template - image templates |
| `expressions`          | Use the `expressions` property to set [expressions](./../Expressions.md) that are reusable throughout the jig.                                    |
| `header`               | Configure a [jig-header](./../Components/jig-header.md) that displays and image, location or video at the top of the jig.                          |
| `icon`                 | The icon will be displayed on the [widget]() of this jig. Start typing the name of the icon to invoke the available list in IntelliSene. See [Jigx icons]() for information on working with icons.                                                    |
| `inputs`               | Configure [inputs]()  that allow you to receive data from other jigs and use it in the current jig.                                                |
| `isCollapsible`        | When the jig is used in a [jig.composite](./jig_composite.md) and this property is set to `true`, a collapse and expand icon is shown, allowing the jig to be collapsed. This is helpful if the composite jig has a number of jigs configured, making it easier to view and interact with the app.                                                       |
| `isInitiallyCollapsed` | When the property is set to `true` and the jig is part of a composite jig, the jig will open in collapsed mode when the composite jig is launched.      |
| `isWaitingSync`        | Displays a waiting sync indicator.             |
| `jigId`                | Give the jig a unique id that can be referenced outside the jig, for example in state expressions.                                                |
| `outputs`              | Configure [outputs]() that allow you to transfer data out of the current jig and use it in another jig.                                           |
| `placeholders`         | Create a placeholder to show when there is no data to use yet. See <a href="https://community.jigx.com/t/tips-tricks-use-placeholders/78" target="_blank">tips and tricks -use a placeholder</a> for a placeholder example.                         |
| `preview`              | Configure the [Preview](./../Preview.md) which is triggered by *long-pressing* on the grid-item.                                                   |
| `summary`              | Add a [summary](./../Components/summary.md) component that displays at the bottom of the jig.                                                     |

| ### Events  | ****                                                                                         |
| ----------- | -------------------------------------------------------------------------------------------- |
| `onFocus`   | Configure an action that executes when the jig opens, for example, `reset-solution-state`.   |
| `onRefresh` | Configure an action that executes when the jig is pulled down, for example, `sync-entities`. |

## Considerations

- When using the `grid-item` with a `component.jig-widget`, note of the following:
  - A `widgetId` is required if the referenced jig includes a widget configuration. This value should match the `Widget Name` specified in the referenced jig.
  - If no widget configuration exists, the widget's icon is derived from the jig's `icon` value. If none is specified, a default icon is assigned.

## Examples and code snippets 

:::::ExpandableHeading
### Custom grid jig

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-w5fDciaaOqvoKxuVxeQJQ-20250430-101252.png" size="60" position="center" caption="Custom Grid - Delivery " alt="Custom Grid - Delivery "}
:::

:::VerticalSplitItem
In this example, a delivery company uses a dashboard for drivers to display their daily deliveries, urgent tasks, inspection checklists, logs, and customer ratings or complaints. The `jig.grid` with the `custom grid` option is used, allowing multiple `grid-item` configurations. These items include widgets, images, and custom components in various sizes.

**Examples:**
See the full code sample in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jig-types/jig-grid/grid-custom.jigx).
Supporting jig samples in [GitHub](https://github.com/jigx-com/jigx-samples/tree/main/quickstart/jigx-samples/jigs/jig-types/jig-grid).
:::
::::

:::CodeblockTabs
grid-custom.jigx

```yaml
# Use the custom grid jig type to create a jig with images, icons, widgets, 
# and custom component.
type: jig.grid
title: ="Morning " & @ctx.user.displayName

children:
  # Configure multiple grid-items one for each element to display on the grid.
  # Elements are displayed in the order of grid-items starting from the top down.
  - type: component.grid-item
    options:
      # Specify the grid-item size.
      size: "2x2"
      children:
       # Add an image component with an onPress event to go to a jig.       
        type: component.image
        options:
          title: Today's deliveries
          source:
            uri: https://cdn.pixabay.com/photo/2021/04/05/16/28/packages-6153947_1280.jpg
          onPress: 
            type: action.go-to
            options:
              linkTo: delivery-list
  # Second Grid-item        
  - type: component.grid-item
    options:
      size: "2x2"
      children: 
        # Add an image component with an onPress event to go to a jig.          
        type: component.image
        options:
          title: Inspection checklist
          onPress: 
            type: action.go-to
            options:
              behaviour: existing
              linkTo: inspection   
          source:
            uri: https://cdn.pixabay.com/photo/2014/11/20/19/16/insurance-539659_640.jpg
  # Third Grid-item        
  - type: component.grid-item
    options:
      size: "1x1"
      children: 
        # Add a jig-widget component and link to the jig using the jigId.         
        type: component.jig-widget
        options:
          jigId: time-log
  # Fourth Grid-item
  - type: component.grid-item
    options:
      size: "1x1"
      children: 
        type: component.jig-widget
        options:
          jigId: fuel-log
  # Fifth Grid-item
  - type: component.grid-item
    options:
      size: "1x1"
      children: 
        type: component.jig-widget
        options:
          jigId: customer-complaints              
  # Sixth Grid-item
  - type: component.grid-item
    options:
      size: "1x1"
      children: 
        type: component.jig-widget
        options:
          jigId: customer-rating    
  # Seventh Grid-item          
  - type: component.grid-item
    options:
      size: "4x4"
      children: 
        # Add a custom component to display a card with a location and button.           
        type: component.custom-component
        componentId: grid-location
```

grid-location.jigx

```yaml
type: component.default
children:
  - type: component.card
    options:
      children:
        - type: component.entity
          options:
            children:
                  - type: component.field-row
                    options:
                      children:
                        - type: component.entity-field
                          options:
                            rightIcon: shield-warning 
                            style:
                              isNegative: true
                            label: URGENT DELIVERY 
                            value: 345 Harrison Ave, Boston, MA 02118
        - type: component.location
          options:
            camera:
              centerPosition: middle
              address: 345 Harrison Ave, Boston, MA 02118
              zoomLevel: 11
       
  - type: component.view
    options:
      style:
        flex:
          direction: row
        bottom: medium
        top: medium
        alignSelf: flex-end
      children:
        - type: component.button
          options:
            title: Navigate
            type: primary
            isCompact: true
            onPress: 
              type: action.open-url
              options:
                url: https://www.google.com/maps/place/Boston
```

inspection.jigx

```yaml
title: Vehicle Inspection Checklist
type: jig.default

header:
  type: component.jig-header
  options:
    height: medium
    children:
      type: component.image
      options:
        source:
          uri: https://images.unsplash.com/photo-1498887960847-2a5e46312788?w=500&auto=format&fit=crop&q=60&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8Nnx8Y2FyJTIwY2hlY2tsaXN0fGVufDB8fDB8fHww

children:
  - type: component.form
    instanceId: checklist
    options:
      isDiscardChangesAlertEnabled: false
      children: 
        - type: component.checkbox
          instanceId: insp-tyres
          options:
            icon: car-dashboard-window-rear-wipe
            label: Tyres
            helperText: Check tyres pressure and for puntures
        - type: component.checkbox
          instanceId: insp-lights
          options:
            icon: car-dashboard-lights
            label: Lights
            helperText: Check front lights, indicator & rear lights     
        - type: component.checkbox
          instanceId: insp-windscreen
          options:
            icon: car-dashboard-window-rear
            label: Windscreen
            helperText: Check windscreen for chips and cracks
        - type: component.checkbox
          instanceId: insp-wipers
          options:
            icon: car-dashboard-window-rear-wipe
            label: Windscreen wipers
            helperText: Switch on wipers, and check wash liquid.     
        - type: component.checkbox
          instanceId: insp-locks
          options:
            icon: car-key-1
            label: Vehicle locks
            helperText: Check all door locks to maintain security standards
```

customer-complaints.jigx

```yaml
title: Complaints
type: jig.default
icon: people-conflict-1

header:
  type: component.jig-header
  options:
    height: medium
    children:
      type: component.image
      options:
        source:
          uri: https://images.unsplash.com/photo-1503525537183-c84679c9147f?w=500&auto=format&fit=crop&q=60&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8M3x8YW5ncnklMjBjdXN0b21lcnxlbnwwfHwwfHx8MA%3D%3D

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

customer-rating.jigx

```yaml
title: Rating  
description: Customer Survey
type: jig.default

header:
  type: component.jig-header
  options:
    height: medium
    children:
      type: component.image
      options:
        source:
          uri: https://images.unsplash.com/photo-1628313388777-9b9a751dfc6a?q=80&w=1548&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D

datasources:
  customer-satisfaction: 
    type: datasource.static
    options:
      data:
        - id: 1
          option: 😀 Happy
        - id: 2
          option: 😕 Neutral  
        - id: 3
          option: 😡 Sad 

children:
  - type: component.form
    instanceId: customer-survey
    options:
      isDiscardChangesAlertEnabled: false
      children:
        - type: component.choice-field
          instanceId: satisfaction
          options:
            itemsPerRow: 3
            label: How satisfied were you with our service today?
            data: =@ctx.datasources.customer-satisfaction
            item:
              type: component.choice-field-item
              options:
                title: =@ctx.current.item.option
                value: =@ctx.current.item.option
actions:
  - children:
      - type: action.execute-entity
        options:
          title: submit
          provider: DATA_PROVIDER_DYNAMIC
          entity: default/customer
          method: create
          onSuccess: 
            type: action.info-modal
            options:
              modal:
                element: 
                  type: image
                  uri: https://images.unsplash.com/photo-1643878037082-ba1fd9a60b16?q=80&w=1632&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D
                title: Survey complete
                buttonText: Thank you
          data:
            satisfaction: =@ctx.components.satisfaction.state.value
```

fuel-log.jigx

```yaml
title: Fuel log
description: Description of your Jig
type: jig.default
icon: fuel-pump-reload

header:
  type: component.jig-header
  options:
    height: medium
    children:
      type: component.image
      options:
        source:
          uri: https://images.unsplash.com/photo-1602853175733-5ad62dc6a2c8?w=500&auto=format&fit=crop&q=60&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8M3x8ZnVlbHxlbnwwfHwwfHx8MA%3D%3D

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

time-log.jigx

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
:::
:::::

:::::ExpandableHeading
### Auto grid jig

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-AA7qAcJ34IJsD36GlpeAm-20241205-080912.png" size="60"  position="center" caption="Auto Grid -Image Gallery  " alt="Auto Grid -Image Gallery  "}
:::

:::VerticalSplitItem
In this example, a gallery of images is created to showcase the services a company offers. The `jig.grid` type is used with a datasource, enabling a simple configuration based on the records in the datasource. The `component.grid-item` only needs to be configured once using the expression `=@ctx.current.item.` followed by the desired data field. Using `current` loops through the datasource, creating a grid-item for each data record. Note that the specified `size` will apply to all returned records.

**Examples:**
See the full code sample in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jig-types/jig-grid/grid-auto.jigx).

:::
::::

:::CodeblockTabs
cleaning-services.jigx

```yaml
title: Cleaning services
description: Available services in your area.
# Use the grid jig type to create a gallery of images and titles.
type: jig.grid
# Define the datasource used to list the images and services.          
data: =@ctx.datasources.cleaning
item:
 # One grid-item component generates the entire grid using current data.
  type: component.grid-item
  options:
    # Select the size that all the items will display as, all items use the same size.
    size: "2x2"
    children: 
      # Choose the component to show in the grid.    
      type: component.image
      options:
        # Use the expression =@ctx.current.item.x with the data field name.
        # Use current loops through the datasource creating grid-items for each data record. 
        title: =@ctx.current.item.service
        source:  
          uri: =@ctx.current.item.image
```

cleaning (datasource)&#x20;

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
:::
:::::

