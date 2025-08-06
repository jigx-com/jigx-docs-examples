# avatar

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
The avatar widget can be used as a unique visual identifier, for example, to display a profile photo, company logo, initials, or flags. Additionally, text or a description can be added. The avatar can be used alone or combined with another widget inside a [widget/group](https://docs.jigx.com/examples/group).
:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/dfGetxkAlt3Vcv55GBnnm_wd-avatar.PNG" size="70" position="center" caption="Avatar widgets" alt="Avatar widgets" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/dfGetxkAlt3Vcv55GBnnm_wd-avatar.PNG" width="800" height="1613" darkWidth="800" darkHeight="1613"}
:::
::::

## Configuration options

<table isTableHeaderOn="true" selectedColumns="" selectedRows="" selectedTable="false" columnWidths="130">
  <tr>
    <td selected="false" align="left">
      <p><strong>Core structure</strong></p>
    </td>
    <td selected="false" align="left">
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>text</code></p>
    </td>
    <td selected="false" align="left">
      <p>Display text content on the widget surface when the URI is empty, for example, initials.</p>
    </td>
  </tr>
</table>

<table isTableHeaderOn="true" selectedColumns="" selectedRows="" selectedTable="false" columnWidths="137">
  <tr>
    <td selected="false" align="left">
      <p><strong>Other options</strong></p>
    </td>
    <td selected="false" align="left">
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>bottom</code></p>
    </td>
    <td selected="false" align="left">
      <p>The  component will be added to the bottom of the widget.</p>
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
      <p>The  component will be added to the top of the widget.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>uri</code></p>
    </td>
    <td selected="false" align="left">
      <p>Provide the <code>uri</code> for the image. The following can be used: </p>
      <ul>
      <li>https//: <em>imagesource</em></li>
      <li>image from a datasource referenced in an expression</li>
      </ul>
    </td>
  </tr>
</table>

## Examples and code snippets

:::::ExpandableHeading
### Avatar widget example

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/2zMUlETjxsJBNeE0fHc0e_avatariphone13blueportrait.png" size="80" position="center" caption="Avatar widget" alt="Avatar widget" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/2zMUlETjxsJBNeE0fHc0e_avatariphone13blueportrait.png" width="800" height="1493" darkWidth="800" darkHeight="1493"}
:::

:::VerticalSplitItem
This is a simple example of using the avatar widget to show a quick overview of the next meeting.

**Examples**:
See the complete example using static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/widgets/avatar/static-data/avatar-on-widget/avatar-on-widget.jigx).
See the complete example using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/widgets/avatar/dynamic-data/avatar-on-widget/avatar-on-widget-dynamic.jigx).

**Datasources**:
See the complete datasource for static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/examples/static-global.jigx).
See the complete datasource for dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/examples/dynamic-global.jigx).
:::
::::

:::CodeblockTabs
avatar-widget (static)

```yaml
widgets:    
  avatar-widget:
    type: widget.avatar
    options:
      text: =$substring($substringBefore(@ctx.datasources.static-global.name, " "), 0, 1) & $substring($substringAfter(@ctx.datasources.static-global.name, " "), 0, 1)
      uri: =@ctx.datasources.static-global.picture
      bottom: 
        type: component.titles
        options:
          align: center
          title: =@ctx.datasources.static-global.name
          subtitle: =$fromMillis($toMillis(@ctx.datasources.static-global.date_from),'[H01]:[m01]') & '-' & $fromMillis($toMillis(@ctx.datasources.static-global.date_to),'[H01]:[m01]')
```

avatar-widget (dynamic)

