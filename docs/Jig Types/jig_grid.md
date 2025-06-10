# jig.grid

The `jig.grid` enables you to create grid layouts in your app, organizing content into rows and columns for a visually consistent and flexible interface. It helps align elements proportionally, ensuring a structured design. The grid is ideal for creating galleries to display photos or product images, as well as dashboards, menus, and product lists.

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-4E4I4-UEZCwohqjOv3ATj-20250514-065552.png" size="52" position="center" caption="Custom Grid " alt="Custom Grid " signedSrc="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-4E4I4-UEZCwohqjOv3ATj-20250514-065552.png"}
:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-AA7qAcJ34IJsD36GlpeAm-20241205-080912.png" size="52" position="center" caption="Auto Grid " alt="Auto Grid " signedSrc="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-AA7qAcJ34IJsD36GlpeAm-20241205-080912.png"}
:::
::::

## Configuration options

The `jig.grid` has two available configuration options:

1. **Auto Grid** - used to create a grid layout from a datasource. This is similar in configuration to a [jig.list](./jig_list.md) where a single `grid-item` is configured and iterates through the datasource.
2. **Custom Grid** - used to create a custom grid layout using widgets, images, or custom components in various sizes.
   Some properties are common to all jig types, see [Common jig type properties](docId\:AvbKAkPpRDHkZ8I8iSTkF) for a list and their configuration options.

| **Core structure** |                                                                                                                                                                                                                      |
| ------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `title`            | Give the jig a title that is displayed at the top of the screen. If you do not want to show a title in a jig use `title: ' '`.                                                                                       |
| `type`             | Select `jig.grid` for a grid layout configuration.                                                                                                                                                                   |
| `component`        | Within a grid jig type, the [grid-item](./../Components/grid/grid-item.md) component is used to define each of the elements in the grid layout. Within the `grid-item` a select set of components can be configured. |
| `datasources`      | Configure a datasource to call the data to display in the grid layout. The datasource property is required for the Auto Grid, but is optional for the Custom Grid selection.                                         |

