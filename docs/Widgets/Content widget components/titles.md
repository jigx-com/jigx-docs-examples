# titles

This component displays a title, subtitle, comment, or any type of text content. As the titles component is always part of a widget, this text will be displayed on the widget.

Titles are available in the following content widgets:

* [avatar](../avatar.md)
* [chart](../chart.md)
* [image](../image.md)
* [location](../location.md)
* [status](../status.md)
* [value](../value.md)

## Configuration options

<table><thead><tr><th width="133.9375">Core structure</th><th></th></tr></thead><tbody><tr><td><code>title</code></td><td>Display the text content for the title.</td></tr><tr><td><code>subtitle</code></td><td>Add a subtitle under the title text.</td></tr></tbody></table>

<table><thead><tr><th width="136.79296875">Other options</th><th></th></tr></thead><tbody><tr><td><code>align</code></td><td><code>center</code>, <code>left</code>, <code>right</code></td></tr><tr><td><code>icon</code></td><td>icon used in the widget.</td></tr><tr><td><code>iconColor</code></td><td>Sets the icon's color. Choose a color from the provided palette. If the property is not specified in the YAML, the default color is black.</td></tr><tr><td><code>style</code></td><td>Properties used for component styling.</td></tr></tbody></table>

## Examples and code snippets

### Titles in the image widget

{% columns %}
{% column %}
Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/qzUhfHOAIhwl4ruMOw20K\_title-imgiphone13blueportrait.png" size="78" position="center" caption="Image widget with titles" alt="Image widget with titles" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/qzUhfHOAIhwl4ruMOw20K\_title-imgiphone13blueportrait.png" width="800" height="1493" darkWidth="800" darkHeight="1493"}
{% endcolumn %}

{% column %}
A descriptive title added to the image widget.

**Examples:**

See the full example using static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/titles/static-data/titles-widget-image/titles-widget-image.jigx) See the full example using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/titles/dynamic-data/titles-widget-image/titles-widget-image-dynamic.jigx).

**Datasource**: See the full datasource for static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/adhoc-components/titles-static.jigx) See the full datasource for dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/adhoc-components/titles.jigx).
{% endcolumn %}
{% endcolumns %}

{% tabs %}
{% tab title="titles-widget (static)" %}
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
{% endtab %}

{% tab title="title-widget (dynamic)" %}
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
{% endtab %}

{% tab title="datasource (static)" %}
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
{% endtab %}

{% tab title="datasource (dynamic)" %}
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
{% endtab %}

{% tab title="grid-item" %}
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
{% endtab %}
{% endtabs %}

### Titles in the location widget

{% columns %}
{% column %}
Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/ShMgsX1bPDxAhXNfPFuo1\_title-locationiphone13blueportrait.png" size="80" position="center" caption="Location widget with titles" alt="Location widget with titles" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/ShMgsX1bPDxAhXNfPFuo1\_title-locationiphone13blueportrait.png" width="800" height="1493" darkWidth="800" darkHeight="1493"}&#x20;
{% endcolumn %}

{% column %}
The title/description of the place displayed on the location widget.

**Examples**: See the full example using static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/titles/static-data/titles-widget-location/titles-widget-location.jigx). See the full example using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/titles/dynamic-data/titles-widget-location/titles-widget-location-dynamic.jigx).

**Datasource**: See the full datasource for static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/adhoc-components/titles-static.jigx). See the full datasource for dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/adhoc-components/titles.jigx).
{% endcolumn %}
{% endcolumns %}

{% tabs %}
{% tab title="titles-widget-location.jigx" %}
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
{% endtab %}

{% tab title="titles-widget-location-dd.jigx" %}
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
{% endtab %}

{% tab title="grid-item" %}
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
{% endtab %}
{% endtabs %}
