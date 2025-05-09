---
title: stage
slug: _6vp-stage
description: Learn how to implement a versatile component for items with left and right elements. This document offers customization options for icons and actions, along with practical code snippets and examples. Discover how to integrate the component with both stati
createdAt: Thu Jun 09 2022 19:58:34 GMT+0000 (Coordinated Universal Time)
updatedAt: Mon Aug 05 2024 13:21:50 GMT+0000 (Coordinated Universal Time)
---

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
A stage is a primary container for displaying various UI components on the left and right, typically showing a start-and-end concept.


:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/yWymE6Po4TH-JLyB7xKK2_cc-list-stage.png" size="88" position="center" caption="Stage in a list" alt="Stage in a list"}
:::
::::

## Configuration options

Some properties are common to all components, see [Common component properties](docId\:LLnTD-rxe8FmH7WpC5cZb) for a list and their configuration options.

| **Core structure** |                                                               |
| ------------------ | ----------------------------------------------------------------- |
| `left`             | Add content to the `left` element as text, or use an expression.  |
| `right`            | Add content to the `right` element as text, or use an expression. |
| `title`            | Add `titles` for the text on the `left` and `right` elements.     |

|**Other options** |                                              |
| ----------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `icon`            | Add an icon to show in the `centerElement`. A list of icons is available. See [Jigx icons]() for more information.                                                   |
| `style`           | `isWaitingSync` - Will display a "Waiting sync" indicator (cloud with a line through it), a visual indicator showing that data has not been synced to the cloud yet. |
| `subtitle`        | Add a `subtitle` to either the left or right element as text, or use an expression.                                                                                  |

| **Actions** |          |
| ----------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| `onPress`   | The action is triggered while pressing on an item in the stage. Use IntelliSense (ctrl+space) to see the list of available actions.  |

## Consideration

- `component.stage` can only be used in the `component.list` or an [expander](./../expander.md).

## Examples and code snippets

:::::ExpandableHeading
### List with stage

::::VerticalSplit{layout="left"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/RjT9ffFl39FHcgn4CQhU4_n-v2bpok86ynufyojh-jvlist-default-jig-with-stage-listiphone13blueportrait.png" size="80"  position="center" caption="Stage for flights" alt="Stage for flights"}
:::

:::VerticalSplitItem
This example shows list items with left and right elements and typically shows a start-and-end concept. Flight schedules are used in this example. However, you can choose a different icon for many different use cases.

**Examples:**
See the full example using static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/list/static-data/default-w-stage-list-sd.jigx).
See the full example using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/list/dynamic-data/default-w-stage-list-dd.jigx).

**Datasource:**
See the full datasource for static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/expanders%20and%20stages/flight-schedule-static.jigx).
See the full datasource for dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/expanders%20and%20stages/flight-schedule-dynamic.jigx).
:::
::::

:::CodeblockTabs
default-w-stage-list (static)

```yaml
children:
  - type: component.entity
    options:
      children:
        - type: component.entity-field
          options:
            label: Current User
            value: =@ctx.user.displayName
  - type: component.list
    options:
      data: =@ctx.datasources.flight-schedule-static
      item: 
        type: component.stage
        options:
          icon: plane-1
          right:
            title: =@ctx.current.item.toabrv
            subtitle: =@ctx.current.item.board
          left:
            title: =@ctx.current.item.fromabrv
            subtitle: =@ctx.current.item.disembark
```

default-w-stage-list (dynamic)

```yaml
children:
  - type: component.entity
    options:
      children:
        - type: component.entity-field
          options:
            label: Current User
            value: =@ctx.user.displayName
  - type: component.list
    options:
      data: =@ctx.datasources.flight-schedule-dynamic
      item: 
        type: component.stage
        options:
          icon: plane-1
          right:
            title: =@ctx.current.item.toabrv
            subtitle: =@ctx.current.item.board
          left:
            title: =@ctx.current.item.fromabrv
            subtitle: =@ctx.current.item.disembark
```

datasources (static)