```yaml
widgets:    
  avatar-meeting:
    type: widget.avatar
    options:
      text: =$substring($substringBefore(@ctx.datasources.dynamic-global.name, " "), 0, 1) & $substring($substringAfter(@ctx.datasources.dynamic-global.name, " "), 0, 1)
      uri: =@ctx.datasources.dynamic-global.picture
      bottom: 
        type: component.titles
        options:
          align: center
          title: =@ctx.datasources.dynamic-global.name
          subtitle: =$fromMillis($toMillis(@ctx.datasources.dynamic-global.date-from),'[H01]:[m01]') & '-' & $fromMillis($toMillis(@ctx.datasources.dynamic-global.date-to),'[H01]:[m01]')

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
          jigId: avatar-widget
          widgetId: avatar-widget
```
:::
:::::

:::::ExpandableHeading
### Avatar widget with title

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
This is example shows the avatar widget using the `component.title` to add a name and icon to the widget.

**Examples**:
See the complete example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/widgets/2x2/avatar-2_2x2.jigx).
:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/_U1nDQMrehHQwSgcfmuRF_wd-avatartitle.PNG" size="74" position="center" caption="Avatar widget with title" alt="Avatar widget with title" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/_U1nDQMrehHQwSgcfmuRF_wd-avatartitle.PNG" width="800" height="1613" darkWidth="800" darkHeight="1613"}
:::
::::

:::CodeblockTabs
avatar-2\_2x2.jigx

```yaml
widgets:
  avatar2-2x2:
    type: widget.avatar
    options:
      text: MR
      uri: https://randomuser.me/api/portraits/men/20.jpg
      bottom:
        type: component.titles
        options:
          title: Marty Randolph
          subtitle: Product Design Lead
          align: center
          icon: calendar                  
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
          jigId: avatar-2_2x2
          widgetId: avatar2-2x2
```
:::
:::::

:::::ExpandableHeading
### Avatar widget/group with list

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/BQMj-dwf5_KkhMH4AMvys_avatargroupiphone13blueportrait.png" size="80" position="center" caption="Avatar in a group widget" alt="Avatar in a group widget" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/BQMj-dwf5_KkhMH4AMvys_avatargroupiphone13blueportrait.png" width="800" height="1493" darkWidth="800" darkHeight="1493"}
:::

:::VerticalSplitItem
Here is the avatar widget associated with the list widget inside the group widget. The next patient is displayed as an avatar and the next three patients are on the list for a better overview.

**Examples**:
See the complete example using static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/widgets/avatar/static-data/avatar-on-group-widget/avatar-on-group-widget.jigx)
See the complete example using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/widgets/avatar/dynamic-data/avatar-on-group-widget/avatar-on-group-widget-dynamic.jigx)

**Datasources**:
Full datasource for static data for [avatar widget](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/examples/static-global.jigx) and for the [list widget](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/examples/static-global-multiple.jigx) in GitHub.
Full datasource for dynamic data for avatar [widget](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/employees/employees-dynamic.jigx) and for the [list widget](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/employees/employees-dynamic.jigx) in GitHub.
:::
::::

:::CodeblockTabs
avatar-group (static)

```yaml
wwidgets:
  patientStatic-4x2:
    type: widget.group
    options:
      children:
        - type: widget.avatar
          options:
            text: =$substring($substringBefore(@ctx.datasources.static-global.name, " "), 0, 1) & $substring($substringAfter(@ctx.datasources.static-global.name, " "), 0, 1)
            uri: =@ctx.datasources.static-global.picture
        - type: widget.list
          options:
            data: =@ctx.datasources.static-global-multiple
            item:
              type: component.list-item
              options:
                title: =@ctx.current.item.name
                subtitle: =$fromMillis($toMillis(@ctx.current.item.date_from),'[H01]:[m01]') & '-' & $fromMillis($toMillis(@ctx.current.item.date_to),'[H01]:[m01]')
                leftElement:
                  element: avatar
                  text: =$substring($substringBefore(@ctx.current.item.name, " "), 0, 1) & $substring($substringAfter(@ctx.current.item.name, " "), 0, 1)
                  uri: =@ctx.current.item.picture
```

avatar-group (dynamic)&#x20;