| **Other options**      |                                                                                                                                                                                                                                                                                                                                                           |
| ---------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `actions`              | Choose from the provided list of available actions, for example, use the `go-to` action to open a different jig.                                                                                                                                                                                                                                          |
| `badge`                | Enhance your tabs with a badge, for instance show the number of grid-items. Add the `badge` property to the jig YAML with an expression.                                                                                                                                                                                                                  |
| `description`          | Give the jig a description that is displayed under the `title`.                                                                                                                                                                                                                                                                                           |
| `data`                 | Reference a global datasource to use in the jig .                                                                                                                                                                                                                                                                                                         |
| `grid-item`            | `size` - Select either `1x1`,` 2x2`, `2x4`, `4x2`, `4x4`&#xA;`children` - Select a component from the predefined list to display in the grid. The components for selection are:&#xA;- [Custom components (Alpha)](<./../Custom components _Alpha_.md>) &#xA;- [image](./../Components/image.md)&#xA;- [widgets](#)  &#xA;- Use Template - image templates |
| `expressions`          | Use the `expressions` property to set [expressions](./../Expressions.md) that are reusable throughout the jig.                                                                                                                                                                                                                                            |
| `header`               | Configure a [jig-header](./../Components/jig-header.md) that displays and image, location or video at the top of the jig.                                                                                                                                                                                                                                 |
| `icon`                 | The icon will be displayed on the [widget](#) of the jig. Start typing the name of the icon to invoke the available list in IntelliSense. See [Jigx icons](#) for information on working with icons. The `icon` property applies to `component.jig-widget` without a `widgetId`. See the considerations below for the rules governing icon behavior.      |
| `inputs`               | Configure [inputs](#)  that allow you to receive data from other jigs and use it in the current jig.                                                                                                                                                                                                                                                      |
| `isCollapsible`        | When the jig is used in a [jig.composite](./jig_composite.md) and this property is set to `true`, a collapse and expand icon is shown, allowing the jig to be collapsed. This is helpful if the composite jig has a number of jigs configured, making it easier to view and interact with the app.                                                        |
| `isInitiallyCollapsed` | When the property is set to `true` and the jig is part of a composite jig, the jig will open in collapsed mode when the composite jig is launched.                                                                                                                                                                                                        |
| `isWaitingSync`        | Displays a waiting sync indicator.                                                                                                                                                                                                                                                                                                                        |
| `jigId`                | Give the jig a unique id that can be referenced outside the jig, for example in state expressions.                                                                                                                                                                                                                                                        |
| `outputs`              | Configure [outputs](#) that allow you to transfer data out of the current jig and use it in another jig.                                                                                                                                                                                                                                                  |
| `placeholders`         | Create a placeholder to show when there is no data to use yet. See <a href="https://community.jigx.com/t/tips-tricks-use-placeholders/78" target="_blank">tips and tricks -use a placeholder</a> for a placeholder example.                                                                                                                               |
| `preview`              | Configure the [Preview](./../Preview.md) which is triggered by *long-pressing* on the grid-item.                                                                                                                                                                                                                                                          |
| `summary`              | Add a [summary](./../Components/summary.md) component that displays at the bottom of the jig.                                                                                                                                                                                                                                                             |
| `title`                | By default, the jig's `title` is displayed on the widget. You can override it by adding the `title` property to the `component.jig-widget` in the `grid-item`, either with a custom `title` or with `''` (a blank space) to remove the title entirely.                                                                                                    |

| **Events**  |                                                                                              |
| ----------- | -------------------------------------------------------------------------------------------- |
| `onFocus`   | Configure an action that executes when the jig opens, for example, `reset-solution-state`.   |
| `onRefresh` | Configure an action that executes when the jig is pulled down, for example, `sync-entities`. |
| `onPress`   | Add an `onPress` event to add an action directly on the grid-item, such as `open-url`.       |

## Considerations

- When using the `grid-item` with a `component.jig-widget`, note the following:
  - A `widgetId` is required if the referenced jig includes a widget configuration. This value should match the `Widget Name` specified in the referenced jig.
  - If no widget configuration exists, the widget’s icon is inherited from the jig’s `icon` value. If no `icon` is specified there either, a default icon is used. You can override the icon by specifying one in the `component.jig-widget` of the `grid-item`.
- For a `1x1` widget, or a `component.widget` with no widgetId, the following rules apply:
  - If no `icon` is specified, a default icon is displayed.
  - If an `icon` is configured in the linked jig, that icon is used.
  - If an `icon` is specified in the `component.widget` of the `grid-item`, it overrides all other icon settings.
- A jig with inputs in it's `title` will display without a title (blank) as the jig would not have received those inputs.

## Examples and code snippets

:::::ExpandableHeading
### Custom grid jig

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-4E4I4-UEZCwohqjOv3ATj-20250514-065552.png" size="60" position="center" caption="Custom Grid - Delivery " alt="Custom Grid - Delivery " signedSrc="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-4E4I4-UEZCwohqjOv3ATj-20250514-065552.png"}
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
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-AA7qAcJ34IJsD36GlpeAm-20241205-080912.png" size="60" position="center" caption="Auto Grid -Image Gallery  " alt="Auto Grid -Image Gallery  " signedSrc="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-AA7qAcJ34IJsD36GlpeAm-20241205-080912.png"}
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

:::::ExpandableHeading
### Custom grid jig with default widget icons and titles

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-OKrZ-aPdkRLtb-y-wYsci-20250605-062154.png" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-OKrZ-aPdkRLtb-y-wYsci-20250605-062154.png" size="66" width="1313" height="2676" position="center" caption="Default icons" alt="Default icons"}
:::

:::VerticalSplitItem
In this example, no icons are configured, so all widgets display the default icon. The `title` of the jig is displayed below the widget.
:::
::::

:::CodeblockTabs
grid-default-icons.jigx

```yaml
title: Grid default icons
type: jig.grid

children:
  - type: component.grid-item
    options:
      size: "1x1"
      children:
        type: component.jig-widget
        options:
          jigId: fuel-log

  - type: component.grid-item
    options:
      size: "1x1"
      children:
        type: component.jig-widget
        options:
          jigId: inspection

  - type: component.grid-item
    options:
      size: "2x2"
      children:
        type: component.jig-widget
        options:
          jigId: delivery-list

  - type: component.grid-item
    options:
      size: "1x1"
      children:
        type: component.jig-widget
        options:
          jigId: time-log

  - type: component.grid-item
    options:
      size: "1x1"
      children:
        type: component.jig-widget
        options:
          jigId: customer-rating
```

fuel-log.jigx

```yaml
title: Fuel log
description: Description of your Jig
type: jig.default

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

delivery-list.jigx

```yaml
title: Today's Delivery List
type: jig.default

onFocus: 
  type: action.reset-state
  options:
    state: =@ctx.solution.state
    
header:
  type: component.jig-header
  options:
    height: medium
    children:
      type: component.image
      options:
        source:
          uri: https://images.unsplash.com/photo-1480632563560-30f503c09195?w=500&auto=format&fit=crop&q=60&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8NHx8cGFyY2VsfGVufDB8fDB8fHww

datasources:
  deliveries: 
    type: datasource.static
    options:
      data:
        - id: 1
          delivery-no: ABB3456
          name: Paul Harrison
          address: 12 Maple Close Beacon Hill Boston
        - id: 2
          delivery-no: WDX5635
          name: Claudia Trent
          address:  77 N Washington Street Boston
        - id: 3
          delivery-no: YGD4465
          name: Kate Masson
          address: 200 Claredon Street FL 49 Boston
        - id: 4
          delivery-no: RDE3957
          name: Ronald Price
          address: 88 Wareham Street Boston    

children: 
  - type: component.list
    options:
      data: =@ctx.datasources.deliveries
      maximumItemsToRender: 8
      item: 
        type: component.list-item
        options:
          title: =@ctx.current.item.address
          subtitle: =@ctx.current.item.name
          leftElement: 
            element: icon
            icon: package-size-l                  
```

time-log.jigx

```yaml
title: Time log
type: jig.default

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
:::
:::::

:::::ExpandableHeading
### Custom grid with jig icons&#x20;

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
In this example, the widget `icons` are configured in each jig, and the jig `title` is displayed below the widget.
:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-jF1rEGTotK6gMI6Yr3SMk-20250605-062807.png" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-jF1rEGTotK6gMI6Yr3SMk-20250605-062807.png" size="66" width="1313" height="2676" position="center" caption="Jig icons " alt="Jig icons "}
:::
::::

:::CodeblockTabs
grid-jig-icons

```yaml
title: Grid jig icons
type: jig.grid

children:
  - type: component.grid-item
    options:
      size: "1x1"
      children:
        type: component.jig-widget
        options:
          jigId: fuel-log

  - type: component.grid-item
    options:
      size: "1x1"
      children:
        type: component.jig-widget
        options:
          jigId: inspection

  - type: component.grid-item
    options:
      size: "2x2"
      children:
        type: component.jig-widget
        options:
          jigId: delivery-list

  - type: component.grid-item
    options:
      size: "1x1"
      children:
        type: component.jig-widget
        options:
          jigId: time-log

  - type: component.grid-item
    options:
      size: "1x1"
      children:
        type: component.jig-widget
        options:
          jigId: customer-rating
```

fuel-log.jigx

```yaml
title: Fuel log
description: Description of your Jig
type: jig.default
# Configure the icon to display on the widget.
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

inspection.jigx

```yaml
title: Vehicle Inspection Checklist
type: jig.default
# Configure the icon to display on the widget.
icon: model-magnifying-stand

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

time-log.jigx

```yaml
title: Time log
type: jig.default
# Configure the icon to display on the widget.
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

delivery-list.jigx

```yaml
title: Today's Delivery List
type: jig.default
# Configure the icon to display on the widget.
icon: delivery-person-motorcycle

onFocus:
  type: action.reset-state
  options:
    state: =@ctx.solution.state

header:
  type: component.jig-header
  options:
    height: medium
    children:
      type: component.image
      options:
        source:
          uri: https://images.unsplash.com/photo-1480632563560-30f503c09195?w=500&auto=format&fit=crop&q=60&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8NHx8cGFyY2VsfGVufDB8fDB8fHww

datasources:
  deliveries:
    type: datasource.static
    options:
      data:
        - id: 1
          delivery-no: ABB3456
          name: Paul Harrison
          address: 12 Maple Close Beacon Hill Boston
        - id: 2
          delivery-no: WDX5635
          name: Claudia Trent
          address: 77 N Washington Street Boston
        - id: 3
          delivery-no: YGD4465
          name: Kate Masson
          address: 200 Claredon Street FL 49 Boston
        - id: 4
          delivery-no: RDE3957
          name: Ronald Price
          address: 88 Wareham Street Boston

children:
  - type: component.list
    options:
      data: =@ctx.datasources.deliveries
      maximumItemsToRender: 8
      item:
        type: component.list-item
        options:
          title: =@ctx.current.item.address
          subtitle: =@ctx.current.item.name
          leftElement:
            element: icon
            icon: package-size-l

```

customer-rating.jigx

```yaml
title: Rating
description: Customer Survey
type: jig.default
# Configure the icon to display on the widget.
icon: rating-five-star

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
:::
:::::

:::::ExpandableHeading
### Custom grid jig with custom widget icons

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-pPENIb9VM7Y5emq97n8fa-20250605-074146.png" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-pPENIb9VM7Y5emq97n8fa-20250605-074146.png" size="66" width="1313" height="2676" position="center" caption="Custom icons" alt="Custom icons"}
:::