```yaml
datasources:
  flight-schedule-static:
    type: datasource.static
    options:
      data: 
        - id: 1
          airline: Get Stuff Done Airlines
          board: 11:30
          disembark: 12:30
          date: 30 Jul
          flight: A 0123
          from: Hawaii
          fromabrv: HNL
          gate: 16
          name: July Nelson
          seat: 12F
          to: New York
          toabrv: JFK
          image: https://images.unsplash.com/photo-1436491865332-7a61a109cc05?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxzZWFyY2h8MXx8cGxhbmV8ZW58MHx8MHx8&auto=format&fit=crop&w=500&q=60
        - id: 2
          airline: Get Stuff Done Airlines
          board: 08:10
          disembark: 10:45
          date: 30 Jul
          flight: A 5738
          from: Phoenix
          fromabrv: PHX
          gate: 2
          name: Nora Gordon
          seat: 27A
          to: Alabama
          toabrv: MCZ
          image: https://images.unsplash.com/photo-1464037866556-6812c9d1c72e?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxzZWFyY2h8Nnx8cGxhbmV8ZW58MHx8MHx8&auto=format&fit=crop&w=500&q=60
        - id: 3
          airline: Get Stuff Done Airlines
          board: 14:00
          disembark: 19:59
          date: 30 Jul
          flight: A 1123
          from: Iowa
          fromabrv: DSM
          gate: 15
          name: Tracy Matthews
          seat: 13F
          to: Ohio
          toabrv: DAY
          image: https://images.unsplash.com/photo-1488085061387-422e29b40080?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxzZWFyY2h8MTN8fHBsYW5lfGVufDB8fDB8fA%3D%3D&auto=format&fit=crop&w=500&q=60
```

datasources (dynamic)

```yaml
datasources:
  flight-schedule-dynamic:
    type: 'datasource.sqlite'
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
:::
:::::

:::::ExpandableHeading
### List with expander and stage as a Header

::::VerticalSplit{layout="left"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/rHih_dHdqqMASbcxefEw-_rxx3cpwfsmgibkcygpxznlist-with-expander.png" size="80"  position="center" caption="Stage in list with expanders" alt="Stage in list with expanders"}
:::

:::VerticalSplitItem
This example shows a list of expanders that have used the stage components as their header elements.

Expanders are ideal for displaying additional information without having to navigate to another page.

**Examples:**
See the full example using static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/list/static-data/default-w-exp-stage-list-sd.jigx).
See the full example using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/list/dynamic-data/default-w-exp-stage-list-dd.jigx).

**Datasource:**
See the full datasource for static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/expanders%20and%20stages/flight-schedule-static.jigx).
See the full datasource for dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/expanders%20and%20stages/flight-schedule-dynamic.jigx).
:::
::::

:::CodeblockTabs
list-expander (static)

```yaml
children:
  - type: component.entity
    options:
      children:
        - type: component.entity-field
          options:
            label: Current User
            value: =@ctx.user.displayName
  - type: component.list
    options:
      data: =@ctx.datasources.flight-schedule-static
      item: 
        type: component.expander
        options:
          header:
            centerElement: 
              type: component.stage
              options:
                right:
                  title: =@ctx.current.item.toabrv
                  subtitle: =@ctx.current.item.board
                left:
                  title: =@ctx.current.item.fromabrv
                  subtitle: =@ctx.current.item.disembark
          children:
            - type: component.entity
              options:
                children:
                  - type: component.field-row
                    options:
                      children:
                        - type: component.entity-field
                          options:
                            label: Boarding
                            value: =@ctx.current.item.from
                        - type: component.entity-field
                          options:
                            label: Destination
                            value: =@ctx.current.item.disembark
                  - type: component.field-row
                    options:
                      children:
                        - type: component.entity-field
                          options:
                            label: Board Time
                            value: =@ctx.current.item.board
                        - type: component.entity-field
                          options:
                            label: Disembark Time
                            value: =@ctx.current.item.disembark
                  - type: component.entity-field
                    options:
                      label: Passenger
                      value: =@ctx.current.item.name
                  - type: component.field-row
                    options:
                      children:
                        - type: component.entity-field
                          options:
                            label: Flight
                            value: =@ctx.current.item.flight
                        - type: component.entity-field
                          options:
                            label: Gate
                            value: =@ctx.current.item.gate
                        - type: component.entity-field
                          options:
                            label: Seat
                            value: =@ctx.current.item.seat
            - type: component.location
              options:
                address: =@ctx.current.item.to
