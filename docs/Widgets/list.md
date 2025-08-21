# list

Whenever a list jig is configured either in the [list](./../Components/list.md) , or [list-item](./../Components/list/list-item.md) component, the list is automatically populated on the surface of the widget without needing additional configuration.
There is also the option to extend the list widget by using the `Extend List Widget` property, which reuses the list jig configuration and its data to extend or override some of the properties in the widget. The item data is called from `=@ctx.current.item.value`.

There are, instances when you want to create a list widget on a jig that is not a list jig, such as a `jig.default`. This is primarily where the list widget is used.

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/x_tcUv7lpa0tsER9sVivd_img3900.PNG" size="74" position="center" caption="List widgets" alt="List widgets" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/x_tcUv7lpa0tsER9sVivd_img3900.PNG" width="800" height="1732" darkWidth="800" darkHeight="1732"}
:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/U6BPOZ0OYlFedss3Z_mND_img3901.PNG" size="74" position="center" caption="List widgets" alt="List widgets" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/U6BPOZ0OYlFedss3Z_mND_img3901.PNG" width="800" height="1732" darkWidth="800" darkHeight="1732"}
:::
::::

## Configuration options

A list widget can be used on any type of jig, i.e. list, default, composite, calendar and document.

<table isTableHeaderOn="true" selectedColumns="" selectedRows="" selectedTable="false" columnWidths="135">
  <tr>
    <td selected="false" align="left">
      <p><strong>Core options</strong></p>
    </td>
    <td selected="false" align="left">
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>item</code></p>
    </td>
    <td selected="false" align="left">
      <p>The <code>item</code> property includes the setup options of: <a href="https://docs.jigx.com/examples/product-item">Product-item </a><a href="https://docs.jigx.com/examples/list-item">List-item</a></p>
    </td>
  </tr>
</table>

<table isTableHeaderOn="true" selectedColumns="" selectedRows="" selectedTable="false" columnWidths="138">
  <tr>
    <td selected="false" align="left">
      <p><strong>Other options</strong></p>
    </td>
    <td selected="false" align="left">
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>badge</code></p>
    </td>
    <td selected="false" align="left">
      <p>Add a badge to the list widget to highlight critical information and capture the user's attention, ensuring key updates or notifications are easily noticeable within the app. The badge can be configured at the root level of the jig file:</p>
      <ul>
      <li>To display as a red dot using the <code>empty</code> value.</li>
      <li>A red dot with a number using an expression to perform a count. For example, counting the number of tasks in the list.</li>
      </ul>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>bottom</code></p>
    </td>
    <td selected="false" align="left">
      <p>The component will be added to the bottom of the widget.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>data</code></p>
    </td>
    <td selected="false" align="left">
      <p>Provide the datasource for the list. For example: <code>data: =@ctx.datasources.tasklist</code></p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>footer</code></p>
    </td>
    <td selected="false" align="left">
      <p>Add text to the footer of the widget.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>footerAlign</code></p>
    </td>
    <td selected="false" align="left">
      <p>Align the footer text to <code>left</code>, <code>right</code>, <code>center</code>.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>placeholders</code></p>
    </td>
    <td selected="false" align="left">
      <p>Specify a placeholder text to display if there is no data, for example - <code>title: No data to display</code>.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>top</code></p>
    </td>
    <td selected="false" align="left">
      <p>The component will be added to the top of the widget.</p>
    </td>
  </tr>
</table>

<table isTableHeaderOn="true" selectedColumns="" selectedRows="" selectedTable="false" columnWidths="231,124">
  <tr>
    <td selected="false" align="left">
      <p><strong>State Configuration</strong></p>
    </td>
    <td selected="false" align="left">
      <p><strong>Key</strong></p>
    </td>
    <td selected="false" align="left">
      <p><strong>Notes</strong></p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>=@ctx.current.state.</code></p>
    </td>
    <td selected="false" align="left">
      <p>amount checked</p>
    </td>
    <td selected="false" align="left">
      <p>Applies to a list, list.item, product-item, and stage components. List's data is an array of records. The <code>=@ctx.current.state</code> is the state of the current object in the array.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>=@ctx.component.state.</code></p>
    </td>
    <td selected="false" align="left">
      <p>amount checked</p>
    </td>
    <td selected="false" align="left">
      <p>State is the variable of the component.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>=@ctx.solution.state.</code></p>
    </td>
    <td selected="false" align="left">
      <p>activeItemId now</p>
    </td>
    <td selected="false" align="left">
      <p>Global state variable that can be used throughout the solution.</p>
    </td>
  </tr>
</table>

## Configuration options for extended list widget

The `Extended List Widget` can only be used on a list jig . The purpose of using this widget is to customize what shows in the widget on the Home Hub rather than showing its automatic list display.  The `Extended List Widget` must be configured with a size 2x2 or greater. Reuse the data in the list jig , for example, `=@ctx.datasources.users.title` or `=@ctx.current.item.value`.

<table isTableHeaderOn="true" selectedColumns="" selectedRows="" selectedTable="false" columnWidths="126">
  <tr>
    <td selected="false" align="left">
      <p><strong>Core options</strong></p>
    </td>
    <td selected="false" align="left">
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>item</code></p>
    </td>
    <td selected="false" align="left">
      <p>The <code>item</code> property includes the setup options of:</p>
      <ul>
      <li> <a href="./../Components/expander.md">expander</a></li>
      <li><a href="https://docs.jigx.com/examples/stage">Stage</a></li>
      <li><a href="https://docs.jigx.com/examples/product-item">Product-item</a></li>
      <li><a href="https://docs.jigx.com/examples/list-item">List-item</a></li>
      <li><a href="./../Components/charts/pie-chart.md">pie-chart</a></li>
      </ul>
    </td>
  </tr>