:::VerticalSplitItem
In this example, the widget `icons` are configured in the `component.widget` of the `grid-item`, overriding the `icons` defined in the individual jigs. The jig `title` is displayed below each widget.
:::
::::

:::CodeblockTabs
grid-custom-icons.jigx

```yaml
title: Grid custom icons
type: jig.grid

children:
  - type: component.grid-item
    options:
      size: "1x1"
      children:
        type: component.jig-widget
        options:
          jigId: fuel-log
          # Configure a custom icon for the widget.
          icon: low-fuel

  - type: component.grid-item
    options:
      size: "1x1"
      children:
        type: component.jig-widget
        options:
          jigId: inspection
          # Configure a custom icon for the widget.
          icon: checklist

  - type: component.grid-item
    options:
      size: "2x2"
      children:
        type: component.jig-widget
        options:
          jigId: delivery-list
          # Configure a custom icon for the widget.
          icon: delivery-truck-2

  - type: component.grid-item
    options:
      size: "1x1"
      children:
        type: component.jig-widget
        options:
          jigId: time-log
          # Configure a custom icon for the widget.
          icon: time-clock-file-add

  - type: component.grid-item
    options:
      size: "1x1"
      children:
        type: component.jig-widget
        options:
          jigId: customer-rating
          # Configure a custom icon for the widget.
          icon: rating-star
```

