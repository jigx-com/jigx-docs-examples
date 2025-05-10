---
title: expander
slug: MNoZ-expander
description: This document provides an in-depth discussion on the use of an expander component that allows users to display additional content by clicking on a small portion of the content. It explains various options available for the expander component, including st
createdAt: Thu Jun 09 2022 19:32:20 GMT+0000 (Coordinated Universal Time)
updatedAt: Tue Apr 29 2025 09:15:37 GMT+0000 (Coordinated Universal Time)
---

The expander component** **is a collapsible element that initially displays a small portion of content, such as a name. Users can tap the arrow, aligned either to the left or right, to expand the component and reveal additional details. The expander is customizable, and the content inside can be configured using components such as forms, lists, or cards. This helps keep screens clean and organized while making additional information easily accessible.


![Expander Preview](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/xDQizxD7Vjjgr1tbdQpPr_expander.png "Expander Preview")

## Configuration options

Some properties are common to all components, see [Common component properties](docId\:LLnTD-rxe8FmH7WpC5cZb) for a list and their configuration options.

| **Core structure** |                                               |
| ------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `children`         | Define the content of the expander. The following components can be used in the expander:<br />* [avatar](./avatar.md)<br />* [bar-chart](./charts/bar-chart.md)<br />* [entity](./entity.md)<br />* [form](./form.md)<br />* [interactive-image](./interactive-image.md)<br />* [line-chart](./charts/line-chart.md)<br />* [list](./list.md)<br />* [location](./location.md)<br />* [pie-chart](./charts/pie-chart.md)<br />* [stepper](./stepper.md)<br />* [video-player](./video-player.md)<br />* [web-view](./web-view.md) |
| `header`           | `centerElement` - what is initially visible in your jig. &#xA;The following options are available in `header`:<br />* component [stage](https://docs.jigx.com/examples/stage)<br />* component [titles](https://docs.jigx.com/examples/h1bm-titles).                                                                                                                                                                        |

| **Other options**      |              |
| ---------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `divider`              | Added the ability to add a solid or transparent `divider`. Default setting is `none`.                                                                    |
| `expandIcon`           | Allows the ability to customize the alignment of the expander button. Default setting is `right`.                                                        |
| `isInitiallyCollapsed` | If the expander is initially collapsed. `true` is the default setting.&#xA;`false` - expanded&#xA;`true` - collapsed                                     |
| `leftElement`          | Add a left element, for example, an ordering number or avatar.                                                                                           |
| `variant`              | Determine the background color for header versus body using the `variant` property with `plain` or `emphasized` values. Default setting is `emphasized`. |

| **Actions**    |        |
| ---------------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| `onContentPress` | Action triggered while pressing on the content in the expander. Use IntelliSense (ctrl+space) to see the available list of actions.  |

## Examples and code snippets

:::::ExpandableHeading
### Expander with titles in a header, entity-fields and bar-chart

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/XKqP3rQXzqg4vzPaen2DY_bzjgtccktzcmqfgs-mdseexpander-with-titles-in-a-headeriphone13blueportrait.png" size="80" position="center" caption="Expander with titles" alt="Expander with titles"}
:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/A-syqy6kp5jw7sh9vGb1t_ivsv2bndlkg7ebc6cdb8zexpander-with-titles-in-a-header2iphone13blueportrait.png" size="80" position="center" caption="Expander with bar-chart & entity-fields" alt="Expander with bar-chart & entity-fields"}
:::
::::

**Examples**:
See the full example using static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/expander/static-data/expander.jigx).
See the full example using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/expander/dynamic-data/expander-dynamic-data.jigx).

**Datasource**:
See the full datasource for dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/expanders%20and%20stages/expander-dynamic.jigx).

:::CodeblockTabs
expander (static)

```yaml
children:
  - type: component.expander
    options:
      header:
        centerElement: 
          type: component.titles
          options:
            title: July Nelson
            subtitle: Manager
            icon: person
            align: left
      children:
        - type: component.entity
          options:
            children:
              - type: component.field-row
                options:
                  children:
                    - type: component.entity-field
                      options:
                        label: Phone
                        value: "3249432812"
                    - type: component.entity-field
                      options:
                        label: Email
                        value: july@first.com
              - type: component.entity-field
                options:
                  label: Address
                  value: 141 Harbor Dr Claymont, Delaware(DE), 19703
        - type: component.bar-chart
          options:
            chart:
              title: 
                text: Last year revenue
            legend:
              isHidden: true
            series:
              - data: =@ctx.datasources.series1
```

expander (dynamic)

