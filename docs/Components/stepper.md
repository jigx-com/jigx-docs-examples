---
title: stepper
slug: RNdr-stepper
description: Learn how to use the versatile "Stepper" component to visually demonstrate the progress of tasks on your website. This document showcases various configuration options such as data, item, completedPercentage, and more. It also includes examples and code s
createdAt: Thu Jun 09 2022 19:48:29 GMT+0000 (Coordinated Universal Time)
updatedAt: Wed Jul 24 2024 09:58:36 GMT+0000 (Coordinated Universal Time)
---

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
This component displays the progress status of a task. Useful when tracking deliveries or claims. This component can only be used in a [jig.default](<./../Jig Types/jig_default.md>).
:::

:::VerticalSplitItem
![Stepper Preview](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/lRGV6B3arl4EitmWCT0SE_stepper.png "Stepper Preview")
:::
::::

## ****Configuration options

Some properties are common to all components, see [Common component properties](docId\:LLnTD-rxe8FmH7WpC5cZb) for a list and their configuration options.

| **Core structure**    |                                                                  |
| --------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `data`                | Define the data to be used in the step items, you can use expressions to reference a datasource.                                                                           |
| `item`                | There is only one available option, which is [step](./stepper/step.md). The `item` property is core for the stepper component, so even if you are creating a non-expandable stepper you must configure the step component's `title` and `value` properties with an empty string: "" |
| `completedPercentage` | Define the percentage to be displayed on the chart. Example "0.24" => 24 %. 1 represents 100% complete.                                                                       |

| **Other options** |           |
| ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `isExpandable`    | Set to `true` the stepper will be expandable into steps. Set to `false` the stepper is not expandable.        |
| `style`           | The styling determines the color of the chart. There are three colors options. For example if the status is complete use `isPositive` to show the chart in green. If no style is specified the chart shows in blue.&#xA; are styling sets:<br />* `isNegative` - red<br /* `isPositive` -  green<br />* `isWarning` - orange |
| `subtitle`        | The subtitle/short description of the stepper to display under the title. You can use an expression to set the subtitle.                                                                                       |
| `title`           | The title for the stepper, you can use an expression to set the title.  |

## Examples and code snippets

:::::ExpandableHeading
### Stepper example

::::VerticalSplit{layout="left"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/3q5XYI9fcgYMnxTTSMBaa_xqldilpo0dsaonqcdwm8ostepperiphone13blueportrait.png" size="88" position="center" caption="Stepper for shipment status" alt="Stepper for shipment status"}
:::

:::VerticalSplitItem
In this example, a stepper component shows that the task is half done. For completeness, use it together with the step component. After expanding the stepper, the individual steps will be shown.

**Examples**:
See the full example using static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/stepper/static-data/stepper-example/stepper-example.jigx).
See the full example using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/stepper/dynamic-data/stepper-example/stepper-example-dynamic.jigx).

**Datasource**:
See the full datasource for static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/adhoc-components/steps.jigx).
See the full datasource for dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/adhoc-components/steps-dynamic.jigx).
:::
::::

:::CodeblockTabs
stepper (static)

```yaml
children:
  - type: component.stepper
    options:
      data: =@ctx.datasources.steps
      isExpandable: true
      title: Shipment in transit
      item:
        type: component.step
        options:
          title: =@ctx.current.item.title
          description: =@ctx.current.item.description
          value: =@ctx.current.item.value 
          leftElement:
            element: icon
            icon: =@ctx.current.item.icon
          style:
            isPositive: =@ctx.current.item.isCompleted
            isActive: =@ctx.current.item.isActive
            isStrikeThrough: =@ctx.current.item.isCompleted
            isDisabled: =@ctx.current.item.isWaiting
      completedPercentage: 0.5
      style:  
        isPositive: false
        isWarning: false
        isNegative: false
```

stepper (dynamic)

```yaml
tchildren:
  - type: component.stepper
    options:
      data: =@ctx.datasources.steps-dynamic
      isExpandable: true
      title: Shipment in transit
      item:
        type: component.step
        options:
          title: =@ctx.current.item.title
          description: =@ctx.current.item.description
          value: =@ctx.current.item.value 
          leftElement:
            element: icon
            icon: =@ctx.current.item.icon
          style:
            isPositive: =@ctx.current.item.iscompleted
            isActive: =@ctx.current.item.isactive
            isStrikeThrough: =@ctx.current.item.iscompleted
            isDisabled: =@ctx.current.item.iswaiting
      completedPercentage: 0.5
      style:  
        isPositive: false
        isWarning: false
        isNegative: false
```

datasources (static)

```yaml
datasources:
  steps:
    type: datasource.static
    options:
      data:
        - title: Order
          value: step1
          icon: checkbox-checked
          isActive: false
          isCompleted: true
          isWaiting: false
        - description: The shipment is in transit.
          title: Shipment in transit
          value: step2
          icon: time-clock-circle
          isActive: true
          isCompleted: false
          isWaiting: false
        - title: On the way to you
          value: step3
          isActive: false
          isCompleted: false
          isWaiting: true
        - title: Delivered to the recipient
          value: step4
          isActive: false
          isCompleted: false
          isWaiting: true
```

datasources (dynamic)

```yaml
datasources:
  steps-dynamic:
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_DYNAMIC
      entities:
        - entity: default/steps
      query: |
        SELECT
          '$.title',
          '$.description',
          '$.value',
          '$.icon',
          '$.isactive',
          '$.iscompleted',
          '$.iswaiting'
        FROM [default/steps]
        ORDER BY value
```
:::
:::::

