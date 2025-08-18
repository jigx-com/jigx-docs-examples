---
title: stage
slug: Cw5F-stage
createdAt: Thu Jun 09 2022 19:58:34 GMT+0000 (Coordinated Universal Time)
updatedAt: Thu Apr 24 2025 07:14:20 GMT+0000 (Coordinated Universal Time)
description: >-
  Learn how to use the "Stage" component to efficiently showcase content with
  left and right elements. This comprehensive document highlights the
  component's configuration options, such as customizing t
---

# stage

In this component, you add left and right elements, typically showing a start-and-end concept, such as flight schedules.

### Configuration options

Some properties are common to all components, see [Common component properties](docId:LLnTD-rxe8FmH7WpC5cZb) for a list and their configuration options.

| **Core structure** |                                                                   |
| ------------------ | ----------------------------------------------------------------- |
| `left`             | Add content to the `left` element as text, or use an expression.  |
| `right`            | Add content to the `right` element as text, or use an expression. |
| `title`            | Add `titles` for the text on the `left` and `right` elements.     |

| **Other options** |                                                                                                                                                                      |
| ----------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `icon`            | Add an icon to show in the `centerElement`. A list of icons is available. See [Jigx icons](https://docs.jigx.com/jigx-icons) for more information.                   |
| `style`           | `isWaitingSync` - Will display a "Waiting sync" indicator (cloud with a line through it), a visual indicator showing that data has not been synced to the cloud yet. |
| `subtitle`        | Add a `subtitle` to either the left or right element as text, or use an expression.                                                                                  |

| **Actions** |                                                                                                                                         |
| ----------- | --------------------------------------------------------------------------------------------------------------------------------------- |
| `onPress`   | The action is triggered while pressing on the content in the stage. Use IntelliSense (ctrl+space) to see the list of available actions. |

### Consideration

* `component.stage` can only be used in the `component.expander` or a [list](../list/stage.md).

### Examples and code snippets

:::::ExpandableHeading

#### Stage in expander

::::VerticalSplit{layout="left"} :::VerticalSplitItem ![Stage in expander](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/BQUOSOOooTNZSRT6fBCoU_dqf676mvwvyz4w1feir5qstageiphone13blueportrait.png) :::

:::VerticalSplitItem **Examples:**

See the full example using static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/stage/static-data/stage.jigx). See the full example using dynamic data [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/stage/dynamic-data/stage-dynamic.jigx). ::: ::::

:::CodeblockTabs stage (static)

```yaml
children:
  - type: component.expander
    options:
      header:
        centerElement:
          type: component.stage
          options:
            right:
              title: Boston
              subtitle: 11:30
            left:
              title: New York
              subtitle: 12:30
```

stage (dynamic)

```yaml
title: Stage
type: jig.default

children:
  - type: component.expander
    options:
      header:
        centerElement:
          type: component.stage
          options:
            right:
              title: =@ctx.datasources.trip-dynamic[3].from
              subtitle: =@ctx.datasources.trip-dynamic[3].board
            left:
              title: =@ctx.datasources.trip-dynamic[3].to
              subtitle: =@ctx.datasources.trip-dynamic[3].disembark
      children:
        - type: component.entity
          options:
            children:
              - type: component.entity-field
                options:
                  label: tbd
                  value: tbd
```

datasources (dynamic)

```yaml
datasources:
  trip-dynamic:
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_DYNAMIC
      entities:
        - entity: default/flight-schedule
      query: |
        SELECT 
          id, 
          '$.airline', 
          '$.board', 
          '$.disembark', 
          '$.date', 
          '$.flight', 
          '$.from', 
          '$.fromabrv', 
          '$.gate', 
          '$.name', 
          '$.seat', 
          '$.to', 
          '$.toabrv' 
        FROM [default/flight-schedule]
```

::: :::::

:::::ExpandableHeading

#### Stage in list

::::VerticalSplit{layout="left"} :::VerticalSplitItem ![Stage in list](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/8oR-ecX43O27thnShsgId_mlmkhpfrzwatv8spkkz7vstageiphone13blueportrait.png) :::

:::VerticalSplitItem **Examples:**

See the full example using static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/stage/static-data/stage-list.jigx). See the full example using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/stage/dynamic-data/stage-list-dynamic.jigx).

**Datasources:**

See the full datasource for static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/examples/trip-static.jigx). See the full datasource for dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/adhoc-components/trip-dynamic.jigx). ::: ::::

:::CodeblockTabs stage-list (static)

```yaml
title: Trip in list
type: jig.list

data: =@ctx.datasources.trip-static
item:
  type: component.stage
  options:
    right:
      title: =@ctx.current.item.to
      subtitle: =@ctx.current.item.time-to
    left:
      title: =@ctx.current.item.from
      subtitle: =@ctx.current.item.time-from
```

stage-list (dynamic)

```yaml
title: Stage in list
type: jig.list

data: =@ctx.datasources.trip-dynamic
item:
  type: component.stage
  options:
    right:
      title: =@ctx.current.item.from
      subtitle: =@ctx.current.item.board
    left:
      title: =@ctx.current.item.to
      subtitle: =@ctx.current.item.disembark
```

datasources (static)

```yaml
datasources:
  trip-static:
    type: datasource.static
    options:
      data:
        - id: 1
          from: Boston
          time-from: 11:30
          to: New York
          time-to: 12:30
        - id: 1
          from: Las Vegas
          time-from: 09:45
          to: London
          time-to: 19:00
        - id: 1
          from: Paris
          time-from: 13:15
          to: Prague
          time-to: 17:30
```

datasources (dynamic)

```yaml
datasources:
  trip-dynamic:
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_DYNAMIC
      entities:
        - entity: default/flight-schedule
      query: |
        SELECT 
          id, 
          '$.airline', 
          '$.board', 
          '$.disembark', 
          '$.date', 
          '$.flight', 
          '$.from', 
          '$.fromabrv', 
          '$.gate', 
          '$.name', 
          '$.seat', 
          '$.to', 
          '$.toabrv' 
        FROM [default/flight-schedule]
```

::: :::::
