---
title: list
slug: 9Auy-list
description: Learn how to use list widgets in Jig to create dynamic and customizable lists. Explore code snippets and examples for creating list items with various elements. Discover two types of list widgets - stage component items and product items - and their speci
createdAt: Thu Jun 09 2022 20:14:58 GMT+0000 (Coordinated Universal Time)
updatedAt: Mon Mar 10 2025 09:54:31 GMT+0000 (Coordinated Universal Time)
---

&#x20;Whenever a list jig is configured either in the <a href="" target="_blank">jig.list</a>, or <a href="https://docs.jigx.com/examples/list-item" target="_blank">list-item </a>component, the list is automatically populated on the surface of the widget without needing additional configuration.&#x20;
There is also the option to extend the list widget by using the `Extend List Widget` property, which reuses the list jig configuration and its data to extend or override some of the properties in the widget. The item data is called from `=@ctx.current.item.value`.

There are, instances when you want to create a list widget on a jig that is not a list jig, such as a `jig.default`. This is primarily where the list widget is used.&#x20;

::::VerticalSplit{layout}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/x_tcUv7lpa0tsER9sVivd_img3900.PNG" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/x_tcUv7lpa0tsER9sVivd_img3900.PNG" size="74" width="1125" height="2436" position="center" caption="List widgets" alt="List widgets"}
:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/U6BPOZ0OYlFedss3Z_mND_img3901.PNG" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/U6BPOZ0OYlFedss3Z_mND_img3901.PNG" size="74" width="1125" height="2436" position="center" caption="List widgets" alt="List widgets"}
:::
::::

## ****Configuration options****

A list widget can be used on any type of jig, i.e. list, default, composite, calendar and document.

| **Core options** |                                                                                                                                                                                                                                                                                                                |
| ---------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `item`           | The `item` property includes the setup options of:<br />* <a href="https://docs.jigx.com/examples/stage" target="_blank">Stage</a>
* <a href="https://docs.jigx.com/examples/product-item" target="_blank">Product-item</a>
* <a href="https://docs.jigx.com/examples/list-item" target="_blank">List-item</a> |

| ### Other options | ****                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| ----------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `badge`           | Add a badge to the list widget to highlight critical information and capture the user's attention, ensuring key updates or notifications are easily noticeable within the app. The badge can be configured at the root level of the jig file:&#xA;-  To display as a red dot using the `empty` value.&#xA;-  A red dot with a number using an expression to perform a count. &#xA;For example, counting the number of tasks in the list. |
| `bottom`          | The <a href="https://docs.jigx.com/examples/titles" target="_blank">titles</a> component will be added to the bottom of the widget.                                                                                                                                                                                                                                                                                                      |
| `data`            | Provide the datasource for the list. For example:&#xA;`data: =@ctx.datasources.tasklist`                                                                                                                                                                                                                                                                                                                                                 |
| `footer`          | Add text to the footer of the widget.                                                                                                                                                                                                                                                                                                                                                                                                    |
| `footerAlign`     | Align the footer text to `left`, `right`, `center`.                                                                                                                                                                                                                                                                                                                                                                                      |
| `placeholders`    | Specify a placeholder text to display if there is no data, for example - `title: No data to display`.                                                                                                                                                                                                                                                                                                                                    |
| `top`             | The <a href="https://docs.jigx.com/examples/titles" target="_blank">titles</a> component will be added to the top of the widget.                                                                                                                                                                                                                                                                                                         |

| ### State Configuration  | **Key**              | **Notes**                                                                                                                                                                                 |
| ------------------------ | -------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `=@ctx.current.state.`   | amount&#xA;checked   | - Applies to a list, list.item, product-item, and stage components. List's data is an array of records. The `=@ctx.current.state` is the state of the current object in the array. &#x20; |
| `=@ctx.component.state.` | amount&#xA;checked   | * State is the variable of the component.                                                                                                                                                 |
| `=@ctx.solution.state.`  | activeItemId&#xA;now | - Global state variable that can be used throughout the solution.                                                                                                                         |

## Configuration options **for extended list widget**

The `Extended List Widget` can only be used on a list jig . The purpose of using this widget is to customize what shows in the widget on the Home Hub rather than showing its automatic list display.  The `Extended List Widget` must be configured with a size 2x2 or greater. Reuse the data in the list jig , for example, `=@ctx.datasources.users.title` or `=@ctx.current.item.value`.