```yaml
children:
  - type: component.expander
    options:
      header:
        centerElement: 
          type: component.titles
          options:
            title: =@ctx.datasources.expander-dynamic.firstname & ' ' & @ctx.datasources.expander-dynamic.lastname
            subtitle: =@ctx.datasources.expander-dynamic.position
            icon: person
            align: left
      children:
        - type: component.entity
          options:
            children:
              - type: component.field-row
                options:
                  children:
                    - type: component.entity-field
                      options:
                        label: Phone
                        value: =@ctx.datasources.expander-dynamic.phone
                    - type: component.entity-field
                      options:
                        label: Email
                        value: =@ctx.datasources.expander-dynamic.email
              - type: component.entity-field
                options:
                  label: Address
                  value: =@ctx.datasources.expander-dynamic.address
        - type: component.bar-chart
          options:
            chart:
              title: 
                text: Last year revenue
            legend:
              isHidden: true
            series:
              - data: =@ctx.datasources.series1-dynamic
```

datasources (dynamic)

```yaml
datasources:
  expander-dynamic:
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_DYNAMIC
      entities:
        - entity: default/employees
      query: | 
        SELECT 
          id,
          '$.firstname',
          '$.lastname',
          '$.picture', 
          '$.date_from', 
          '$.date_to', 
          '$.email',
          '$.phone', 
          '$.position', 
          '$.address', 
          '$.category' 
        FROM [default/employees] WHERE '$.firstname' = "July" AND '$.category' = 'employees'
```
:::
:::::

:::::ExpandableHeading
### Expander with stage in header and entity-field

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/BCWgmHKWYvB2jD2gt9jHK_hs8ymbcaghjk2zqrbi6daexpander-with-stageiphone13blueportrait.png" size="80"  position="center" caption="Expander with stage" alt="Expander with stage"}
:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/ANaskxsOt0saAl1DqnWtu_rsfux7yzcblgkgbnpyu-expander-stage2.png" size="80"  position="center" caption="Expander with stage & entity" alt="Expander with stage & entity"}
:::
::::

**Examples**:
See the full example using static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/expander/static-data/expander-trip.jigx).
See the full example using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/expander/dynamic-data/expander-trip-dynamic-data.jigx).

**Datasource**:
See the full datasource for dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/adhoc-components/trip-dynamic.jigx).

:::CodeblockTabs
expander-trip (static)

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
            left:
              title: New York
      children:
        - type: component.entity
          options:
            children:
              - type: component.field-row
                options:
                  children:
                    - type: component.entity-field
                      options:
                        label: Passanger name
                        value: July Nelson
                    - type: component.entity-field
                      options:
                        label: Date
                        value: 25 Jul
                    - type: component.entity-field
                      options:
                        label: Time
                        value: 12:30
              - type: component.field-row
                options:
                  children:
                    - type: component.entity-field
                      options:
                        label: From
                        value: Boston
                    - type: component.entity-field
                      options:
                        label: Flight
                        value: A 0123
                    - type: component.entity-field
                      options:
                        label: Seat
                        value: 12F
              - type: component.field-row
                options:
                  children:
                    - type: component.entity-field
                      options:
                        label: To
                        value: New York
                    - type: component.entity-field
                      options:
                        label: Gate
                        value: '16'
                    - type: component.entity-field
                      options:
                        label: Board till
                        value: 11:30
          
```

expander-trip (dynamic)

```yaml
children:
  - type: component.expander
    options:
      header:
        centerElement: 
          type: component.stage
          options:
            right:
              title: =@ctx.datasources.trip-dynamic.to
            left:
              title: =@ctx.datasources.trip-dynamic.from
      children:
        - type: component.entity
          options:
            children:
              - type: component.field-row
                options:
                  children:
                    - type: component.entity-field
                      options:
                        label: Passanger name
                        value: =@ctx.datasources.trip-dynamic.name
                    - type: component.entity-field
                      options:
                        label: Date
                        value: =@ctx.datasources.trip-dynamic.date
                    - type: component.entity-field
                      options:
                        label: Time
                        value: =@ctx.datasources.trip-dynamic.time
              - type: component.field-row
                options:
                  children:
                    - type: component.entity-field
                      options:
                        label: From
                        value: =@ctx.datasources.trip-dynamic.from
                    - type: component.entity-field
                      options:
                        label: Flight
                        value: =@ctx.datasources.trip-dynamic.flight
                    - type: component.entity-field
                      options:
                        label: Seat
                        value: =@ctx.datasources.trip-dynamic.seat
              - type: component.field-row
                options:
                  children:
                    - type: component.entity-field
                      options:
                        label: To
                        value: =@ctx.datasources.trip-dynamic.to
                    - type: component.entity-field
                      options:
                        label: Gate
                        value: '16'
                    - type: component.entity-field
                      options:
                        label: Board till
                        value: =@ctx.datasources.trip-dynamic.board
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
:::
:::::

:::::ExpandableHeading
### Expander with variant, divider & expandIcon

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
This example includes four expander components, each configured with different options for the `variant`, `divider`, and `expandIcon` properties.

