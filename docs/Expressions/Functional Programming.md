---
title: Functional Programming
slug: jSzt-functional
description: Learn how to use JSONata functional programming to compare values, display data, and more with this informative document. Explore code snippets, examples, and step-by-step guidance on comparing values, using variables in content, and implementing multiple
createdAt: Thu Jul 27 2023 13:15:54 GMT+0000 (Coordinated Universal Time)
updatedAt: Mon Sep 18 2023 13:18:44 GMT+0000 (Coordinated Universal Time)
---

You can use <a href="https://docs.jsonata.org/programming" target="_blank">JSONata Functional programming </a>to compare values or display data based on certain conditions. You can quickly make any logical statements, and based on the result, you can perform different actions.

## Configuration

| **Result**                                                         | **Expression**                                                                                                                                        |
| ------------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------- |
| Determine if the value is bigger or smaller than a certain number  | `"=@ctx.datasources.mydata.number2 > 10 
      ? 'Number is bigger':'Number is lower'"`                                                               |
| Variables                                                          | `="<div style='font-size: 40px'>Welcome on board      <b>" & @ctx.datasources.html.name & "</b>      - " & @ctx.datasources.html.email &
    "</div>` |

:::hint{type="warning"}
Be careful when using complex expressions, such as expressions that iterate one datasource across another, as your solution performance could become slower. To avoid this, try to use the datasource queries to get the desired result rather than an expression.
:::

## Examples and code snippets 

### Compare values

:::::VerticalSplit{layout="left"}
:::VerticalSplitItem
![Functional expressions](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/0uqaFEwFcsgWqmsxHy1uN_mk6aixjb8o06to7dpzsifimg0979iphone13blueportrait.png "Functional expressions")
:::

::::VerticalSplitItem
In this example we determine if the value for `entity.field` is bigger or smaller that 10.

See the full code sample in <a href="https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/guide-expressions/static-data/expression.jigx" target="_blank">GitHub</a>.&#x20;

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

children:
  - type: component.entity
    options:
      children:
        - type: component.entity-field
          options:
            label: Functional expression
            value: "=@ctx.datasources.mydata.number2 > 10 
                    ? 'Number is bigger':'Number is lower'"
```
:::
::::
:::::

### Variables in content

:::::VerticalSplit{layout="left"}
:::VerticalSplitItem
![Content](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/VAw06TIFPwJhNmAezMiwA_contentiphone13blueportrait.png "Content")
:::

::::VerticalSplitItem
This example shows how to write variables in HTML content.

See the full code sample in <a href="https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/guide-expressions/static-data/variablesInContent.jigx" target="_blank">GitHub</a>.

:::CodeblockTabs
variablesInContent.jigx

```yaml
source:
  documentType: HTML
  content: |
    ="<div style='font-size: 40px'>Welcome on board 
    <b>" & @ctx.datasources.html.name & "</b>
     - " & @ctx.datasources.html.email &
    "</div>
    <br />
    <img src='https://chart.googleapis.com/chart?cht=qr&chl=id"&@ctx.datasources.html.itemId&"&chs=380x380&choe=UTF-8&chld=L|2' alt='qr code'>
    <a href='https://www.qr-code-generator.com' border='0' style='cursor:default'  rel='nofollow'></a>
    <br />"  & @ctx.datasources.html.itemId
```
:::
::::
:::::

### Multiple select in a dropdown

:::::VerticalSplit{layout="left"}
:::VerticalSplitItem
![Multiple selector expression](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/q9ObXqaGM9y4_deRVoVdX_multipleselectiphone13blueportrait.png "Multiple selector expression")
:::

::::VerticalSplitItem
In this example, we use the notation in which we select the instanceId of our component from the components, and extract the selected from the state of the component, then choose the required value. For example id, name,...

See the full code sample in <a href="https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/guide-expressions/static-data/multipleSelect.jigx" target="_blank">GitHub</a>.

:::CodeblockTabs
multipleSelect.jigx

```yaml
children:
  - type: component.form
    instanceId: selected-people-form
    options:
      children:
        - type: component.dropdown
          instanceId: selected-people-dropdown
          options:
            label: Select people
            data: =@ctx.datasources.employees-static
            isMultiple: true
            item:
              type: component.dropdown-item
              options:
                title: =@ctx.current.item.firstname & ' ' & @ctx.current.item.lastname
                value: =@ctx.current.item.id
                leftElement: 
                  element: avatar
                  text: =$substring(@ctx.current.item.firstname, 0, 1) & $substring(@ctx.current.item.lastname, 0, 1)
                  uri: =@ctx.current.item.img
```
:::
::::
:::::