| **Core options** |                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| ---------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `item`           | The `item` property includes the setup options of:<br />* [bar-chart](./../Components/charts/bar-chart.md)
* [expander](./../Components/expander.md)
* <a href="https://docs.jigx.com/examples/stage" target="_blank">Stage</a>
* <a href="https://docs.jigx.com/examples/product-item" target="_blank">Product-item</a>
* <a href="https://docs.jigx.com/examples/list-item" target="_blank">List-item</a>
* [pie-chart](./../Components/charts/pie-chart.md) |

## Examples and code snippets ****

:::::ExpandableHeading
### Automatic widget display because of list jig type (Simple)

::::VerticalSplit{layout="left"}
:::VerticalSplitItem
![2x2 list](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/z9yZ9dIPXE6foUtoUUyt3_list1iphone13blueportrait.png "2x2 list")
:::

:::VerticalSplitItem
When using a `jig.list` and any size widget larger than 1x1 the list will automatically be displayed without additional configurations. This is visible in this example.&#x20;

In this example,  the list on the widget is the same as the `jig.list` once the widget has been accessed.&#x20;

**Examples:
**See the complete example using static data in <a href="https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/list-item/static-data/list-with-left-elements/list-with-left-checkbox-sd.jigx" target="_blank">GitHub</a>.
See the complete example using dynamic data in <a href="https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/list-item/dynamic-data/list-with-left-elements/list-with-left-avatar-dd.jigx" target="_blank">GitHub</a>.

**Datasources:
**See the complete datasource for static data in <a href="https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/services/repair-services-static.jigx" target="_blank">GitHub</a>.&#x20;
See the complete datasource for dynamic data in <a href="https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/services/cleaning-services-dynamic.jigx" target="_blank">GitHub</a>.&#x20;
:::
::::

:::CodeblockTabs
list-widget (Static)

```yaml
data: =@ctx.datasources.repair-services-static
item:
  type: component.list-item
  options:
    title: =@ctx.current.item.service
    subtitle: =@ctx.current.item.description
```

list-widget (dynamic)

```yaml
data: =@ctx.datasources.cleaning-services-dynamic
item:
  type: component.list-item
  options:
    title: =@ctx.current.item.service
    subtitle: =@ctx.current.item.area
```

grid-item

```yaml
# Grid-item for the static jig.
children:
  - type: component.grid-item
    options:
      size: "2x2"
      children: 
        type: component.jig-widget
        options:
          jigId: list-widget
```
:::
:::::

:::::ExpandableHeading
### Automatic widget display because of list jig type (UI elements)

::::VerticalSplit{layout="left"}
:::VerticalSplitItem
![2x2 list with avatar](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/rinQmlbPzRXwTyKEcgBvq_listcompiphone13blueportrait.png "2x2 list with avatar")
:::

:::VerticalSplitItem
When using a `jig.list` and any size widget larger than 1x1 the list will automatically be displayed without additional configurations.&#x20;

In this example, the list on the widget is exactly the same as the `jig.list` once the widget has been accessed.&#x20;

**Examples:
**See the complete example using static data in <a href="https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/components/list-item/static-data/list-with-left-elements/list-with-left-checkbox-sd.jigx" target="_blank">GitHub</a>.&#x20;
See the complete example using dynamic data in <a href="https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/components/list-item/dynamic-data/list-with-left-elements/list-with-left-avatar-dd.jigx" target="_blank">GitHub</a>.&#x20;

**Datasources:
**See the complete datasource for static data in <a href="https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/services/repair-services-static.jigx" target="_blank">GitHub</a>.&#x20;
See the complete datasource for dynamic data in <a href="https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/services/cleaning-services-dynamic.jigx" target="_blank">GitHub</a>.
:::
::::

:::CodeblockTabs
list-with-left-element (static)

```yaml
data: =@ctx.datasources.repair-services-static
item:
  type: component.list-item
  options:
    title: =@ctx.current.item.service
    subtitle: =@ctx.current.item.description
    leftElement:
      element: checkbox
      initialValue: =(@ctx.current.item.materials) = true ? true :false
```

list-with-left-element (dynamic)

