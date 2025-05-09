---
title: Predicate Queries
slug: ELoX-pre
description: Learn how to filter and select specific values from an array using JSONata Predicate Queries. Discover how to use a predicate expression to display the name of a nurse with a specified color. This document includes a helpful code snippet and a direct link
createdAt: Thu Jul 27 2023 13:16:54 GMT+0000 (Coordinated Universal Time)
updatedAt: Mon Jul 31 2023 09:13:59 GMT+0000 (Coordinated Universal Time)
---

Use [JSONata Predicate Queries](https://docs.jsonata.org/predicate) at any location path; the selected items can be filtered using a predicate - **\<expr>** where expr evaluates to a Boolean value. With that, you can select values from the array based on the specific type set as the predicate expression.

## Configuration

| **Result**                         | **Expression**                                                  |
| ---------------------------------- | --------------------------------------------------------------- |
| Evaluate if true and show the name | `=@ctx.datasources.mydata[title='Nurse' and color='blue'].name` |

:::hint{type="warning"}
Be careful when using complex expressions, such as expressions that iterate one datasource across another, as your solution performance could become slower. To avoid this, try to use the datasource queries to get the desired result rather than an expression.
:::

## Examples and code snippets 

:::::VerticalSplit{layout="left"}
:::VerticalSplitItem
![Predicate queries](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/pJL_aAds1bbqRl0w5trhY_qfbtw3l1pzojf6xyfwlvvimg0976iphone13blueportrait.png "Predicate queries")


:::

::::VerticalSplitItem
In this example the expression is used to show the name of the nurse whose color is blue.

See the full code sample in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/guide-expressions/static-data/expression.jigx).

:::CodeblockTabs
expression.jigx

```yaml
datasources:
  mydata: 
    type: datasource.static
    options:
      data:
        - name: Jane Stevens
          title: Doctor
          email: jane@first.com
          number: 0.64734
          number2: 12
          color: blue
          time: '2021-11-07T15:07:54.972Z'
          array: [5,1,2,3,7,9]
        - name: Arthur Marks
          title: Nurse
          email: arthur@first.com
          number: 0.98
          number2: 10
          color: red
          time: '2021-11-07T15:07:54.972Z'
          array: [5,1,2,3,7,9]
        - name: Merley Shanks
          title: Nurse
          email: merley@first.com
          number: 0.43
          number2: 9
          color: blue
          time: '2021-11-07T15:07:54.972Z'
          array: [5,1,2,3,7,9]
children:
  - type: component.entity
    options:
      children:
        - type: component.entity-field
          options:
            label: Predicate expression
            value: =@ctx.datasources.mydata[title='Nurse' and color='blue'].name
```
:::
::::
:::::