fuel-log.jigx

```yaml
title: Fuel log
description: Description of your Jig
type: jig.default
# This icon is overridden by the icon configured in the grid jig.
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

inspection.jigx

```yaml
title: Vehicle Inspection Checklist
type: jig.default
# This icon is overridden by the icon configured in the grid jig.
icon: model-magnifying-stand

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

delivery-list.jigx

```yaml
title: Today's Delivery List
type: jig.default
# This icon is overridden by the icon configured in the grid jig.
icon: delivery-person-motorcycle

onFocus:
  type: action.reset-state
  options:
    state: =@ctx.solution.state

header:
  type: component.jig-header
  options:
    height: medium
    children:
      type: component.image
      options:
        source:
          uri: https://images.unsplash.com/photo-1480632563560-30f503c09195?w=500&auto=format&fit=crop&q=60&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8NHx8cGFyY2VsfGVufDB8fDB8fHww

datasources:
  deliveries:
    type: datasource.static
    options:
      data:
        - id: 1
          delivery-no: ABB3456
          name: Paul Harrison
          address: 12 Maple Close Beacon Hill Boston
        - id: 2
          delivery-no: WDX5635
          name: Claudia Trent
          address: 77 N Washington Street Boston
        - id: 3
          delivery-no: YGD4465
          name: Kate Masson
          address: 200 Claredon Street FL 49 Boston
        - id: 4
          delivery-no: RDE3957
          name: Ronald Price
          address: 88 Wareham Street Boston

children:
  - type: component.list
    options:
      data: =@ctx.datasources.deliveries
      maximumItemsToRender: 8
      item:
        type: component.list-item
        options:
          title: =@ctx.current.item.address
          subtitle: =@ctx.current.item.name
          leftElement:
            element: icon
            icon: package-size-l

```