```

list-expander (dynamic)

```yaml
children:
  - type: component.entity
    options:
      children:
        - type: component.entity-field
          options:
            label: Current User
            value: =@ctx.user.displayName
  - type: component.list
    options:
      data: =@ctx.datasources.flight-schedule-dynamic
      item: 
        type: component.expander
        options:
          header:
            centerElement: 
              type: component.stage
              options:
                right:
                  title: =@ctx.current.item.toabrv
                  subtitle: =@ctx.current.item.board
                left:
                  title: =@ctx.current.item.fromabrv
                  subtitle: =@ctx.current.item.disembark
          children:
            - type: component.entity
              options:
                children:
                  - type: component.field-row
                    options:
                      children:
                        - type: component.entity-field
                          options:
                            label: Boarding
                            value: =@ctx.current.item.from
                        - type: component.entity-field
                          options:
                            label: Destination
                            value: =@ctx.current.item.disembark
                  - type: component.field-row
                    options:
                      children:
                        - type: component.entity-field
                          options:
                            label: Board Time
                            value: =@ctx.current.item.board
                        - type: component.entity-field
                          options:
                            label: Disembark Time
                            value: =@ctx.current.item.disembark
                  - type: component.entity-field
                    options:
                      label: Passenger
                      value: =@ctx.current.item.name
                  - type: component.field-row
                    options:
                      children:
                        - type: component.entity-field
                          options:
                            label: Flight
                            value: =@ctx.current.item.flight
                        - type: component.entity-field
                          options:
                            label: Gate
                            value: =@ctx.current.item.gate
                        - type: component.entity-field
                          options:
                            label: Seat
                            value: =@ctx.current.item.seat
            - type: component.location
              options:
                address: =@ctx.current.item.to
```

datasources (static)

```yaml
datasources:
  flight-schedule-static:
    type: datasource.static
    options:
      data: 
        - id: 1
          airline: Get Stuff Done Airlines
          board: 11:30
          disembark: 12:30
          date: 30 Jul
          flight: A 0123
          from: Hawaii
          fromabrv: HNL
          gate: 16
          name: July Nelson
          seat: 12F
          to: New York
          toabrv: JFK
          image: https://images.unsplash.com/photo-1436491865332-7a61a109cc05?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxzZWFyY2h8MXx8cGxhbmV8ZW58MHx8MHx8&auto=format&fit=crop&w=500&q=60
        - id: 2
          airline: Get Stuff Done Airlines
          board: 08:10
          disembark: 10:45
          date: 30 Jul
          flight: A 5738
          from: Phoenix
          fromabrv: PHX
          gate: 2
          name: Nora Gordon
          seat: 27A
          to: Alabama
          toabrv: MCZ
          image: https://images.unsplash.com/photo-1464037866556-6812c9d1c72e?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxzZWFyY2h8Nnx8cGxhbmV8ZW58MHx8MHx8&auto=format&fit=crop&w=500&q=60
        - id: 3
          airline: Get Stuff Done Airlines
          board: 14:00
          disembark: 19:59
          date: 30 Jul
          flight: A 1123
          from: Iowa
          fromabrv: DSM
          gate: 15
          name: Tracy Matthews
          seat: 13F
          to: Ohio
          toabrv: DAY
          image: https://images.unsplash.com/photo-1488085061387-422e29b40080?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxzZWFyY2h8MTN8fHBsYW5lfGVufDB8fDB8fA%3D%3D&auto=format&fit=crop&w=500&q=60
```

datasources (dynamic)

```yaml
datasources:
  flight-schedule-dynamic:
    type: 'datasource.sqlite'
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
:::
:::::