```yaml
data: =@ctx.datasources.cleaning-services-dynamic
item:
  type: component.list-item
  options:
    title: =@ctx.current.item.service
    subtitle: =@ctx.current.item.time & ' minutes for task completion'
    leftElement: 
      element: avatar
      text: $substring($substringBefore(@ctx.current.item.service, " "), 1, 1) & $substring($substringAfter(@ctx.current.item.service, " ") , 1, 1)
      uri: =@ctx.current.item.illustration
```

grid-item

```yaml
# Grid-item for the static jig.
children:
  - type: component.grid-item
    options:
      size: "2x2"
      children: 
        type: component.jig-widget
        options:
          jigId: list-with-left-element
```
:::
:::::

:::::ExpandableHeading
### List widget with stage component items

::::VerticalSplit{layout="left"}
:::VerticalSplitItem
![2 stage list widget](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/wLfGvJAdHpWNfCmBtm4ix_liststageiphone13blueportrait.png "2 stage list widget")
:::

:::VerticalSplitItem
This example is for list items that have a left and right element and shows a start-and-end. An example of this is flight schedules, however, this can be used for many different use cases as you can choose a different icon. Here a slightly different setup is used to that in the actual list to show you the widget configuration.&#x20;

**Examples:
**See the complete example using static data in <a href="https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/widgets/list/static-data/widget-list-stage-sd.jigx" target="_blank">GitHub</a>.
See the complete example using dynamic data in <a href="https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/widgets/list/dynamic-data/widget-list-stage-dd.jigx" target="_blank">GitHub</a>.&#x20;

**Datasources:
**See the complete datasource for static data in <a href="https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/expanders%20and%20stages/flight-schedule-static.jigx" target="_blank">GitHub</a>.&#x20;
See the complete datasource for dynamic data in <a href="https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/expanders%20and%20stages/flight-schedule-dynamic.jigx" target="_blank">GitHub</a>.&#x20;
:::
::::

:::CodeblockTabs
stage-list-widget (static)

```yaml
widgets:
  stageStatic-2x2:
    type: widget.list
    options:
      data: =@ctx.datasources.flight-schedule-static
      item: 
        type: component.stage
        options:
          icon: plane-1
          right:
            title: =@ctx.current.item.toabrv
            subtitle: =@ctx.current.item.to
          left:
            title: =@ctx.current.item.fromabrv
            subtitle: =@ctx.current.item.from
```

stage-list-widget (dynamic)

```yaml
widgets:
  stageDD-2x2:
    type: widget.list
    options:
      data: =@ctx.datasources.flight-schedule-dynamic
      item: 
        type: component.stage
        options:
          icon: plane-2
          right:
            title: =@ctx.current.item.toabrv
            subtitle: =@ctx.current.item.to
          left:
            title: =@ctx.current.item.fromabrv
            subtitle: =@ctx.current.item.from
```

grid-item

```yaml
# Grid-item for the static jig.
children:
  - type: component.grid-item
    options:
      size: "2x2"
      children: 
        type: component.jig-widget
        options:
          jigId: stage-list-widget
          widgetId: stageStatic-2x2
```
:::
:::::

:::::ExpandableHeading
### List widget with product items

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/SmVasJ9L4i3NPUtt8l722_listproductiphone13blueportrait.png" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/SmVasJ9L4i3NPUtt8l722_listproductiphone13blueportrait.png" size="80" width="1570" height="2932" position="center" caption="2x2 product-item list widget" alt="2x2 product-item list widget"}
:::

:::VerticalSplitItem
This example shows product items with their images and respective prices.

**Examples:
**See the complete example using static data in <a href="https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/widgets/list/static-data/widget-list-product-item-sd.jigx" target="_blank">GitHub</a>.&#x20;
See the complete example using dynamic data in <a href="https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/widgets/list/dynamic-data/widget-list-product-item-dd.jigx" target="_blank">GitHub</a>.&#x20;

**Datasources:
**See the complete datasource for static data in <a href="https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/products/products.jigx" target="_blank">GitHub</a>.
See the complete datasource for dynamic data in <a href="https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/products/products-dynamic.jigx" target="_blank">GitHub</a>.
:::
::::

:::CodeblockTabs
list-product-widget (static)&#x20;

```yaml
widgets:
  productStatic-2x2:
    type: widget.list
    options:
      data: =@ctx.datasources.products
      item:
        type: component.product-item
        options:
          title: =@ctx.current.item.title
          image: 
            uri: =@ctx.current.item.uri
          price:
            value: =@ctx.current.item.price
            format:
              numberStyle: currency
```

