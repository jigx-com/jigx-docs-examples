# Aggregation

Use JSONata aggregation to return the results of values to find a maximum, minimum, or average value in an array.

## Configuration

| **Result** | **Expression**                         |
| ---------- | -------------------------------------- |
| Maximum    | `=$max(@ctx.datasources.mydata.array)` |
| Minimum    | `=$min(@ctx.datasources.mydata.array)` |
| Sum        | `=$sum(@ctx.datasources.mydata.array)` |

:::hint{type="warning"}
Be careful when using complex expressions, such as expressions that iterate one datasource across another, as your solution performance could become slower. To avoid this, try to use the datasource queries to get the desired result rather than an expression.
:::

## Examples and code snippets

::::VerticalSplit{layout="left"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/X11pn0BVv4LsvZydrxLVL_img6602iphone13blueportrait.png" size="78" position="center" caption="Aggregated expression" alt="Aggregated expression" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/X11pn0BVv4LsvZydrxLVL_img6602iphone13blueportrait.png"}
:::

:::VerticalSplitItem
In this example static data is agregated in a `component.enity` to show the result in the entity field.

See the full example code sample in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/guide-expressions/static-data/expression.jigx).
:::
::::

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
            label: Max
            value: =$max(@ctx.datasources.mydata.array)
        - type: component.entity-field
          options:
            label: Min
            value: =$min(@ctx.datasources.mydata.array)
        - type: component.entity-field
          options:
            label: Sum
            value: =$sum(@ctx.datasources.mydata.array)
```
:::