```yaml
widgets:
  patientDD-4x2:
    type: widget.group
    options:
      children:
        - type: widget.avatar
          options:
            text: =$substring($substringBefore(@ctx.datasources.dynamic-global.name, " "), 0, 1) & $substring($substringAfter(@ctx.datasources.dynamic-global.name, " "), 0, 1)
            uri: =@ctx.datasources.dynamic-global.picture
        - type: widget.list
          options:
            data: =@ctx.datasources.employees-dynamic
            item:
              type: component.list-item
              options:
                title: =@ctx.current.item.firstname & ' ' & @ctx.current.item.lastname
                subtitle: =$fromMillis($toMillis(@ctx.current.item.date_from),'[H01]:[m01]') & '-' & $fromMillis($toMillis(@ctx.current.item.date_to),'[H01]:[m01]')
                leftElement:
                  element: avatar
                  text: =$substring(@ctx.current.item.firstname, 0, 1) & =$substring(@ctx.current.item.lastname, 0, 1)
                  uri: =@ctx.current.item.photo
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
          jigId: avatar-group
          widgetId: patientStatic-4x2
```
:::
:::::

:::::ExpandableHeading
### Avatar widget/group with title and list

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
In this example the avatar widget is combined with the list widget inside the group widget. The avatar widget has a `component.title` configured at the `top` to show a time and `bottom` to add a `title` and `subtitle` to the avatar widget.

**Examples**:
See the complete example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/widgets/4x4/combined-avatar-list-1_4x4.jigx).
:::

:::VerticalSplitItem
::Image[]{src="https://archbee-doc-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-52t4bV7-5EmSZicDP_BNb-20240808-080947.PNG" size="74" position="center" caption="Avatar widget in group widget" alt="Avatar widget in group widget" signedSrc="https://archbee-doc-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-52t4bV7-5EmSZicDP_BNb-20240808-080947.PNG" width="1240" height="2500" darkWidth="1240" darkHeight="2500"}
:::
::::

:::CodeblockTabs
combined-avatar-list-1\_4x4.jigx

```yaml
widgets:
  combined-avatar-list1-4x4: 
    type: widget.group
    options:
      children:            
        - type: widget.avatar
          options:
            text: LS
            uri: https://i.pravatar.cc/400?img=59
            bottom:
              type: component.titles
              options:
                align: center
                title: Leo Siphron
                subtitle: Inter B

            top:
              type: component.titles
              options:
                icon: time-clock-circle
                iconColor: negative
                align: center
                title: 08:30 - 19:00
                subtitle: Today
                style:
                  isNegative: true
                
        - type: widget.list
          options:
            data: =@ctx.datasources.components
            item: 
              type: component.list-item
              options:
                title:  =@ctx.current.item.name
                subtitle: =@ctx.current.item.subtitle
                leftElement: 
                  element: avatar
                  text: =@ctx.current.item.avatar-text
                  uri: =@ctx.current.item.avatar-uri                
```

datasource

```yaml
datasources:
  components:
    type: datasource.static
    options:
      data:
        - name: John Smith
          subtitle: 09:00 - 10:00
          from: 01/10/2024 09:00
          to: 01/10/2022 10:00
          avatar-text: JS
          avatar-uri:  https://images.unsplash.com/photo-1645378999496-33c8c2afe38d?q=80&w=2970&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D   
        
        - name: Laurenz Amram
          subtitle: 12:30 - 14:00
          from: 01/10/2024 12:30
          to: 14:00
          avatar-text: LA
          avatar-uri: https://i.pravatar.cc/400?img=45
        
        - name: Ladislao Børge
          subtitle: 16:00 - 17:00
          from: 01/10/2024 16:00
          to: 01/10/2022 17:00
          avatar-text: LB
          avatar-uri: 
```

grid-item

```yaml
# Grid-item for the jig.
children:
  - type: component.grid-item
    options:
      size: "2x2"
      children: 
        type: component.jig-widget
        options:
          jigId: combined-avatar-list-1_4x4
          widgetId: combined-avatar-list1-4x4
```
:::
:::::