list-product-widget (dynamic)

```yaml
widgets:
  productDD-2x2:
    type: widget.list
    options:
      data: =@ctx.datasources.products-dynamic
      item:
        type: component.product-item
        options:
          title: =@ctx.current.item.title
          image: 
            uri: =@ctx.current.item.uri
          price:
            value: =@ctx.current.item.price
            format:
              numberStyle: currency
```

grid-item

```yaml
# Grid-item for the static jig.
children:
  - type: component.grid-item
    options:
      size: "2x2"
      children: 
        type: component.jig-widget
        options:
          jigId: list-product-widget
          widgetId: productStatic-2x2
```
:::
:::::

:::::ExpandableHeading
### List widget with list items

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/rZCv7iRFImXiqOzMsjRK-_listsdiphone13blueportrait.png" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/rZCv7iRFImXiqOzMsjRK-_listsdiphone13blueportrait.png" size="76" width="1570" height="2932" position="center" caption="2x2 list-item basic widget" alt="2x2 list-item basic widget"}
:::

:::VerticalSplitItem
This example shows a basic `component.list-item` setup.&#x20;

**Examples:
**See the complete example using static data in <a href="https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/widgets/list/static-data/widget-list-items-sd.jigx" target="_blank">GitHub</a>.&#x20;
See the complete example using dynamic data in <a href="https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/widgets/list/dynamic-data/widget-list-items-dd.jigx" target="_blank">GitHub</a>.

**Datasources:
**See the complete datasource for static data in <a href="https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/events-and-calendars/calendar-data.jigx" target="_blank">GitHub</a>.
See the complete datasource for dynamic data in <a href="https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/events-and-calendars/calendar-data-dynamic.jigx" target="_blank">GitHub</a>.&#x20;
:::
::::

:::CodeblockTabs
list-items-widget (static)

```yaml
widgets:
  listitemStatic-2x2:
    type: widget.list
    options:
      data: =@ctx.datasources.calendar-data
      item: 
        type: component.list-item
        options:
          title: =@ctx.current.item.title
          subtitle: =@ctx.current.item.location
```

list-items-widget (dynamic)

```yaml
widgets:
  listitemDD-2x2:
    type: widget.list
    options:
      data: =@ctx.datasources.calendar-data-dynamic
      item: 
        type: component.list-item
        options:
          title: =@ctx.current.item.title
          subtitle: =@ctx.current.item.location
          label:
            title: =@ctx.current.item.title
          divider: solid
          leftElement: 
            element: avatar
            text: ''
            uri: =@ctx.current.item.avatar
```

grid-item

```yaml
# Grid-item for the static jig.
children:
  - type: component.grid-item
    options:
      size: "2x2"
      children: 
        type: component.jig-widget
        options:
          jigId: list-items-widget
          widgetId: listitemStatic-2x2
```
:::
:::::

::::ExpandableHeading
### Extended list widget 2x4, 4x2, 4x4

::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/s4ML69T6TZa5bCeOaYjKr_widget-extend.PNG" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/s4ML69T6TZa5bCeOaYjKr_widget-extend.PNG" size="80" width="2546" height="2500" position="center" caption="Extended list widget" alt="Extended list widget"}

This example shows how the `Extend List Widget` reuses the data from a single `jig.list` to customize the widget's appearance.  In the image above:

1. &#x20;The first widget is the default `2x2` widget that is automatically displayed.&#x20;
2. The second widget is a `2x4` using the `Extend List widget` to only show the `titles` in the list.
3. The third widget is a `4x2` using the `Extend List Widget `with a `component.stage` configuration.&#x20;
4. The fourth widget is a `4x4` using the `Extend List Widget` to show a customized `leftElement` and `RightElement`.

:::CodeblockTabs
extended-list-widget (2x4)

```yaml
data: =@ctx.datasources.users
item:
  type: component.list-item
  options:
    divider: solid
    title: =@ctx.current.item.title
    subtitle: =@ctx.current.item.subtitle
    description: =@ctx.current.item.description
    leftElement:
      element: avatar
      text: =@ctx.current.item.avatar-text
      uri: =@ctx.current.item.avatar
    rightElement:
      element: icon
      icon: arrow-right

widgets:
 # "2x2" automatically populates a list on the widget without needing additional configurations 
  extend-2x4: 
    item: 
      type: component.list-item
      options:
        title: =@ctx.current.item.title
```

