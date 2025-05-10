---
title: jig.fullscreen
slug: yTA--ji
createdAt: Thu Nov 30 2023 05:46:40 GMT+0000 (Coordinated Universal Time)
updatedAt: Tue Apr 29 2025 10:39:47 GMT+0000 (Coordinated Universal Time)
---

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
The `jig.full-screen` allows you to configure a component that covers the entire screen of the jig with no other elements visible. This is useful for creating a full screen of a [location](./../Components/location.md) screen.


:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-sMnc2OSlftv__5xUbT0lS-20250221-132107.png" size="74" position="center" caption="Location in full screen" alt="Location in full screen"}
:::
::::

## Considerations

- This jig type does not allow for a `description` or `header` properties.
- The [location](./../Components/location.md) component can be used in the `jig.full-screen`.
- When using an action within the jig, check that the action button does not overlap the fullscreen functionality. The best practice is not to use an action with the full-screen jig, as the action button covers elements shown in the full-screen.
- It is not recommended to use a full-screen jig in a [composite](./jig_composite.md) jig, combining the fullscreen with another jig will not provide the optimal layout for the jig.

## Configuration options

Some properties are common to all jig types, see [Common jig type properties](docId\:AvbKAkPpRDHkZ8I8iSTkF) for a list and their configuration options.

The `jig.full-screen` can be configured in the following way in Jigx Builder.

| **Core structure** |                                                                                                                                                                                  |
| ------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `component`        |  Select the component to display as a full-screen, the available components are:<br />* `component.chat`<br />* `component.custom-component`<br />* `component.location`<br />* `component.web-view` |
| `title`            | Give the jig a title that is displayed at the top of the screen. If you do not want to show a title in a jig use `title: ' '`.                                                        |
| `type`             | Select `jig.full-screen`                                                          |

## Examples and code snippets 

:::ExpandableHeading
### Full-screen of a map
:::

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-sMnc2OSlftv__5xUbT0lS-20250221-132107.png" size="80" position="center" caption="Location in full screen" alt="Location in full screen"}
:::

:::VerticalSplitItem
In this example the location to the Seattle Aquarium is shown in full screen using jigtype `jig.full-screen`, `component.location` and Dynamic Data datasource called address.

Refer to the [location](./../Components/location.md) component for additional location setup options.

**Examples:**
See the full code sample using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jig-types/jig-fullscreen/fullscreen-location-dd.jigx).
:::
::::

:::CodeblockTabs
location-fullscreen-dynamic.jigx

```yaml
title: Aquarium Location 
type: jig.full-screen

component: 
  type: component.location
  options: 
    viewPoint:
      address: 1483 Alaskan Way, Seattle, US
      zoomLevel: 15
    markers:
      data: =@ctx.datasources.address
      item:
        type: component.marker-item
        options:
          address: 1483 Alaskan Way, Seattle, US
          children:
            type: component.icon
            options:
              size: medium
              color: negative
              icon: end-marker  
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
      '$.address',
      '$.address-us',
      '$.category',  
      '$.lat',
      '$.lng',
      '$.city',
      '$.country',
      '$.street'
    FROM [default/location] WHERE '$.category' = "location"
```
:::

### Chatbot in a full-screen jig

See the [chatbot with OpenAI](./../Components/chat.md) example.

## See Also

- [Jigs (screens)]()
- [location](./../Components/location.md)

