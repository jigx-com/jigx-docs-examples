---
title: titles
slug: YU2a-titles
description: Learn how to use the titles component in Jigx widgets to display titles, subtitles, and comments. This document covers the available widgets, configuration options, and includes examples and code snippets for integrating the titles component in the image 
createdAt: Thu Jun 09 2022 19:55:14 GMT+0000 (Coordinated Universal Time)
updatedAt: Fri Mar 07 2025 14:09:31 GMT+0000 (Coordinated Universal Time)
---

This component displays a title, subtitle, comment, or any type of text content. As the titles component is always part of a widget, this text will be displayed on the widget.

Titles are available in the following content widgets:

- <a href="https://docs.jigx.com/examples/I4a9-avatar" target="_blank">avatar</a>
- <a href="https://docs.jigx.com/examples/chart" target="_blank">chart</a>
- <a href="https://docs.jigx.com/examples/XtQx-image" target="_blank">image</a>
- <a href="https://docs.jigx.com/examples/zOQa-location" target="_blank">location</a>
- <a href="https://docs.jigx.com/examples/status" target="_blank">status</a>
- <a href="https://docs.jigx.com/examples/value" target="_blank">value</a>

## Configuration options

| ### Core structure | ****                                    |
| ------------------ | --------------------------------------- |
| `title`            | Display the text content for the title. |
| `subtitle`         | Add a subtitle under the title text.    |

| ### Other options |                                                                                                                                            |
| ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------ |
| `align`           | `center`, `left`, `right`                                                                                                                  |
| `icon`            | icon used in the widget.                                                                                                                   |
| `iconColor`       | Sets the icon's color. Choose a color from the provided palette. If the property is not specified in the YAML, the default color is black. |
| `style`           | Properties used for component styling.                                                                                                     |

## Examples and code snippets

:::::ExpandableHeading
### Titles in the image widget

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/qzUhfHOAIhwl4ruMOw20K_title-imgiphone13blueportrait.png" size="78" position="center" caption="Image widget with titles" alt="Image widget with titles"}
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
    FROM [default/location] WHERE '$.category' = "titles"
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
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/ShMgsX1bPDxAhXNfPFuo1_title-locationiphone13blueportrait.png" size="80" position="center" caption="Location widget with titles" alt="Location widget with titles"}
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
titles-location (static)

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

titles-location (dynamic)

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