</table>

## Examples and code snippets

:::::ExpandableHeading
## Automatic widget display because of list jig type (Simple)

::::VerticalSplit{layout="left"}
:::VerticalSplitItem
![2x2 list](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/z9yZ9dIPXE6foUtoUUyt3_list1iphone13blueportrait.png "2x2 list")
:::

:::VerticalSplitItem
When using a `jig.list` and any size widget larger than 1x1 the list will automatically be displayed without additional configurations. This is visible in this example.

In this example,  the list on the widget is the same as the `jig.list` once the widget has been accessed.

**Examples**:
See the complete example using static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/list-item/static-data/list-with-left-elements/list-with-left-checkbox-sd.jigx).
See the complete example using dynamic data in [GitHub]().

**Datasources**:
See the complete datasource for static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/services/repair-services-static.jigx).
See the complete datasource for dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/services/cleaning-services-dynamic.jigx)
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
## Automatic widget display because of list jig type (UI elements)

::::VerticalSplit{layout="left"}
:::VerticalSplitItem
![2x2 list with avatar](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/rinQmlbPzRXwTyKEcgBvq_listcompiphone13blueportrait.png "2x2 list with avatar")
:::

:::VerticalSplitItem
When using a `jig.list` and any size widget larger than 1x1 the list will automatically be displayed without additional configurations.

In this example, the list on the widget is exactly the same as the `jig.list` once the widget has been accessed.

**Examples**:
See the complete example using static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/components/list-item/static-data/list-with-left-elements/list-with-left-checkbox-sd.jigx).
See the complete example using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/components/list-item/dynamic-data/list-with-left-elements/list-with-left-avatar-dd.jigx).

**Datasources**:
See the complete datasource for static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/services/repair-services-static.jigx).
See the complete datasource for dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/services/cleaning-services-dynamic.jigx).
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
## List widget with stage component items

::::VerticalSplit{layout="left"}
:::VerticalSplitItem
![2 stage list widget](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/wLfGvJAdHpWNfCmBtm4ix_liststageiphone13blueportrait.png "2 stage list widget")
:::

:::VerticalSplitItem
This example is for list items that have a left and right element and shows a start-and-end. An example of this is flight schedules, however, this can be used for many different use cases as you can choose a different icon. Here a slightly different setup is used to that in the actual list to show you the widget configuration.

**Examples**:
See the complete example using static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/widgets/list/static-data/widget-list-stage-sd.jigx).
See the complete example using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/widgets/list/dynamic-data/widget-list-stage-dd.jigx).

**Datasources**:
See the complete datasource for static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/expanders%20and%20stages/flight-schedule-static.jigx).
See the complete datasource for dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/expanders%20and%20stages/flight-schedule-dynamic.jigx).
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
## List widget with product items

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/SmVasJ9L4i3NPUtt8l722_listproductiphone13blueportrait.png" size="80" position="center" caption="2x2 product-item list widget" alt="2x2 product-item list widget" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/SmVasJ9L4i3NPUtt8l722_listproductiphone13blueportrait.png" width="800" height="1493" darkWidth="800" darkHeight="1493"}
:::

:::VerticalSplitItem
This example shows product items with their images and respective prices.

**Examples**:
See the complete example using static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/widgets/list/static-data/widget-list-product-item-sd.jigx)
See the complete example using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/widgets/list/dynamic-data/widget-list-product-item-dd.jigx)

**Datasources**:
See the complete datasource for static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/products/products.jigx).
See the complete datasource for dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/products/products-dynamic.jigx).
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
## List widget with list items

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/rZCv7iRFImXiqOzMsjRK-_listsdiphone13blueportrait.png" size="76" position="center" caption="2x2 list-item basic widget" alt="2x2 list-item basic widget" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/rZCv7iRFImXiqOzMsjRK-_listsdiphone13blueportrait.png" width="800" height="1493" darkWidth="800" darkHeight="1493"}
:::

:::VerticalSplitItem
This example shows a basic `component.list-item` setup.

**Examples**:
See the complete example using static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/widgets/list/static-data/widget-list-items-sd.jigx).
See the complete example using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/widgets/list/dynamic-data/widget-list-items-dd.jigx).

**Datasources**:
See the complete datasource for static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/events-and-calendars/calendar-data.jigx).
See the complete datasource for dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/events-and-calendars/calendar-data-dynamic.jigx")
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
## Extended list widget 2x4, 4x2, 4x4

::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/s4ML69T6TZa5bCeOaYjKr_widget-extend.PNG" size="80" position="center" caption="Extended list widget" alt="Extended list widget" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/s4ML69T6TZa5bCeOaYjKr_widget-extend.PNG" width="800" height="785" darkWidth="800" darkHeight="785"}

This example shows how the `Extend List Widget` reuses the data from a single `jig.list` to customize the widget's appearance.  In the image above:

1. The first widget is the default `2x2` widget that is automatically displayed.
2. The second widget is a `2x4` using the `Extend List widget` to only show the `titles` in the list.
3. The third widget is a `4x2` using the `Extend List Widget `with a `component.stage` configuration.
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

## Group list widgets

See the following examples under groups:

- :Link[Group with chart and list]{href="https://docs.jigx.com/examples/group#utr1x" newTab="true"} (size: 4x4, split: horizontal)
- :Link[Group with chart and list]{href="https://docs.jigx.com/examples/group#Lk_2j" newTab="true"} (size: 4x4, split: vertical)
- :Link[Group with avatar and list]{href="https://docs.jigx.com/examples/group#3Wi36" newTab="true"} (size: 4x2)
- :Link[Group with value and bar-chart]{href="https://docs.jigx.com/examples/group#VWndb" newTab="true"} (size: 2x4)

## See also

- [State]()

