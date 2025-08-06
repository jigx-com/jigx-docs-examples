# titles

This component displays a title, subtitle, comment, or any type of text content. As the titles component is always part of a widget, this text will be displayed on the widget.

Titles are available in the following content widgets:

- [avatar](./../avatar.md)&#x20;
- [chart](./../chart.md)&#x20;
- [image](./../image.md)&#x20;
- [location](./../location.md)&#x20;
- [status](./../status.md)&#x20;
- [value](./../value.md)&#x20;

## Configuration options

<table isTableHeaderOn="true" selectedColumns="" selectedRows="" selectedTable="false" columnWidths="142">
  <tr>
    <td selected="false" align="left">
      <p><strong>Core structure</strong></p>
    </td>
    <td selected="false" align="left">
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>title</code></p>
    </td>
    <td selected="false" align="left">
      <p>Display the text content for the title.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>subtitle</code></p>
    </td>
    <td selected="false" align="left">
      <p>Add a subtitle under the title text.</p>
    </td>
  </tr>
</table>

<table isTableHeaderOn="true" selectedColumns="" selectedRows="" selectedTable="false" columnWidths="135">
  <tr>
    <td selected="false" align="left">
      <p><strong>Other options</strong></p>
    </td>
    <td selected="false" align="left">
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>align</code></p>
    </td>
    <td selected="false" align="left">
      <p><code>center</code>, <code>left</code>, <code>right</code></p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>icon</code></p>
    </td>
    <td selected="false" align="left">
      <p>icon used in the widget.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>iconColor</code></p>
    </td>
    <td selected="false" align="left">
      <p>Sets the icon's color. Choose a color from the provided palette. If the property is not specified in the YAML, the default color is black.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>style</code></p>
    </td>
    <td selected="false" align="left">
      <p>Properties used for component styling.</p>
    </td>
  </tr>
</table>

## Examples and code snippets

:::::ExpandableHeading
### Titles in the image widget

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/qzUhfHOAIhwl4ruMOw20K_title-imgiphone13blueportrait.png" size="78" position="center" caption="Image widget with titles" alt="Image widget with titles" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/qzUhfHOAIhwl4ruMOw20K_title-imgiphone13blueportrait.png" width="800" height="1493" darkWidth="800" darkHeight="1493"}
:::

:::VerticalSplitItem
A descriptive title added to the image widget.

**Examples:**

See the full example using static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/titles/static-data/titles-widget-image/titles-widget-image.jigx)
See the full example using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/titles/dynamic-data/titles-widget-image/titles-widget-image-dynamic.jigx).

**Datasource**:
See the full datasource for static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/adhoc-components/titles-static.jigx)
See the full datasource for dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/adhoc-components/titles.jigx).
:::
::::

:::CodeblockTabs
titles-widget (static)

```yaml
widgets:
  image-title:
    type: widget.image
    options:
      isContentOverlaid: true
      source:
        uri: =@ctx.datasources.titles-static.image
      bottom:
        type: component.titles
        options:
          align: center
          title: =@ctx.datasources.titles-static.title
```

title-widget (dynamic)

```yaml
widgets:
  image-title-dd:
    type: widget.image
    options:
      isContentOverlaid: true
      source:
        uri: =@ctx.datasources.titles.image
      bottom:
        type: component.titles
        options:
          align: center
          title: =@ctx.datasources.titles.title
```

datasource (static)

```yaml
type: datasource.static
options:
  data:
    - address: Národní 135/14, 110 00 Praha
      image: https://images.unsplash.com/photo-1472289065668-ce650ac443d2?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1738&q=80
      locationSubtitle: Prague Czech Republic
      locationTitle: Co-working space
      title: Work productivity
```

datasource (dynamic)

```yaml
type: datasource.sqlite
options:
  provider: DATA_PROVIDER_DYNAMIC
  entities:
    - entity: default/location
  query: |
    SELECT
      '$.id',
      '$.title',
      '$.image',
      '$.address',
      '$.locationtitle',
      '$.locationsubtitle',
      '$.category'
    FROM [default/location] 
    WHERE '$.category' = "titles"
```

grid-item

```yaml
# Grid-item for the static jig.
children:
  - type: component.grid-item
    options:
      size: "4x4"
      children: 
        type: component.jig-widget
        options:
          jigId: titles-widget-image
          widgetId: image-title
```
:::
:::::

:::::ExpandableHeading
### Titles in the location widget

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/ShMgsX1bPDxAhXNfPFuo1_title-locationiphone13blueportrait.png" size="80" position="center" caption="Location widget with titles" alt="Location widget with titles" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/ShMgsX1bPDxAhXNfPFuo1_title-locationiphone13blueportrait.png" width="800" height="1493" darkWidth="800" darkHeight="1493"}
:::

:::VerticalSplitItem
The title/description of the place displayed on the location widget.

**Examples**:
See the full example using static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/titles/static-data/titles-widget-location/titles-widget-location.jigx).
See the full example using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/titles/dynamic-data/titles-widget-location/titles-widget-location-dynamic.jigx).

**Datasource**:
See the full datasource for static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/adhoc-components/titles-static.jigx).
See the full datasource for dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/adhoc-components/titles.jigx).
:::
::::

:::CodeblockTabs
titles-widget-location.jigx

```yaml
widgets:
  location-title-s:
    type: widget.location
    options:
      viewPoint:  
       address: =@ctx.datasources.titles-static.address
      bottom:
        type: component.titles
        options:
          title: =@ctx.datasources.titles-static.locationTitle
          subtitle: =@ctx.datasources.titles-static.locationSubtitle
          align: left
```

titles-widget-location-dd.jigx

```yaml
widgets:
  location-titles-dd:
    type: widget.location
    options:
      viewPoint:
        address: =@ctx.datasources.titles.address
      bottom:
        type: component.titles
        options:
          title: =@ctx.datasources.titles.locationtitle
          subtitle: =@ctx.datasources.titles.locationsubtitle
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
          jigId: titles-widget-image
          widgetId: image-title
```
:::
:::::

