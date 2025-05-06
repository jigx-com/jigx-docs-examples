---
title: Date & Time
slug: p6OO-date
description: Learn how to manipulate date and time expressions using JSONata Date/Time functions with this comprehensive document. Discover configuration examples to retrieve the current timestamp in different formats like ISO 8601, milliseconds, date, time, and more.
createdAt: Thu Jul 27 2023 13:16:08 GMT+0000 (Coordinated Universal Time)
updatedAt: Tue May 14 2024 12:00:54 GMT+0000 (Coordinated Universal Time)
---

Date and time expressions use the <a href="https://docs.jsonata.org/date-time-functions" target="_blank">JSONata Date/Time functions</a> to return various formats of date/time, date, or time. These expressions are used to get the current timestamp in ISO 8601 formatted string, use an expression over the timestamp to convert the timestamp into a specific format.

## Configuration

| **Result**                                                     | **Expression**                                                             |
| -------------------------------------------------------------- | -------------------------------------------------------------------------- |
| Current timestamp as ISO 8601                                  | `=$now()`                                                                  |
| Current datetime in milliseconds                               | `=$toMillis($now())`                                                       |
| Current date \[M]/\[D]/\[Y]                                    | `=$fromMillis($toMillis($now()), '[M]/[D]/[Y]')`                           |
| Current date \[M01]/\[D01]/\[Y0001]                            | `=$fromMillis($toMillis($now()), '[M01]/[D01]/[Y0001]')`                   |
| Current datetime '\[M01]/\[D01]/\[Y0001] \[H01]:\[m01]:\[s01]' | `=$fromMillis($toMillis($now()), '[M01]/[D01]/[Y0001] [H01]:[m01]:[s01]')` |
| Current date \[MI]/\[DI]/\[YI]                                 | `=$fromMillis($toMillis($now()), '[MI]/[DI]/[YI]')`                        |
| Current date \[D1o] \[MNn] \[Y]                                | `=$fromMillis($toMillis($now()), '[D1o] [MNn] [Y]')`                       |
| Current day                                                    | `=$fromMillis($toMillis($now()), '[FNn]')`                                 |
| Current time                                                   | `=$fromMillis($toMillis($now()), '[H01]:[m01]:[s01]')`                     |
| Current time am/pm                                             | `=$fromMillis($toMillis($now()), '[h#1]:[m01][P]')`                        |
| Current time '\[H01]:\[m01]:\[s01] \[z]', '-0500'              | `=$fromMillis($toMillis($now()), '[H01]:[m01]:[s01] [z]', '-0500')`        |
| Convert UTC to milliseconds                                    | `=$toMillis()`                                                             |
| Convert millisecond to UTC                                     | `=$fromMillis()`                                                           |

## Consideration

- When using `=$now()` on a component level,  the date/time is not refreshed when navigating out and into the jig. To cater to this scenario, add an `onFocus` with a `set-state` action to the jig.

:::CodeblockTabs
component

```yaml
children:
  - type: component.entity
    options:
      children:
        - type: component.entity-field
          options:
            label: Order Date
            value: =@ctx.solution.state.now
```

onFocus

```yaml
onFocus: 
  type: action.set-state
  options:
    state: =@ctx.solution.state.now
    value: =$now()
```
:::

:::hint{type="warning"}
Be careful when using complex expressions, such as expressions that iterate one datasource across another, as your solution performance could become slower. To avoid this, try to use the datasource queries to get the desired result rather than an expression.
:::

## Examples and code snippets 

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem


::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/rLyfpAJd6UWubCCOtnOx8_img6600iphone13blueportrait.png" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/rLyfpAJd6UWubCCOtnOx8_img6600iphone13blueportrait.png" size="72" width="1570" height="2932" position="center" caption="Date & time expressions" alt="Date & time expressions"}
:::

:::VerticalSplitItem
This example uses a component.enitity to show the results of various date/time functions&#x20;

See the full code sample in <a href="https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/guide-expressions/static-data/expression.jigx" target="_blank">GitHub</a>.&#x20;
:::
::::

:::CodeblockTabs
expression.jigx

```yaml
children:
  - type: component.entity
    options:
      children:
        - type: component.entity-field
          options:
            label: Current timestamp as ISO 8601
            value: =$now()
        - type: component.entity-field
          options:
            label: Current datetime in milliseconds
            value: =$toMillis($now())
        - type: component.entity-field
          options:
            label: Current date [M]/[D]/[Y]
            value: =$fromMillis($toMillis($now()), '[M]/[D]/[Y]')
        - type: component.entity-field
          options:
            label: Current date [M01]/[D01]/[Y0001]
            value: =$fromMillis($toMillis($now()), '[M01]/[D01]/[Y0001]')
        - type: component.entity-field
          options:
            label: Current datetime '[M01]/[D01]/[Y0001] [H01]:[m01]:[s01]'
            value: =$fromMillis($toMillis($now()), '[M01]/[D01]/[Y0001] [H01]:[m01]:[s01]')
        - type: component.entity-field
          options:
            label: Current date [MI]/[DI]/[YI]
            value: =$fromMillis($toMillis($now()), '[MI]/[DI]/[YI]')
        - type: component.entity-field
          options:
            label: Current date [D1o] [MNn] [Y]
            value: =$fromMillis($toMillis($now()), '[D1o] [MNn] [Y]')
        - type: component.entity-field
          options:
            label: Current day
            value: =$fromMillis($toMillis($now()), '[FNn]')
        - type: component.entity-field
          options:
            label: Current time
            value: =$fromMillis($toMillis($now()), '[H01]:[m01]:[s01]')
        - type: component.entity-field
          options:
            label: Current time am/pm
            value: =$fromMillis($toMillis($now()), '[h#1]:[m01][P]')
        - type: component.entity-field
          options:
            label: Current time '[H01]:[m01]:[s01] [z]', '-0500'
            value: =$fromMillis($toMillis($now()), '[H01]:[m01]:[s01] [z]', '-0500')
```
:::