time-log.jigx

```yaml
title: Time log
type: jig.default
# This icon is overridden by the icon configured in the grid jig.
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

customer-rating.jigx

```yaml
title: Rating
description: Customer Survey
type: jig.default
# This icon is overridden by the icon configured in the grid jig.
icon: rating-five-star

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
:::
:::::

:::::ExpandableHeading
### Custom grid jig with no widget and image titles

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
This example demonstrates that setting the `title` property in the`component.widget` of the `grid-item` overrides the default jig `title`. Configuring the `component.widget` `title` as a blank space ( ' ' ) removes the title entirely. Custom `icons` are also configured in the `component.widget` of the grid jig for each widget.
:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-Va-TuCoDex7BnFZwAaCZp-20250605-075319.png" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-Va-TuCoDex7BnFZwAaCZp-20250605-075319.png" size="66" width="1313" height="2676" position="center" caption="Widgets with no titles" alt="Widgets with no titles"}
:::
::::

:::CodeblockTabs
grid-custom-no-titles.jigx

```yaml
title: Grid custom no titles icons
type: jig.grid

children:
  - type: component.grid-item
    options:
      size: "4x2"
      children:
        type: component.image
        options:
          source:
            uri: https://images.unsplash.com/photo-1507183711269-1235bed98f14?q=80&w=1548&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D

  - type: component.grid-item
    options:
      size: "1x1"
      children:
        type: component.jig-widget
        options:
          jigId: fuel-log
          # Configure a custom icon for the widget.
          icon: fuel-pump-reload
          # Using a blank space (' ') for the title removes it entirely.
          title: ' '

  - type: component.grid-item
    options:
      size: "1x1"
      children:
        type: component.jig-widget
        options:
          jigId: inspection
          # Configure a custom icon for the widget.
          icon: air-quality-check-magnifying-glass
          # Using a blank space (' ') for the title removes it entirely.
          title: ' '
  - type: component.grid-item
    options:
      size: "2x2"
      children:
        type: component.jig-widget
        options:
          jigId: delivery-list
          # Configure a custom icon for the widget.
          icon: delivery-person-motorcycle-1
          # Using a blank space (' ') for the title removes it entirely.
          title: ' '
  - type: component.grid-item
    options:
      size: "1x1"
      children:
        type: component.jig-widget
        options:
          jigId: time-log
          # Configure a custom icon for the widget.
          icon: time-clock-circle-alternate
          # Using a blank space (' ') for the title removes it entirely.
          title: ' '
  - type: component.grid-item
    options:
      size: "1x1"
      children:
        type: component.jig-widget
        options:
          jigId: customer-rating
          # Configure a custom icon for the widget.
          icon: rating-five-star
          # Using a blank space (' ') for the title removes it entirely.
          title: ' '
```

fuel-log.jigx