1. Expander configured with a `plain` variant & `transparent` divider.
2. Expander configured with `emphasized` variant & no divider.
3. Expander configured with no variant and a `solid` divider.
4. Expander configured with expandIcon aligned to the `left`, `plain` variant & no divider.
:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-LLslE6fh7WCJh3cp8G37g-20250424-093658.gif" size="66" position="center" caption="Expander options" alt="Expander options"}
:::
::::

:::CodeblockTabs
expander-variant.jigx

```yaml
title: Deliveries
type: jig.default

header:
  type: component.jig-header
  options:
    height: small
    children:
      type: component.image
      options:
        source:
          uri: https://images.unsplash.com/photo-1536607278842-2e762f290252?w=500&auto=format&fit=crop&q=60&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8MTF8fGRlbGl2ZXJ5JTIwdHJ1Y2t8ZW58MHx8MHx8fDA%3D
 
children:
  - type: component.section
    options:
      title: EXPANDER WITH VARIANT (plain), DIVIDER (transparent)
      children: 
     # First expander.                
      - type: component.expander
        options:
        # Configure a plain variant.  
          variant: plain
          #Add a transparent divider.
          divider: transparent
          header:
            centerElement: 
              type: component.titles
              options:
                icon: truck-1
                iconColor: color2
                align: right
                title: =@ctx.datasources.product-delivery[0].destination
                subtitle: =@ctx.datasources.product-delivery[0].deliveryId
          children:
            - type: component.list-item
              options:
                title: =@ctx.datasources.product-delivery.Item
                subtitle: =@ctx.datasources.product-delivery[0].expectedDelivery
                isContained: true
                rightElement: 
                  element: value
                  text: =@ctx.datasources.product-delivery[0].status
  - type: component.divider
  - type: component.section
    options:
      title: EXPANDER WITH VARIANT - EMPHASIZED
      children:
      # Second expander. 
      - type: component.expander
        options:
         # Configure an emphasized variant.
          variant: emphasized
          header:
            centerElement: 
              type: component.stage
              options:
                icon: truck-cargo
                right:
                  title: =@ctx.datasources.product-delivery[1].deliveryId
                left:
                  title: =@ctx.datasources.product-delivery[1].status
          children:
            - type: component.entity
              options:
                children:
                  - type: component.entity-field
                    options:
                      label: Product
                      value: =@ctx.datasources.product-delivery[1].Item
                  - type: component.entity-field
                    options:
                      label: Destination
                      value: =@ctx.datasources.product-delivery[1].destination  
                  - type: component.entity-field
                    options:
                      label: Destination
                      value: =@ctx.datasources.product-delivery[1].expectedDelivery  
  - type: component.divider                       
  - type: component.section
    options:
      title: EXPANDER WITH SOLID DIVIDER
      children:
      # Third expander.
      - type: component.expander
        options:
          # Add a solid divider,
          # that displays when the component is expanded.
          divider: solid
          header:
            centerElement: 
              type: component.titles
              options:
                align: left
                title: =@ctx.datasources.product-delivery[2].deliveryId
                subtitle: =@ctx.datasources.product-delivery[2].expectedDelivery       
          children:
            - type: component.list-item
              options:
                title: =@ctx.datasources.product-delivery[2].destination
                subtitle: =@ctx.datasources.product-delivery[2].Item
                color: color4
                leftElement: 
                  element: icon
                  icon: delivery-truck
                rightElement: 
                  element: value
                  text: =@ctx.datasources.product-delivery[2].status
            - type: component.location
              options:
                viewPoint:
                  address: New York, NY 10001, United States
  - type: component.divider
  - type: component.section
    options:
      title: EXPANDER WITH ICON ALIGNMENT & VARIANT (plain)
      children:
      # Fourth expander. 
      - type: component.expander
        options:
         # Configured a plain variant. 
          variant: plain
          header:
            # Configure the expander icon to display on the left.
            expandIcon:
              align: left
            centerElement: 
              type: component.stage
              options: 
                icon: truck-cargo-1
                right:
                  title: =@ctx.datasources.product-delivery[3].status
                left:
                  title: =@ctx.datasources.product-delivery[3].deliveryId                           
          children:
            - type: component.entity
              options:
                children:
                  - type: component.entity-field
                    options:
                      rightIcon: calendar-3
                      style:
                        isWarning: true
                      label: Delivery date
                      value: =@ctx.datasources.product-delivery[3].expectedDelivery
```

product-delivery.jigx

```yaml
type: datasource.sqlite
options:
  provider: DATA_PROVIDER_DYNAMIC

  entities:
    - default/product-delivery

  query: 
    SELECT id,
     '$.deliveryId',
     '$.Item',
     '$.destination',
     '$.status',
     '$.expectedDelivery'
    FROM [default/product-delivery]
  
```
:::
:::::