extended-list-widget (4x2)

```yaml
data: =@ctx.datasources.users
item:
  type: component.list-item
  options:
    divider: solid
    title: =@ctx.current.item.title
    subtitle: =@ctx.current.item.subtitle
    description: =@ctx.current.item.description
    leftElement:
      element: avatar
      text: =@ctx.current.item.avatar-text
      uri: =@ctx.current.item.avatar
    rightElement:
      element: icon
      icon: arrow-right

widgets:
 # "2x2" automatically populates a list on the widget without needing additional configurations 
  extend-4x2: 
    item: 
      type: component.stage
      options:
        icon: person
        right:
          title: =@ctx.current.item.title
        left:
          title: =@ctx.current.item.description
```

extended-list-widget (4x4)

```yaml
data: =@ctx.datasources.users
item:
  type: component.list-item
  options:
    divider: solid
    title: =@ctx.current.item.title
    subtitle: =@ctx.current.item.subtitle
    description: =@ctx.current.item.description
    leftElement:
      element: avatar
      text: =@ctx.current.item.avatar-text
      uri: =@ctx.current.item.avatar
    rightElement:
      element: icon
      icon: arrow-right

widgets: 
 # "2x2" automatically populates a list on the widget without needing additional configurations      
  extend-4x4: 
    item: 
      type: component.list-item
      options:
        title: =@ctx.current.item.title
        leftElement: 
          element: avatar
          text: =@ctx.current.item.avatar
          uri: =@ctx.current.item.avatar
        rightElement: 
          element: switch
          initialValue: " "
```

datasource (static)

```yaml
datasources:
  users:
    type: datasource.static
    options:
      data:
        - title: John
          subtitle: Manager
          description: HR
          avatar-text: N/A
          avatar: https://images.unsplash.com/photo-1633332755192-727a05c4013d?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1480&q=80
        - title: Mary
          subtitle: Accountant
          description: Finance
          avatar-text: N/A
          avatar: https://images.unsplash.com/photo-1494790108377-be9c29b29330?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=987&q=80
        - title: Paul
          subtitle: Auditor
          description: External
          avatar-text: N/A
          avatar: https://images.unsplash.com/photo-1570295999919-56ceb5ecca61?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1480&q=80
        - title: Bob
          subtitle: Accountant
          description: Finance
          avatar-text: N/A
          avatar: https://images.unsplash.com/photo-1568602471122-7832951cc4c5?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8OHx8bWVuJTIwYXZhdGFyc3xlbnwwfHwwfHx8MA%3D%3D&auto=format&fit=crop&w=500&q=60
        - title: Jane
          subtitle: HR specialist
          description: HR
          avatar-text: N/A
          avatar: https://images.unsplash.com/photo-1678346496584-e81410d1e697?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHx0b3BpYy1mZWVkfDE0fHRvd0paRnNrcEdnfHxlbnwwfHx8fHw%3D&auto=format&fit=crop&w=500&q=60
        - title: Fiona
          subtitle: Data capturer
          description: Finance
          avatar-text: N/A
          avatar: https://plus.unsplash.com/premium_photo-1690407617686-d449aa2aad3c?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8NXx8d29tYW4lMjBhdmF0YXJzfGVufDB8fDB8fHww&auto=format&fit=crop&w=500&q=60
     
```

grid-item

```yaml
# Grid-item for the extend-2x4 jig.
children:
  - type: component.grid-item
    options:
      size: "2x4"
      children: 
        type: component.jig-widget
        options:
          jigId: extended-list-widget (2x4)
          widgetId: extend-2x4
```
:::
::::

### Group list widgets&#x20;

See the following examples under groups:

- <a href="https://docs.jigx.com/examples/group#utr1x" target="_blank">Group with chart and list (size: 4x4, split: horizontal)</a>
- <a href="https://docs.jigx.com/examples/group#Lk_2j" target="_blank">Group with chart and list (size: 4x4, split: vertical)</a>
- <a href="https://docs.jigx.com/examples/group#3Wi36" target="_blank">Group with avatar and list (size: 4x2)</a>
- <a href="https://docs.jigx.com/examples/group#VWndb" target="_blank">Group with value and bar-chart (size: 2x4)</a>

## **See also**

- [State]()