```yaml
title: Fuel log
description: Description of your Jig
type: jig.default

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

delivery-list.jigx

```yaml
title: Today's Delivery List
type: jig.default

onFocus:
  type: action.reset-state
  options:
    state: =@ctx.solution.state

header:
  type: component.jig-header
  options:
    height: medium
    children:
      type: component.image
      options:
        source:
          uri: https://images.unsplash.com/photo-1480632563560-30f503c09195?w=500&auto=format&fit=crop&q=60&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8NHx8cGFyY2VsfGVufDB8fDB8fHww

datasources:
  deliveries:
    type: datasource.static
    options:
      data:
        - id: 1
          delivery-no: ABB3456
          name: Paul Harrison
          address: 12 Maple Close Beacon Hill Boston
        - id: 2
          delivery-no: WDX5635
          name: Claudia Trent
          address: 77 N Washington Street Boston
        - id: 3
          delivery-no: YGD4465
          name: Kate Masson
          address: 200 Claredon Street FL 49 Boston
        - id: 4
          delivery-no: RDE3957
          name: Ronald Price
          address: 88 Wareham Street Boston

children:
  - type: component.list
    options:
      data: =@ctx.datasources.deliveries
      maximumItemsToRender: 8
      item:
        type: component.list-item
        options:
          title: =@ctx.current.item.address
          subtitle: =@ctx.current.item.name
          leftElement:
            element: icon
            icon: package-size-l

```

time-log.jigx

```yaml
title: Time log
type: jig.default

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
:::
:::::

:::::ExpandableHeading
### Custom grid with custom widget and image titles

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-W6_bRSRg3PqeSS47-WjXp-20250605-080654.png" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-W6_bRSRg3PqeSS47-WjXp-20250605-080654.png" size="66" width="1313" height="2676" position="center" caption="Custom titles" alt="Custom titles"}
:::

:::VerticalSplitItem
This example demonstrates that setting the `title` property in the `component.widget` `grid-item` overrides the default jig `title`. Custom icons are also configured in the `component.widget` of the grid jig for each widget. For image widgets, the title configured in the `component.image` of the `grid-item` overlays the image.
:::
::::

:::CodeblockTabs
grid-custom-titles.jigx

```yaml
title: Grid custom titles
type: jig.grid

children:
  - type: component.grid-item
    options:
      size: "4x2"
      children:
        type: component.image
        options:
          source:
            uri: https://images.unsplash.com/photo-1507183711269-1235bed98f14?q=80&w=1548&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D
          # Add a custom title to display on the image.
          title: Today's quote
  - type: component.grid-item
    options:
      size: "1x1"
      children:
        type: component.jig-widget
        options:
          jigId: fuel-log
          # Configure a custom icon for the widget.
          icon: fuel-pump-reload
          # Add a custom title to display below the widget.
          title: Fuel

  - type: component.grid-item
    options:
      size: "1x1"
      children:
        type: component.jig-widget
        options:
          jigId: inspection
          # Configure a custom icon for the widget.
          icon: air-quality-check-magnifying-glass
          # Add a custom title to display below the widget.
          title: Checklist
  - type: component.grid-item
    options:
      size: "2x2"
      children:
        type: component.jig-widget
        options:
          jigId: delivery-list
          # Configure a custom icon for the widget.
          icon: delivery-person-motorcycle-1
          # Add a custom title to display below the widget.
          title: Deliveries
  - type: component.grid-item
    options:
      size: "1x1"
      children:
        type: component.jig-widget
        options:
          jigId: time-log
          # Configure a custom icon for the widget.
          icon: time-clock-circle-alternate
          # Add a custom title to display below the widget.
          title: Job card
  - type: component.grid-item
    options:
      size: "1x1"
      children:
        type: component.jig-widget
        options:
          jigId: customer-rating
          # Configure a custom icon for the widget.
          icon: rating-five-star
          # Add a custom title to display below the widget.
          title: Rating
```

fuel-log.jigx

