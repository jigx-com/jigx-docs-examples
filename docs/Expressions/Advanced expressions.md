---
title: Advanced expressions
slug: 4nw7-a
createdAt: Wed Nov 15 2023 12:23:57 GMT+0000 (Coordinated Universal Time)
updatedAt: Wed Nov 15 2023 12:33:23 GMT+0000 (Coordinated Universal Time)
---

Use [Advanced Expressions]() to filter an array of records to display specific data and perform expression transformations over the data.

## Examples and code snippets 

### Create a filtered list from an array of records

We will display a list of people from the array of records, then filter them and display those that have entered a name. We will display their initials as a left avatar and add a label to each list item to display whether they are registered.&#x20;

:::::VerticalSplit{layout="left"}
:::VerticalSplitItem
![Result with Advanced Expressions](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/LGvYapk-Ctp7XNjyF1AhK_ldcfoljjvzbydshpyny6img1005iphone13blueportrait.png "Result with Advanced Expressions")


:::

::::VerticalSplitItem
See the full example in <a href="https://github.com/jigx-com/jigx-samples/blob/main/samples/jigx-samples/jigs/guide-advanced-expressions/static-data/advanced-expressions-list.jigx" target="_blank">GitHub.</a>

:::CodeblockTabs
advanced-expression.jigx

```yaml
title: List with advanced Expressions
type: jig.list

datasources:
  people:
    type: datasource.static
    options:
      data:
        - id: 1
          firstname: Mark
          lastname: Dobrew
          email: mark@gmail.com
          mobile: 783432565
          registered: false
        - id: 2
          firstname: Astra
          lastname: Courts
          email: astra@gmail.com
          mobile: 437874221
          registered: false
        - id: 3
          firstname: Jane
          lastname: Doe
          email: jane@gmail.com
          mobile: 783432531
          registered: true
        - id: 4
          firstname: ''
          lastname: ''
          email: steve@gmail.com
          mobile: 783432531
          registered: true

data: =@ctx.datasources.people[firstname != '' and lastname != '']
item:
  type: component.list-item
  options:
    title: "=@ctx.current.item.firstname 
            & ' ' & 
            @ctx.current.item.lastname"
    subtitle: ='Phone:' & @ctx.current.item.mobile
    description: ='Email:' & @ctx.current.item.email
    style:
      isHighlighted: "=@ctx.current.item.registered = true 
                      ? true:false"
    label:
      title: "=@ctx.current.item.registered = true 
              ? 'Registered':'Not registered'"
      color:
        - when: =@ctx.current.item.registered = true 
          color: color2
        - when: =@ctx.current.item.registered = false
          color: color4
    leftElement: 
      type: avatar
      text: "=$substring(@ctx.current.item.firstname,0,1) 
            & $substring(@ctx.current.item.lastname,0,1)"
```
:::
::::
:::::

### Define functions to run the expressions

As part of advanced expressions, you can define functions that will run the expressions. It can be a function for date transformations, maths calculations, or any string transformations. By using functions you will have cleaner code that is easier to read.

:::::VerticalSplit{layout="left"}
:::VerticalSplitItem
![Divided by 10](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/w4D0z4M_5GZfbVYTORcV1_hncb97qurvw7muuy4qigeimg1002iphone13blueportrait.png "Divided by 10")
:::

::::VerticalSplitItem
This example shows a simple function that will divide the number from the datasource.

See the full code sample in <a href="https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/guide-advanced-expressions/static-data/advanced-expressions-list.jigx" target="_blank">GitHub</a>.

:::CodeblockTabs
advanced-expression.jigx

```yaml
datasources:
  number-data:
    type: datasource.static
    options:
      data:
        - id: 1
          number: 2500
children:
  - type: component.entity
    options:
      children:
        - type: component.entity-field
          options:
            label: Expression to get result divided by 10
            value: =($b := function($l, $w){ $l / $w }; $b(@ctx.datasources.number-data.number,10);)
```
:::
::::
:::::