```yaml
# The widget title is overridden by the title configured in the grid jig.
title: Fuel log
type: jig.default

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

inspection.jigx

```yaml
# The widget title is overridden by the title configured in the grid jig.
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

delivery-list.jigx

```yaml
# The widget title is overridden by the title configured in the grid jig.
title: Today's Delivery List
type: jig.default

onFocus:
  type: action.reset-state
  options:
    state: =@ctx.solution.state

header:
  type: component.jig-header
  options:
    height: medium
    children:
      type: component.image
      options:
        source:
          uri: https://images.unsplash.com/photo-1480632563560-30f503c09195?w=500&auto=format&fit=crop&q=60&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8NHx8cGFyY2VsfGVufDB8fDB8fHww

datasources:
  deliveries:
    type: datasource.static
    options:
      data:
        - id: 1
          delivery-no: ABB3456
          name: Paul Harrison
          address: 12 Maple Close Beacon Hill Boston
        - id: 2
          delivery-no: WDX5635
          name: Claudia Trent
          address: 77 N Washington Street Boston
        - id: 3
          delivery-no: YGD4465
          name: Kate Masson
          address: 200 Claredon Street FL 49 Boston
        - id: 4
          delivery-no: RDE3957
          name: Ronald Price
          address: 88 Wareham Street Boston

children:
  - type: component.list
    options:
      data: =@ctx.datasources.deliveries
      maximumItemsToRender: 8
      item:
        type: component.list-item
        options:
          title: =@ctx.current.item.address
          subtitle: =@ctx.current.item.name
          leftElement:
            element: icon
            icon: package-size-l

```

time-log.jigx

```yaml
# The widget title is overridden by the title configured in the grid jig.
title: Time log
type: jig.default

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

customer-rating.jigx

```yaml
# The widget title is overridden by the title configured in the grid jig.
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
:::
:::::

:::::ExpandableHeading
### Custom grid widgets with OnPress event&#x20;

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
In this example, each `component.widget` is configured with an `onPress` event that executes an action, such as `opening-a-map` or displaying an `info-modal`. Note that the configured `onPress` event overrides the default behavior of opening the jig specified in the `jigId`.
:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-ys9CzEMHsUELDhiBg37KY-20250605-092415.gif" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-ys9CzEMHsUELDhiBg37KY-20250605-092415.gif" size="66" width="681" height="1377" position="center" caption="Widget with onpress" alt="Widget with onpress"}
:::
::::

:::CodeblockTabs
grid-custom-onpress.jigx

```yaml
title: Grid custom onpress
type: jig.grid

children:
  - type: component.grid-item
    options:
      size: "4x2"
      children:
        type: component.image
        options:
          source:
            uri: https://images.unsplash.com/photo-1507183711269-1235bed98f14?q=80&w=1548&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D
          title: Today's quote
  - type: component.grid-item
    options:
      size: "1x1"
      children:
        type: component.jig-widget
        options:
          jigId: fuel-log
          icon: fuel-pump-reload
          title: Fuel
          # Configure an action that 
          onPress:
            type: action.open-media-picker
            options:
              mediaType: image

  - type: component.grid-item
    options:
      size: "1x1"
      children:
        type: component.jig-widget
        options:
          jigId: inspection
          icon: air-quality-check-magnifying-glass
          title: Checklist
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
  - type: component.grid-item
    options:
      size: "1x1"
      children:
        type: component.jig-widget
        options:
          jigId: delivery-list
          icon: delivery-person-motorcycle-1
          title: Deliveries
          onPress:
            type: action.open-map
            options:
              address: 1600 Amphitheatre Parkway, Mountain View, CA 94043

  - type: component.grid-item
    options:
      size: "1x1"
      children:
        type: component.jig-widget
        options:
          jigId: time-log
          icon: time-clock-circle-alternate
          title: Log
          onPress:
            type: action.open-url
            options:
              url: https://jigx.com/solutions/construction/
```
:::
:::::

